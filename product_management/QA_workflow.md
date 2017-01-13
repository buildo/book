# Ensure quality

![](/assets/ensure_quality.png)  
Q.A. in buildo is done in 3 ordered steps:  
1. **developer testing** verify that issue requirements are met, and that no regression has been caused  
2. **PM Q.A.** second verification on issue requirements from the PM perspective  
3. **customer validation** final validation by the customer

Developer testing is explained in the [Pull Requests](../workflow/3.pull-requests.md) chapter.

## PM Q.A.

In this step, the PM moves cards from the "done" column to the "to be reviewed by client" column. While `done` is mandatory and should not change name, client review columns are flexible and should be adapted to the specific product flow.

The function of PM Q.A. is to ensure that requirements have been met, and that nothing was lost in translation.

Even if the development team always implements as required, this step is useful for the PM to verify that requirements were complete and consistent, and to grow their knowledge about the product itself.

It's not responsibility of the PM to find regression bugs or other implementation bugs, and developers should not rely too much on this step.

## Customer validation

In the last step, buildo believes that no bugs exist and all business requirements are met. We only await a final validation from the customer, useful for:

* **contractual reasons** this serves as formal acceptance of the implemented task
* **customer awareness** customers typically request features but often don't check them out for real. It's very beneficial for the product if the customer understands every aspect involved.
* **final requirements verification** at times the implemented feature is not up to expectations, either because buildo failed or because the customer expressed a partial request without knowing. This last step should avoid crippled features to live too long.



