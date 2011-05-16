---
title: Who Watches the Observers?
author: Chandu Tennety
layout: post
excerpt: |-
  ActiveRecord Observers are useful when we need to keep tabs on our models without cluttering up the model with distracting callbacks. The interesting part is getting the Observers to watch only what we want them to watch.
---

[ Janova ](http://www.janova.us) is not purely about running tests in
isolation. It is a full-fledged multi-user environment, with user
permissions that can be set to read-only or read-and-write. Under these
conditions, it becomes important, especially for someone like a QA
Manager to know which parts of an application were modified and by
whom. In other words, Janova needs to track activities performed by
users in order to maintain a record of test development within an
application.

In the Rails world, this situation is an ideal candidate for utilizing
ActiveRecord Observers. I will not go into the details of how they
work, the [ Rails API ](http://railsapi.com/doc/rails-v2.3.8/classes/ActiveRecord/Observer.html)
does a more than adequate job. In this post, I would like to point out
some nuggets I discovered in the process.

### What Changed?

When monitoring user activities, most of the time it is enough to know
when something changed, as in "User A updated Feature B last night at
10:00pm". For these cases, a generic `after_update` callback works fine.

At other times, however, we need to know not only when, but also _what_
changed. For example, say Feature B is about to be picked up by User A.
The QA Manager assigns the feature to that user, and expects a status
update when the user has begun working on the feature. User A begins
work in earnest, but has to take an unplanned leave of absence. The QA
Manager, agile as ever, assigns the feature to User C, who rolls up her
sleeves and picks up the slack.

In this process, Feature B has already undergone three changes in
assignment status:

  1. Assignee: none to User A (made by QA Manager),
  1. Status: Not Started to Started (made by User A), and
  1. Assignee: User A to User C (made by QA Manager).

In this case, a simple `after_update` isn't enough, we need to know what
kind of update was made. We could equivocate and provide all the changes
and let the users sort out what went before and what came after:

> QA Manager changed the assignment of Feature A to User B with a
  status of Not Started

> User B changed the assignment of Feature A to User B with a status
  of Started

> QA Manager changed the assignment of Feature A to User C with a
  status of Started

But Janova is better than that. And certainly, so is Rails.

### Asking the Right Questions

In fact, the Rails team has already thought of this use case and given
us a way out with the `attribute_changed?` method. Not only that, they
have ( oh so elegantly! ) wired it into any model attribute, so that with
our feature assignment, we can ask it to tell us whether a particular
attribute was updated.

Let's look at the changes once again with their `attribute_changed?`
values:

  1. Assignee: none to User A <div class="inline vim_block"># assignee\_changed? => true<br /># assignment\_status\_changed? => false</div>
  1. Status: Not Started to Started <div class="inline vim_block"># assignee\_changed? => false<br /># assignment\_status\_changed? => true</div>
  1. Assignee: User A to User C <div class="inline vim_block"># assignee\_changed? => true<br /># assignment\_status\_changed? => false</div>

Armed with this information, we can simply render different update
activities with the same `after_update` callback: if the assignee has
changed, tell us to whom the feature was assigned; otherwise, tell us
to what assignment status the feature was changed. With this logic,
we get much better activity readouts:

> QA Manager changed the assignment of Feature A to User B

> User B changed the status of Feature A to Started

> QA Manager changed the assignment of Feature A to User C

### Conclusion
If so inclined, we could ask the model not just what the change was, but
also what the value was before the change, so we could report something
like this:

> QA Manager changed the assignment of Feature A **from none** to User B

In the present example, this was not required. This example serves to
demonstrate, however, that with the power and elegance of Rails, Janova
continues to evolve into a richer product every day.
