# Develop, and manage internal issues

![](/assets/develop_and_manage_internal_issues.png)

The full development workflow is under [Development workflow](../workflow/README.md).

Here we only discuss how issues enter and exit the development workflow, plus how to manage **internal issues** in GitHub.

## From backlog to done

### Choose an issue

Everything starts from an open issue associated to a backlog card. Open issues should be only those issues that are "in development". Things that will be developed in the future should stay in Trello, not GitHub.

If you work with sprints \(milestones\), the open issues should mostly be the current sprint.

To help visualize the current sprint \(milestone\), you can use the [milestone overview tool](https://github.com/buildo/core/issues/201). It's a WIP, still under evaluation :\)

### Implement, test and deploy

This is the development flow. Only two things must be highlighed from a PM perspective:

* **testing** is tracked and ensured via test plans: **the first and most important Q.A. step is on developers**.
  * make sure the test plan template is good for your project, and customize it if necessary!
* **deploy** on the test environment is essential for PMs and customers to test: it's mandatory and should be automated.

## Manage internal issues

Internal issues are issues that developers open directly in github, without starting from a request or bug report in PRISMA. They are marked with the label \`internal\`.

To evaluate if an issue should be internal, the DEV should follow this guideline:

* it's a **small** **defects or DX improvement**
* it's outside the scope of a macro issue \(aka it can't be a sub-issue\)
* it's **not directly relevant to the PM**
* typically, the DEV will** fix it right away**

The PM will still see all the "internal issues" in Trello under the "github PM buffer" column. For each new internal issue, a card will appear there. The PM should:

1. if the issue is truly internal =&gt; archive the card
2. if the issue should have started as a request or bug report =&gt; move the card to the right column, and remove the \`internal\` label in GitHub



