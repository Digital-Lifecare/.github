Introduction

Digital Lifecare really encourages anyone to contribute and to make our system better. We ask contributors, however, to read this guide carefully and follow the established guidelines. We don't claim this is perfect, so these guidelines will change over time as we feel that it is not complete or appropriate. Suggestions on how to improve this guide for contributors are also welcome.

Issues and Pull requests

To produce a pull request against Digital Lifecare, follow these steps:

- Create an issue: Create an issue and describe what you are trying to solve. It doesn't matter whether it is a new feature, a bug fix, or an improvement. All pull requests need to be associated to an issue.
- Issue branch: Create a new branch on your fork of the repository. Typically, you need to branch off master, but there could be exceptions. To branch off master, use

_git checkout master_

_git checkout -b \<new-branch-name\>_

- Push the changes: To be able to create a pull request, push the changes to origin:

_git push --set-upstream origin \<new-branch-name\>_

Assuming that origin is your personal repo.

- Branch name: Use the following pattern to create your new branch name: issue-number-description, e.g., issue-1023-reformat-testutils.
- Create a pull request: Github gives you the option of creating a pull request. Give it a title following this format _Issue ###: Description_,

e.g., Issue 1023: Reformat testutils.

If your PR covers more than one issue, use the format Issues 123, 456: Description.

Follow the guidelines in the description and try to provide as much information as possible to help the reviewer understand what is being addressed. It is important that you try to do a good job with the description to make the job of the code reviewer easier. A good description not only reduces review time, but also reduces the probability of a misunderstanding with the pull request.

- Merging: In three steps:

1. Checks: Make sure that all relevant checks have passed, see the previous section. If they didn't pass, then don't be lazy, help the contributor understand what has gone wrong.
2. Merge title: Make sure the merge title is the same as the pull request one. Typically, the Github UI will give you the pull request title as the merge title, but in the one case when the pull request has a single commit, the Github UI will replace the merge title with the title of the first commit. In this latter case, you will need to copy and paste to fix it.
3. Merge text body: This is the box right under the title. It is typically populated with a list, where each bullet corresponds to a commit title. We remove that list and replace with the change log description in the pull request description above at the top of the pull request conversation tab. Sometimes the description has typos, it is not well explained, or simply too long. It is at the discretion of the committer whether to change that text or not. If you change it, then make sure you know what you are doing. Make sure to keep exactly one signed-off-by line to indicate that the developer complied with the DCO requirement.

Another important point to consider is how to keep up with changes against the base the branch (the one your pull request is comparing against). Let's assume that the base branch is master. To make sure that your changes reflect the recent commits, we recommend that you rebase frequently.

The rebase might introduce conflicts, so you better do it frequently to avoid outrageous sessions of conflict resolving.

Creating an issue

When creating an issue, there are two important parts: title and description. The title should be succinct but give a good idea of what the issue is about. Try to add all important keywords to make it clear to the reader. For example, if the issue is about changing the log level of some messages in the segment store, then instead of saying "Log level" say "Change log level in the segment store". The suggested way includes the goal where in the code we are supposed to do it.

For the description, there are three parts:

- Problem description: Describe what it is that we need to change. If it is a bug, describe the observed symptoms. If it is a new feature, describe it is supposed to be with as much detail as possible.
- Problem location: This part refers to where in the code we are supposed to make changes. For example, if it is bug in the client, then in this part say at least "Client". If you know more about it, then please add it.
- Suggestion for an improvement: This section is designed to let you give a suggestion for how to fix the bug described in the Problem description or how to implement the feature described in that same section. Please make an effort to separate between problem statement (Problem Description section) and solution (Suggestion for an improvement).

We next discuss how to create a pull request.

Creating a pull request

When creating a pull request, there are also two important parts: title and description. The title can be the same as the one of the issue, but it must be prefixed with the issue number, e.g.

Issue 724: Change log level in the segment store

NOTE: Github has this trap that if the PR has a single commit, then at merge time, it will populate the commit title with the title of the commit and not with the title of the PR. It happens often that contributors put generic messages, like "fix" or "comments", and committers don't pay close enough attention and that becomes part of the commit log forever.

It is good practice to avoid such mistakes to make the message of the first commit being the same as the title of the PR. Committers should still always revise title and message according to the committer guidelines, but the contributor can clearly help to reduce the number of occurrences of such mistakes.

The description has four parts:

- Changelog description\*: This section should be the two or three main points about this PR. A detailed description should be left for the What the code does section. The two or three points here should be used by a committer for the merge log.
- Purpose of the change: Say whether this closes an issue or perhaps is a subtask of an issue. This section should link the PR to at least one issue.
- What the code does: Use this section to freely describe the changes in this PR. Make sure to give as much detail as possible to help a reviewer to do a better job understanding your changes.
- How to verify it: For most of the PRs, the answer here will be trivial: the build must pass, system tests must pass, visual inspection, etc. This section becomes more important when the way to reproduce the issue the PR is resolving is non-trivial, like running some specific command or workload generator.

Signing your commits

We require that developers sign off their commits to certify that they have permission to contribute the code in a pull request. This way of certifying is commonly known as the Developer Certificate of Origin (DCO). We encourage all contributors to read the DCO text before signing a commit and making contributions.

Signing off a commit: Using the git command line

Use either _–signoff_ or _-s_ with the commit command. See this document for an example.

Make sure you have your username and e-mail set. The _--signoff_ | _-s_ option will use the configured username and e-mail, so it is important to configure it before the first time you commit.

I have forgot to sign-off a commit in my pull request: There are a few ways to fix this, one such a way is to squash commits into one that is signed off. Use a command like:

git rebase --signoff -i \<after-this-commit\>

where \<after-this-commit\> corresponds to the last commit you want to maintain as is and follow the instructions here.

Test cases

In addition to the required code coverage, all pull requests should include at least one test case. If it is a bug fix, then the test case should reproduce the issue it is fixing. If it is a new feature, then the test case(s) should cover all the new code and changes. Reviewers are expected to enforce this and request test cases from the contributor accordingly.

In some instances, providing a test case is really hard if not impossible, so it is acceptable for some pull requests to not have a test case, e.g., for some nasty race condition that is really hard to reproduce. In some cases, when doing the test is difficult but doable, we expect the contributor to go that extra mile and possibly build some classes that help with future test cases.
