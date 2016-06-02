# Customer requests workflow
![](customer_requests.png)

Every request must be tracked in PRISMA. If possible, customers should be trained to submit new requests directly in the Trello board, tipically in a column called `(r) requests to be discussed`. If not possible, the PM will manually add requests here as they come.

The `(r) ` at the beginning of a column name tells PRISMA to treat that column as a request column. This adds a feature to let you open a GitHub issue directly from the card maintaining traceability.

Typically we have 4 requests columns:

- `(r) icebox` requests that are on hold, buildo does not work on these
- `(r) requests to be discussed` requests that need to be refined and transformed into actionable requests
- `(r) bug reports` bug reports from the customer are just a special kind of request to be discussed, but it's useful to keep them apart
- `(r) actionable requests` requests ready to go to the next step (backlog grooming)

The PM is responsible for transforming all requests into actionable requests, we refer to this process as **requirements gathering**.