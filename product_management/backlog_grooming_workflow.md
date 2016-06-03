# Backlog grooming workflow
![](backlog_grooming.png)

This workflow starts from actionable requests, the output of requirements gathering, into a prioritized list of issues for developers, the **backlog**.

A backlog is well groomed if:
- issue requirements are of good quality and provide the necessary level of detail
- priorities are meaningful both for the customer and for buildo
- the backlog is long enough to keep developers busy on useful issues

## Converting actionable requests into issues

This is where we convert a Trello card to a GitHub issue. We are converting from customer language to developer language.

The exact conversion depends on the team. Typically, bigger teams will need more detailed reqs on issues, and the translated issue will be very different.

At the opposite side, for "teams" with a single person doing PM and dev this step is very light.

### Requirements and Specs

As described in the chapter on [Development Workflow](../workflow/README.md), GitHub issues are typically written in the form or **requirements** and **specs**.

In the "prepare for dev" step, we write the requirements. The specs will be written by the developer assigned to the issue.

As usual, this is not 100% applicable. There are times when you want to suggest some specs, or cannot provide complete requirements. In that case, use explicit words such as **DRAFT** or **suggestion** to mark those exceptions.

**What is the difference between requirements and specs?**

As ususal, let's read the [first answer](http://programmers.stackexchange.com/questions/121289/what-is-the-difference-between-requirements-and-specifications) on stackexchange:

> requirements are what your program should do, the specifications are how you plan to do it.

Ehm.. sure, but it just doesn't work like that :( It's difficult to distinguish the what from the how, it depends on:

- the level of detail of the issue
- the person that wrote the issue (more tech or more PM?)
- the issue assignee (how much do they know the product?)
- ...

The definition we use in buildo is:

**Requirements are a description of what to build.
Specs are a description of what to build *written after requirements*, with *higher level of detail* and typically by the person who implements.**

You can see the product development process as a progressive refinement of requirements into specs, first as cards "to be discussed" that become "actionable requests", then in GitHub issues. Same concepts apply.

### Completeness, consistency and detail

When you write requirements in GitHub, your job is to make sure that they are:
- **complete** with respect to the requirements in Trello
- **consistent** internally, and with the existing product
- with the **right level of detail** for the assigned developer

![](reqs_quality_detail.png)

**[BAD]** If your requirements are incomplete, inconsistent and also with little details, the developer will typically complain and ask you to improve them.

**[DANGER]** If you requirements are incomplete, inconsistent but with a lot of details, the developer will typically go and implement something **broken by design ®**. This is because **detail is a proxy for quality, but often a false friend**. Always remember that, if you want to provide a lot of details, your effort to keep requirements complete and consistent will grow likewise.

## Estimating and managing priorities
