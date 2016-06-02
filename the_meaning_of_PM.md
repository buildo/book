# Product Management

We often talk about project managers, and refer to what we do as projects, but *what is a project?*

The [PMI](http://www.pmi.org/) defines a project like this:
> A project can be defined as a **temporary endeavor undertaken to create a unique product or service.**

> Projects are different from other ongoing operations in an organization, because unlike operations, projects have a definite beginning and an end - they have a **limited duration**.

Others use projects to create the `v1.0` of a new product. We use [MVPs](https://en.wikipedia.org/wiki/Minimum_viable_product).

They use projects to plan and execute every new release. We use [continuous delivery](http://martinfowler.com/bliki/ContinuousDelivery.html) to incrementally bring value to our customers.

In buildo, big projects don't exist. That's why we don't need a lot of traditional project management. The following sections outline our product management workflow, a continuous flow that starts with customer requests and ends with delivered business value.

**disclaimer: ** we'll still refer to our products as projects, and talk about project managers, that's life. As long as we understand the fundamental difference between a project and a product, we should be fine. 

## PRISMA flow

1. Everything starts from a new **request** in Trello, typically added directly by the customer.
2. The requests is then refined, following our **requirements gathering guidelines**, and it becomes actionable by buildo.
3. The **actionable request** is then transformed into a GitHub issue, and tracked as a backlog card in Trello.
4. completion of the issue in GitHub triggers PRISMA to move the backlog card to "done"
5. in PRISMA a few more steps for approval and QA are set, depending on product needs

We call this the **PRISMA flow**. In this section we explain in detail this flow.

The PRISMA flow is a template on which to build your specific product development flow. Each product is different, and has a different implementation of the flow, but all flows..

- start from the PRISMA flow as a guideline
- are specified in written form
- are fully discussed and shared with the development team and the customer

Let's get serious:

![](PRISMA flow.png)


