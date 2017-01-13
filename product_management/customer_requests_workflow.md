# Manage requests and defects



![](/assets/manage_requests_and_defects.png)

Every request must be tracked in PRISMA. If possible, customers should be trained to submit new requests directly in the Trello board, typically in a column called `requests to be refined`. If not possible, the PM will manually add requests here as they come.

The `(r)` at the beginning of a column name tells PRISMA to let you open a GitHub issue directly from the card, maintaining traceability.

Typically we have 4 requests columns:

* `icebox` requests that are on hold, buildo does not work on these
* `requests to be refined` requests that need to be refined and transformed into actionable requests
* `bug reports` bug reports that need to be verified \(can come from the customer, the PM or the DEV team\)
* `(r) actionable requests` requests ready to be prepared for development, kept here in a prioritized list

The PM is responsible for transforming all requests \(except those in icebox\) into actionable requests. We refer to this process as **requirements gathering**.

## Requirements gathering guidelines

buildo is not a mere executor. **buildo helps customers in defining exactly what they want**.

This process, helping a customer defining their wish, is "requirements gathering".

Our objective is to shape a customer wish into a set of requirements that are:

* **effective**: fully respond to the _real_ customer need
* **efficient**: our mission is not to charge extra hours whenever possible
* **actionable**: complete, consistent, and with a sufficient level of details for buildo to execute

It's a 2 step process:  
1. understand the real business need  
2. design a solution

We won't go into detail for the second step, as we don't have yet some magic guideline to help you do good design.

On the contrary, understanding the real business need might seem trivial, but requires practice and can have devastating results if not taken seriously.

### The XY problem

The most authoritative definition of the [XY problem](http://xyproblem.info/) is, as usual, in stack exchange:

> The XY problem is asking about your attempted solution rather than your actual problem.
>
> That is, you are trying to solve problem X, and you think solution Y would work, but instead of asking about X when you run into trouble, you ask about Y.

You can find the full question and answers [here](http://meta.stackexchange.com/questions/66377/what-is-the-xy-problem), it's an interesting read.

We face this problem all the time with our customers. They have a problem, which we'll call **business need**, but they start talking about _a_ solution. For example, they need to notify their user quickly when a specific event happen, but instead of explaining their business need, they start asking about a push notification system.

At times the solution is the perfect one, but in general it will be sub-optimal in terms of efficiency and effectiveness.

### Solutions to the XY problem

Just look for the most upvoted comment, of course:

![](5whys.png)

The [5 Whys technique](https://en.wikipedia.org/wiki/5_Whys) is typically used to find the root cause of a problem in a chain of cause-effect.

We can follow a similar approach, asking our customer **why** they need a push notification system. And when they tell you "to let users know this happened", ask **why** they need to know. And when you discover that they need to know so that they can react right away, ask **why** they need to react so quickly. After only 3 whys, you might discover that a reaction time of 1 week is perfectly fine.

And you can simply add an email to the existing email notification module. Turns out the customer solution was inefficient.

Or maybe they want to add an additional field in a form, **why**? _Because we need that information._ **Why**? _Because from that information we get relevant metrics._ And you say.. _do you know how many people actually complete those extra fields? 5%_.

Ah.

Well, turns out we need to do something much more complex and costly to get that information. In this case, the customer solution was not effective.

### User Stories as a way to communicate requests

It is encouraged to write user stories in Trello to better define a feature. If possible, the customer should be trained to write user stories themselves.

Without going into much detail, a user story is composed of:

* who: **as a **student
* what: **I want to **download my schedule in PDF
* why: **so that **I can print it and bring it too school, where we don't have Wi-Fi

This way of expressing requests gives us insight as to why the feature is necessary, and who will be the user of this feature. This lets us optimize our requirements gathering discussion.

**Important: **User stories are useful both for external and internal requests. Many times the line between a customer and us is blurred in PRISMA. Someone in the back-end team might act as a customer w.r.t. the front-end team, of more often the PM acts as the customer. User stories are still suggested as a way to express requests.

The request template looks like this:

![](/assets/request_template.png)

1. The first step is to define the stories \(high level who, what, why\). 
2. Then, detailed requirements are written \(the "what"\). 
3. Specs are typically written later on \(in the "prepare for dev" step\), but hints or a draft can be added here as well



