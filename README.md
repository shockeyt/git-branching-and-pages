<!--
Market: SF
Adapted for: DEN
-->

![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png)

<!--9:00 5 minutes -->

<!-- So who remembers Git?

What is the difference between Git and Github?

So what we know about Git and GitHub is great if we have only one developer.  But what happens if we bring ten, twenty, thirty developers, working on five different projects onto our team?  What problems might we see?

Some of those problems can be alleviated with branching.

Who has published websites online?

Today we will show an incredibly easy way to get a front-end website online called GitHub pages.  This can save you countless hours of setting up servers, and interfacing with 3rd party tools. -->

# Github Branches and Pages

## Why is this important?
*This workshop is important because:*
- Local and cloud based version control are **fundamental** tools of **every** developer
- Git and Github are the most popular version control solution for open-source projects
- Proficient use of Git and Github allows collaboration on projects from small teams to hundreds or thousands of developers.
- Github Pages allows for simple, quick deployment of front end apps.

## What are the objectives?
*After this lesson, students will be able to:*

- **Fork, clone, and make pull** requests to repositories
- **Create, merge and delete** branches on local and remote repositories
- **Use** git, GitHub and branches to collaborate with other developers
- **Deploy** a project to Github Pages

## Where should we be now?
*Before this lesson, students should already be able to:*

- **Use** the command line
- **Use** a text editor
- **Explain** basic git commands like init, add, commit, push, pull and clone
- **Fork and clone** remote repositories

<!--9:05 15 minutes -->

## Git Branching

Branching: How developers collaborate on projects

#### So what is branching?

Think of making a new branch like spinning up an alternate universe to play with. Each branch exists like a parallel dimension, side by side, for you to hack on.

