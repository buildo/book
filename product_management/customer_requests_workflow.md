# Customer requests workflow
![](customer_requests.png)

Every request must be tracked in PRISMA. If possible, customers should be trained to submit new requests directly in the Trello board, tipically in a column called `(r) requests to be discussed`. If not possible, the PM will manually add requests here as they come.

The `(r) ` at the beginning of a column name tells PRISMA to treat that column as a request column. This adds a feature to let you open a GitHub issue directly from the card maintaining traceability.

Typically we have 4 requests columns:

- `(r) icebox` requests that are on hold, buildo does not work on these
- `(r) requests to be discussed` requests that need to be refined and transformed into actionable requests
- `(r) bug reports` bug reports from the customer are just a special kind of request to be discussed, but it's useful to keep them apart
- `(r) actionable requests` requests ready to go to the next step (backlog grooming)

The PM is responsible for transforming all requests (except those in icebox) into actionable requests. We refer to this process as **requirements gathering**.

## Requirements gathering guidelines

buildo is not a mere executor. **buildo helps customers in defining exactly what they want**.

This process, helping a customer defining their wish, is requirements gathering.

Our objective is to shape a customer wish into a set of requirements that are:

- **effective**: fully respond to the *real* customer need
- **efficient**: our mission is not to charge extra hours whenever possible
- **actionable**: complete, consistent, and with a sufficient level of details for buildo to execute

It's a 2 step process:
1. understand the real business need
2. design a solution

We won't go into detail for the second step, as we don't have yet some magic guideline to help you do a good and efficient design.

On the contrary, understanding the real business need might seem trivial, but requires practice and can have devastating results if not taken seriously.

### The XY problem

The most authoritative definition of the [XY problem](http://xyproblem.info/) is, as usual, in stack exchange:

> The XY problem is asking about your attempted solution rather than your actual problem.

> That is, you are trying to solve problem X, and you think solution Y would work, but instead of asking about X when you run into trouble, you ask about Y.

You can find the full question and answers [here](http://meta.stackexchange.com/questions/66377/what-is-the-xy-problem), it's an interesting read.

We face this problem all the time with our customers. They have a problem, which we'll call **business need**, but they start talking about *a* solution. For example, they need to notify their user quickly when a specific event happen, but instead of explaining their business need, they start asking about a push notification system.

At times the solution is the perfect one, but in general it will be sub-optimal in terms of efficiency and effectiveness.

### Solutions to the XY problem

### Practical example

    - client: I want a signup form and a profile page!!
    - PO: why do you want a signup form?
    - client: so that people can sign up and have their profile page //this is not a business need
    - PO: why should people have a profile page?
    - because they need to easily find their previous contracts //this is a business need, but not really basic because it doesn’t touch basic things such as retention, revenue, etc..?
    - PO: why do they need to easily find previous contracts?
    - client: because they already put information in those contracts, such as maybe a client they collaborate with a lot, and they can easily find such information and use it in new contracts
    - PO: ok, so your need is to optimize the experience of creating new contracts, by facilitating information retrieval, so that more people will complete a contract and sales will increase. Correct?
    - client: yes yes, and maybe if you have previous contracts you can click “duplicate” and use them as templates.
    - PO: sure, let me think about this a bit more (PO asks a dev or does himself some data gathering about how much data is actually reused, tries to validate the client’s assumptions with data and if not possible, says this to the client and makes it clear that they’re working on an assumption)
    - PO again: one last question.. we actually started from you wanting to have a profile page and a signup system. What other use cases does it serve? 
    - client: password reset can be in the profile
    - PO: of course (secretly thinks: if there is no signup, there is no password reset => this is a typical scenario when, because of a light decision at the beginning, complexity grows and it seems necessary..), what else?
    - client: nothing, that was the need mostly..
    - PO: maybe to redownload previous contracts?
    - client: yes, also. they can also do that from the email where we have the big download button, but we should put that in the profile also if we can
    - PO: ok thanks, I’ll get back to you
      - PO now has a clear understanding of the business need, he also needs:
        - understanding of the product features (how to exploit)
        - understanding of the implementation complexity of every change idea
        - understanding of the product roadmap
      - PO realizes that, just by adding a “use as template” button to the emails where the contract is sent, next to the “download” button (which the client says it’s working fine btw), you get all the advantages you want for 1/100 of the cost, you don’t add complexity, you don’t disrupt existing customers etc..
      - PO suggests this solution to the client, who loves it and is happy because he saves money and can go on with other features. Buildo is happy because if our customers are happy they keep paying higher than average wages to buildo per day :p

