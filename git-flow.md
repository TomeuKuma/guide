# Git workflow

![Image](images/git-flow-app.png?raw=true)

# How to add more code to the project

## 1. Create feature branch / hot fix branch
On your fork, create a new branch from the latest upstream master branch
commit of the repository you need to work on.

We do not enforce any particular branch naming policy, but we recommend using prefixes, like `fix`, `feature` or `improvement`, for example.

### Resources

#### Accessing GitHub
- [Generating a new ssh key](https://docs.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
- [Adding a new ssh key to your github account](https://docs.github.com/en/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account)
- [How to avoid 2FA errors using tokens](https://medium.com/@ginnyfahs/github-error-authentication-failed-from-command-line-3a545bfd0ca8)

#### Learning Git
- [Git Handbook](https://guides.github.com/introduction/git-handbook/): Quick introduction to Git.
- [GitHub Git cheat sheet](https://education.github.com/git-cheat-sheet-education.pdf): 
  Contains examples of the most commonly used commands.
- [Git presentation](http://vmarkovtsev.github.io/mipt_web_2015/02_git/index.html): 
  Introductory tutorial illustrating the importance of using Git in a collaborative environment. Incorporates a summary of the essential commands, and helpful links to Git bibliography and interactive courses.
- [Pro Git book](https://git-scm.com/book/en/v2): Contains everything there is to know about Git.

#### Interactive Git labs
Online courses and step-by-step demonstrations explaining the most popular Git commands and collaborative processes: 

- [Fundamentals of Git](https://gitimmersion.com/lab_01.html)
- [Git Branching](https://learngitbranching.js.org/)
- [Resources to learn Git](https://try.github.io/)
- [Staging, cloning, branching, and collaborating with Git](https://www.pluralsight.com/courses/code-school-git-real)

## 2. Development and Pull Requests
Work on your local repository as you see fit. When the time comes to make the PR, rearrange your 
commits to improve its readability: squash similar changes into individual commits and try 
to keep the overall commit count at a minimum.

### Resources
- [About pull requests](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/about-pull-requests)
- [Creating a pull request](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/creating-a-pull-request)
- [Commenting on a pull request](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/commenting-on-a-pull-request)

## 3. Code review and requested changes

- The project maintainer or a designated reviewer will review PRs.

After a code review, add the requested changes in a new commit. This is useful
because it’s possible to check again only the specific changes that the reviewer
requested. When your PR is approved, rearrange all the commits to have a descriptive history of your changes. Also, rebase your pull request with master branch.

### Resources
* [Intro to code reviews](https://www.evoketechnologies.com/blog/simple-effective-code-review-tips/)
* [Checklist for code review](https://www.evoketechnologies.com/blog/code-review-checklist-perform-effective-code-reviews/)
* [Another checklist with useful principles](https://dev.to/codemouse92/10-principles-of-a-good-code-review-2eg)
* [Tips for being nice during a code review](https://developers.redhat.com/blog/2019/07/08/10-tips-for-reviewing-code-you-dont-like/)

#### Referencing pull requests and issues in GitHub 

* Use `Cross Links` to [reference](https://docs.github.com/en/github/writing-on-github/autolinked-references-and-urls#issues-and-pull-requests) and connect different conversations within a repository. When commenting, type `#` to bring up a list of suggested __issues__ and __pull reqests__, and select the issue or pull request number to reference it. These references are automaically converted to shortened links to the issue or pull request. 
* If you are opening a pull request that fixes the question proposed in an issue, add `closes #[issue number]` in the pull request message. This will close automatically the issue when the reviewer approves and merge the pull request.

### 3.1 Avoiding cascading delays when submitting PRs that depend on one another
If you want to submit several PRs that depend on one another, and you don’t want to wait for the revisions of the former to submit the latter, you can, as an exceptional measure, submit them without 
waiting to rebase them against master, so each of them will depend on the changes of the previous ones.

Always add a comment to the Pull Request showing that it depends on other PRs
that must be merged first.

To merge this kind of Pull Request you need to know how to use the
`rebase -i` git command:

- (Maintainers only) Merge into master the first PR in the dependency chain.
- Because this PR is merged using squash, you need to rewrite your PR commit
history removing old commits from the previous PR and adding the squashed one from
master. Using `rebase -i` command is a simple task.
  
### Resources

* [Interactive rebase with Gitkraken](https://support.gitkraken.com/working-with-repositories/interactive-rebase/)
* [Rewriting git history](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)


**This document is based on the [source{d} engineering guide](https://github.com/src-d/guide/blob/master/engineering/git-flow.md).**
