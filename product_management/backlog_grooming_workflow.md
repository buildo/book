# Open Issues

This workflow transforms actionable requests, the output of requirements gathering, into a list of issues for developers, the **backlog**.

![](/assets/open_issues.png)

### Requirements and Specs

As described in the chapter on [Development Workflow](../workflow/README.md), GitHub issues are typically written in the form or **requirements** and **specs**.

In the "prepare for dev" step, we do 2 things:

1. **challenge the PM:** make sure the requirements are complete and sound, and the request overall makes sense.
2. **draft specs:** in particular for complex issues, this is the time when a draft of the specs is written, typically with the help of a Tech Lead and/or other developers. 

There are times when you know the requirements are not complete, or the specs are very tentative. In that case, use explicit words such as **DRAFT** or **suggestion** to mark those exceptions.

**What is the difference between requirements and specs?**

As usual, let's read the [first answer](http://programmers.stackexchange.com/questions/121289/what-is-the-difference-between-requirements-and-specifications) on stackexchange:

> requirements are **what** your program should do, the specifications are **how** you plan to do it.

Ehm.. sure, but it just doesn't work like that :( It's difficult to distinguish the what from the how, it depends on:

* the level of detail of the issue
* the person that wrote the issue (more tech or more PM?)
* the issue assignee (how much do they know the product?)
* ...

The definition we use in buildo is:

**Requirements** are a description of **what to build.**

**Specs** are a description of **what to build and how**, written by the **DEV team** after requirements, with **higher level of detail**.

You can see the product development process as a progressive refinement of requirements into specs, first as cards "to be refined" that become "actionable requests", then in GitHub issues. Same concepts apply.

### Completeness, consistency and detail

As a PM, when you write requirements, your job is to make sure that they are:

* **complete** with respect to the requirements in Trello
* **consistent** internally, and with the existing product
* with the **right level of detail** for the assigned developer

![](reqs_quality_detail.png)

**[BAD]** If your requirements are incomplete, inconsistent and also with little details, the developer will typically complain and ask you to improve them.

**[DANGER]** If your requirements are incomplete, inconsistent but with a lot of details, the developer will typically go and implement something **broken by design®**. This is because **detail is a false proxy for completeness and consistency**. Always remember that, if you want to provide a lot of details, your effort to keep requirements complete and consistent will grow likewise.

**[OK]** If you requirements are complete, consistent and have a level of detail that make the issue actionable for the developer, they are OK. The key here is to know your developers, and their level of knowledge of the product, striving to provide the right level of detail.  
If you give more, you're missing out on the developer's abilities and failing to trust and delegate.  
If you give less, you're making it too hard for developers to implement and inevitably causing many roundtrips of questions in the future.

## [optional] Estimating and managing priorities

The customer handles priorities. However, we need to give an idea of the effort required so that they can prioritize.

All cards in backlog can have an **effort label**. Typically we have:

![](effort_label.png)

Effort labels can be set by the PM, Dev Lead or asking directly to developers. It depends on the team.

This is not a perfect estimation system because:

* we don't incorporate feedback, as we're not tracking implementation time
* we don't do blind estimation with many people involved

This is fine, our goal here is to provide high level guidance to the customer about what takes long, and what doesn't.

This step is only necessary if the customer is actively involved in prioritizing in Trello, but can be avoided if prioritization is done live in recurrent meetings.