[![git branching](https://www.atlassian.com/git/images/tutorials/collaborating/using-branches/01.svg)](https://www.atlassian.com/git/tutorials/using-branches/git-branch)

You create a branch anytime you want to work on a new feature, fix a bug, or refactor some code. Any changes you make in a branch stay on that branch, so it won't ruin any other versions you have sitting in other branches.

## Creating a Branch - Demo

By default, as soon as you make your first commit, you are on a `master` branch, and that's where your most production-ready, least experimental code lives.

Any time you're tasked with building a new feature, you make a branch named something obvious, switch to it, write some code, and then eventually merge it into master. Hopefully after someone's double-checked your work.

But let's see what this all looks like from scratch. Just watch and absorb for now, you'll practice it in a minute.

#### The normal git init process

We're working with a new dummy repo just for an example.

```bash
$ mkdir branching-is-awesome
$ cd branching-is-awesome/
$ git init
$ touch readme.md
$ git add readme.md
$ git commit -m 'initializes repository with an empty readme'
```

#### Suddenly, a new feature!

Now, let's say we have a feature we're about to work on. Something simple for now - let's say we want someone to know what this project is all about if they find it on Github, so we should add some info to our readme.

Writing a readme. **That's a new feature, so we should make a new branch.**

```bash
$ git branch writing-our-readme
```

Git created it, but let's double check by listing all our branches:

```bash
$ git branch
  writing-our-readme
* master
```

Nice. The `*` tells us which one we're on (your terminal may or may not color it differently, too), and we see from the list of all our branches we have a new one. Let's switch to it so we can change some stuff without affecting `master`.

```bash
$ git checkout writing-our-readme
Switched to branch 'writing-our-readme'
```

Nice. `git checkout` is a beautiful command – you can use it to check out an old piece of history, another branch, even a specific file or a folder from an old piece of history _on_ another branch.

Now we're working in an alternate universe. We can make whatever changes we need. Let's pretend we filled that sucker up with the best readme you've ever read. Obviously we should save our history with a commit, but we're still on our `writing-our-readme` branch, that hasn't changed.

```
$ git add -A
$ git commit -am 'adds incredible writing to readme'
```

#### Seeing the effects

You can really start to see this idea of parallel universes once you have a commit like this in a branch.

When we switch back and forth, like so:
```bash
$ git checkout master
$ git checkout writing-our-readme
# etc etc
```

We can actually see the changes:

<img width="740" alt="branch-readmes" src="https://cloud.githubusercontent.com/assets/25366/9808262/8bef4ffc-5812-11e5-817a-60571f97deea.png">


- On `master`, `readme.md` has no text in it.
- On `writing-our-readme`, `readme.md` is full of text.

You can literally switch between those branches in your terminal, switch back to your text editor, and see the text appear and disappear. Because in one universe, the text exists, and in another it doesn't.

### Finally, we merge

The very last step of this process is to _merge_ your changes from one branch back into your master. In a few weeks, when you work on your group projects, we'll show you how to use Github to merge changes in a more collaborative, central way.

But before we get to GitHub, or maybe just because we love Terminal, let's look at how to merge your own branches back into your production-ready `master`.

We've gone through the whole process – you're starting a new feature, so you make a new branch, make a bunch of commits on that branch as you work on it, and now you're satisfied it's ready to ship.

You navigate to the branch you want to merge into – most often `master`, but it could be any branch.

```
$ git checkout master
```

And you simply tell it to `merge`:

```
$ git merge writing-our-readme
Updating 5da20b7..62b3656
Fast-forward
 readme.md | 7 +++++++
 1 file changed, 7 insertions(+)
```

This analyzes all the changes you've made on your feature branch, brings them into your `master` branch, and commits them to `master`.

And now that your `master` looks just like your `writing-our-readme` branch, you can delete it.

```
$ git branch -d writing-our-readme
Deleted branch writing-our-readme (was 62b3656).
```

Don't worry – just like most things in git, it's not gone forever. You could always checkout the last piece of history before you deleted the branch, and your branch would be there. Consider that timehopping to the past, but in the present it's gone and you don't need it.

Your most recent code ready to ship is in `master`, and you're a flipping pro.


#### Pushing Branches

Since you're getting to be experts with Github, you should know you can store branches on Github, too, not just your local git repo. While this will totally come into play on your group projects in a different way, it might be useful to you now for the simple purpose of backing up your work.

Maybe you're in the middle of a feature or a bug fix and you're just not done, but it's time for bed. Make your commits, of course, but if you've set up your repo to connect with Github, you can easily push your branch up there.

While you've seen this:

```
$ git push origin master
```

What you should know is that `origin` is simply an alias. We _could_ call it `github` if we wanted, or `zebra` or `fnarf` or `bagel`. It would then be:

```
$ git push zebra master
```

And you've now learned that `master` is just your special, default, production-ready branch. So, assuming you're using the default alias of `origin` (and not `zebra`), guess how you push a branch?

```
$ git push origin my-new-but-unfinished-feature-branch
```

You can `push` and `pull` those branches easily to save your work up in the cloud.

> "Real programmers don't edit `master`." – Dave, the Programmer

<!--9:20 5 minutes -->

## Practice thinking in "branches" - Discussion

Team up with the person next to you, and go through the following commands we've reviewed in class.  

- git branch
- git checkout
- git merge

Based on what we've talked about, and before you jump into your terminal, discuss the correct commands you would have to use - and the correct order you would need to use them in - to repeat the process of creating a readme. Be aware of the "why" and that you may have to use some commands more than once.

<!--9:25 10 minutes -->

## Branch, Push, Merge, Repeat - Independent Practice

Time for you to try it. With your partner, walk through the steps necessary together, catching each other if either makes any missteps.

Start by mimicking our example – create a branch to write another readme.

- `git init`
- `git add` & `git commit`
- Create a new branch for the feature you're about to work on
- Switch to that branch
- Write some code
- `git merge` that branch back into your `master`

Once you've got it down, switch roles, and do the same process again, so you get in the habit of creating branches whenever you need to make changes.

<!--9:35 10 minutes -->

## Create a pull request on GitHub - Catchup

Before you can open a pull request, you must create a branch in your local repository, commit to it, and push the branch to a repository or fork on GitHub.

<!--Do this on the git-branching-and-pages repo on my personal fork -->

1. Visit the repository you pushed to
2. Click the "Compare, review, create a pull request" button in the repository ![pr](https://cloud.githubusercontent.com/assets/40461/8229344/d344aa8e-15ad-11e5-8578-08893bcee335.jpg)

3. You'll land right onto the compare page - you can click Edit at the top to pick a new branch to merge in, using the Head Branch dropdown.
4. Select the target branch your branch should be merged to, using the Base Branch dropdown
5. Review your proposed change
6. Click "Click to create a pull request" for this comparison
7. Enter a title and description for your pull request
8. Click 'Send pull request'

<!--Have all students practice making a pull request for this repo -->

<!--9:45 10 minutes -->

## GitHub pages - Demo

Now that you have had some good practice at branching and merging it's time to deploy using GitHub pages.

We strongly encourage checking out the official [docs](https://pages.github.com/) and practice more at home.

It's _super_ easy and - basically - all that needs to happen is the creation of a new branch called `gh-pages`.  

From our readme project:

```bash
git branch gh-pages
git checkout gh-pages
```

As long as there is an index.html in your root directory of your gh-pages branch...

```bash
echo "<h1> GitHub pages! </h1>" >> index.html
```

...you'll be able to navigate to http://YOURUSERNAME.github.io/REPOSITORYNAME to view the rendered html. You can also point a new domain name to this URL; this would give you a fully deployed project with a custom URL.

<!--9:55 5 minutes -->

## Conclusion

As a developer, you'll have to use Git pretty much everyday, the learning curve is steep and all the principles of version control can  be a bit blurry sometimes, hence why we ask students to push their homework everyday and to commit regularly during project time.

Don't be frustrated by all the new commands because we will definitely have the time to practice during this course.

- Explain the difference between forking and cloning.
- Describe the steps to initialize a Git repository and link your local repository to a GitHub remote location.
- What's a branch in git? When do you use it?
- How do you create a branch?
- How do you switch between branches?
- How do you merge & delete a branch?

## Associated Lab
Refine the skills covered in this workshop with this [lab](https://github.com/den-wdi-2/gh-lab)
