+++
date = "2016-07-08T01:24:58+02:00"
title = "13 Secrets to Coding Awesome JS Plugins NOT Like a Jerk"
description = "Oftentimes, we programmers are lazy. Nothing wrong with that."
image = "introduction.jpg"
type = "post"

tags = [
  "thinking",
  "development",
]

categories = [
  "News",
]

toc = false
+++

Oftentimes, we programmers are lazy. Nothing wrong with that. But, also oftentimes, we get a desire to contribute our ideas and skills to the community. Usually as creating a open source library that will help people in some way. Then, our laziness meets our enthusiasm to contribute, and well... weird things can happen.

Sometimes, you'll start to write a plugin, but lose enthusiasm and not finish it. No problem with this, since it doesn't get open sourced at all. I mean, it'd be great if you finished that library you started 2 years ago and never got around to comlpeting it. But hey, we're all humans here, we get lazy.

And sometimes, you'll finish your plugin, you'll make it work. But you'll get lazy in the last step, which is - make it polished. Write the documentation, refactor the messy code. Create scripts for minifying your code.

### Well, no more, I say. No more!

Let's explore 13 steps to make your open source plugin tidy and slick, and how to keep it in a good shape.

## But why bother?

You're wondering why should you put all this effort into an Open Source library.


Your repository might not get any contributors aside from yourself. That's not the point. If you make the code public, it's your responsibility to make it as lean as possible. 

You can think of your Open Source project as your dog. When you walk your dog outside, you need to clean after it. I mean, you can get away by not doing it, but then you are a jerk.

And the more open source projects you have, the more dogs you have. So that can amount to a lot of cleaning up!

I admit, I myself didn't follow these guidelines for a long time. Now, I'm trying to stick to them as much as possible.

The ultimate goal here is to define guidelines that every Open Source project can follow. Imagine if all the open source projects used the same structure and guidelines. It would be much easier to both use those libraries and to contribute to them.

I know how eager you are to publish your library as soon as possible. Following these rules might seem like they will put off the release. But here's the secret - you don't have to do all these steps before you publish you lib. You can keep improving it after publishing.

If you want to hear that this will benefit you directly in some way, it will. You will get good reputation, people will respect you. And while it may not be an immediate benefit, over time it will pay itself off. Employers looking into you will discover that you have a high standard for code you write. Probably you'll be able to negotiate a higher salary. And besides, all this can teach you some new things and help you do a better job.

You should apply this advice to small and big projects alike. No project is too small to be well groomed, especially if it solves a problem and / or people use it.

# First part - While in development

While you're developing the plugin, here are a few things you can do to make your efforts systematic and make it easier for yourself later on. Gotta think about future!

## 1. Write awesome commit messages

There are a lot of people who are just careless about the commit messages they write. Don't be one of those people. Especially when you're creating a public library that others will use and contribute to.

There are some good tips on how to write commit messages over the Internet. But some of them go above and beyond of what you'd expect for a commit message. I think those are only applicable in big code bases that will to be maintained for years to come. Here's an example of one recommendation:
>Summarize changes in around 50 characters or less

>More detailed explanatory text, if necessary. Wrap it to about 72
>characters or so. In some contexts, the first line is treated as the
>subject of the commit and the rest of the text as the body. The
>blank line separating the summary from the body is critical (unless
>you omit the body entirely); various tools like `log`, `shortlog`
>and `rebase` can get confused if you run the two together.

>Explain the problem that this commit is solving. Focus on why you
>are making this change as opposed to how (the code explains that).
>Are there side effects or other unintuitive consequences of this
>change? Here's the place to explain them.

>Further paragraphs come after blank lines.

> - Bullet points are okay, too

> - Typically a hyphen or asterisk is used for the bullet, preceded
>   by a single space, with blank lines in between, but conventions
>   vary here

>If you use an issue tracker, put references to them at the bottom,
>like this:

>Resolves: #123
>See also: #456, #789

Commit messages structured this way can be most useful in big Open Source projects with a whole lot of contributors. Check out the [angular repo](https://github.com/angular/angular.js) which has almost 8k commits, 1.5k contributors, 8k issues and 15 branches. Who can even begin to grasp how it all works, seriously! But look at their commit messages, which are nice:

>fix(modules): allow modules to be loaded in any order when using `angular-loader`

>Some modules used to assume that the angular helpers would always be available when their script was executed. This could be a problem when using `angular-loader` and the module file happened to get loaded before the core `angular.js` file.
>This commit fixes the issue by delaying the access to angular helpers, until they are guaranteed to be available.

>Affected modules:
- `ngAnimate`
- `ngMessageFormat`
- `ngMessages`
- `ngRoute`
- `ngSanitize`

>Fixes #9140

>Closes #14794

They almost completely follow the advice above, and I imagine it helps them quite a bit. But, for your everyday, small javascript plugin, you don't need to be this diligent. It's an overkill. So lets explore how we can use some of the the advice above and still be kind of casual about the whole thing. You know, you don't want to be that guy who comes to the office in a suit and starts coding.

Here is a format of a relaxed, but still good commit message that's find for most projects. Example is from [Pikaday](https://github.com/dbushell/Pikaday), a nice date picker JS plugin.
>Show days in next and previous months

What, that's it?! Yep. Just enough for most use cases, I'd say. If you want to refer to an issue, do it like this:

>[#410] fixing invalid selector for next and prev buttons

Now, we covered the format of the commit message, but what should you actually say there? Some points that always hold true:

- Start the sentence with a verb, like "fix something" or "change parsing of strings"
- If you add an issue number before the message, make sure to wrap it in [] as in the example above. Vim (and maybe some other editors, I don't know) won't recognise # as a symbol on the beginning of the first line.
- Make it as meaningful as you can, without blabbering too much
- Make it meaningful, as opposed to writing messages like this generator does: [http://whatthecommit.com/](http://whatthecommit.com/). **"Something fixed"** and **"It's Working!"** are lousy commit messages.
- Don't try to be funny. People looking at commit messages need **information**, not fun.
- Group commits in small atomic pieces of work. Don't do one commit at the end of the day with everything in it. Following this will also make it easier to write better commit messages, because you actually do know what you did in that commit.

## 2. Use linters for standards compliant code

Don't you just hate it when everyone on your project is using single quotes, and then there's this guy that just won't give up his double quotes? It's just bad manners, I tell you, seeing code that has mixed single and double quotes. Or tabs and spaces. Or naming of variables.

All these things, even if they seem shallow and only aesthetic in nature, they are much more. They increase mental friction. They hinder productivity. Linters often also track constructs that may be harmful and cause bugs. Like redeclaring variables in JavaScript. Sure, it's won't throw an error (unless in strict mode), but it probably is an error.

Having consistent code in a project where many people are contributing is important. It shows professionalism and discipline. It enables new team members to quickly get up to speed. And it removes some of the cognitive dissonance that arises when there are many people working on the same thing.

This is especially important in Open Source projects where people you've likely never met are working on your code.

There are a lot of linters out there. They can and should be integrated into text editors and workflows. Check out jshint, jslint and eslint for JavaScript. There are scsslint and csslint for CSS too.

You can even go a step further and setup Git pre-commit hooks. That way, anyone who commits must respect the code style and consistency.

## 3. Have a good branching strategy.

Use a branching strategy. Have separate branches for development and releases. Have feature branches. I recommend you use `git flow`.

Here is a classic article on the topic, [http://nvie.com/posts/a-successful-git-branching-model/](http://nvie.com/posts/a-successful-git-branching-model/).

Using branches will help you in not being a jerk. New features that you develop won't break the master branch on which people depend. Only when you're sure that new feature is working you can merge it into master and roll out to your users.

## 4. Releases

Take care of your releases. It's easy to make a release - just `git tag v.1.0.0` and `git push --tags` and it's out there.

It's important you pick a naming convention for you releases and stick to it. You'll want to use [semantic versioning](http://semver.org/)

You should have a log of changes that go into each release. You can create a `CHANGELOG.md` in the root of your project. See React's [changelog](https://github.com/facebook/react/blob/master/CHANGELOG.md) to get the idea.

But, you'll want to describe not only what has changed, but also what impact will that change have. In each release, you should group the changes by **Breaking**, **Bug Fixes** and **Features**. For an example of this, check out Angular's [changelog](https://github.com/angular/angular/blob/master/CHANGELOG.md)

## 5. Play well with other libraries

Provide a `noConflict` method. Even if you think that it's unlikely that someone is using your library's name, or that another library has the same name, be a good guy and do this.

Here is what jQuery has to say on this topic:
> Many JavaScript libraries use $ as a function or variable name, just as jQuery does. In jQuery's case, $ is just an alias for jQuery, so all functionality is available without using $. If we need to use another JavaScript library alongside jQuery, we can return control of $ back to the other library with a call to $.noConflict()

Write your code as a closed module via IFEEs, so that your stuff doesn't leak out into the global scope. Export your library as an AMD and Require module. You can see an example of this in [Anime's source](https://github.com/juliangarnier/anime/blob/master/anime.js).

This modularisation is really important, and if you don't employ it, then you're a jerk. 

## 6. Use build tools

Provide scripts for common tasks like concatenating and minifying your code, or css preprocessor compilation, linting, testing... These will be useful to developers trying to contribute to your code. If you do use some kind of task automation, be sure to include clear documentation on how people can use it.

There are a lot of task automation tools out there. Get some time to try out a couple, see which one you like. Popular ones are Gulp, Grunt and [npm scripts](https://css-tricks.com/why-npm-scripts/)

## 7. Tests

Tests are just common sense for Open Source libraries now days. It is a way to prove to everyone that your code works. Also, to make sure that new releases don't break existing functionality. You position your library as stable if you have good tests. People can use it without being wary or afraid that something will break.

Tests are not only for big Open Source projects either. All projects should have them. Take a look at this small jQuery plugin, [jQuery.fullscreen](https://github.com/private-face/jquery.fullscreen). It doesn't have a lot of code, yet it's tested.

We have established that all projects should have tests. But what kind of tests? There are 3 kinds:
- Unit tests
- Integration tests
- E2E tests

Although it'd be nice to have all these tests and cover 100% of the code paths with each one, it's not practical.

Aim for covering what your library does, given different inputs and different options. Cover the ways of interacting with your library. Focus on unit tests. But also provide some E2E tests, so that people can see how your library interacts with it's surroundings.

Make sure you put effort in writing clear and meaningful tests. They will also serve as a kind of documentation.

### Bonus:

- Don't forget `.gitignore`

# Second Part - After development

## 8. Squash your commits

When you're developing a feature, you will have some commits that don't quite make sense. Like `add @mentions to list items` and then `fix @mentions to be case insensitive`. And then `fix again @mentions - typo`. The second commit was caused by you not testing the feature enough. The third was a typo, it happens. Those two commits are not necessary. They don't bring any value to someone looking at your commits. So what you can do is squash those three commits into one nice, full featured commit.
 
Here is a nice read on the topic:
[https://ariejan.net/2011/07/05/git-squash-your-latests-commits-into-one/](https://ariejan.net/2011/07/05/git-squash-your-latests-commits-into-one/)

Why is this important? It is confusing if many of your commits are unnecessary. Squashing keeps your git history nice and clean.

## 9. Good documentation

Good documentation is the most important thing you can put your effort into. If you do just one thing from this list, let it be this.

What can you do when you come across repos like [this](https://github.com/hamaxx/lml) and [this](https://github.com/PAntoine/look)? Pull your hair out in rage and disappointment? You have no idea what it is, what it does, how it does it, or how to use it.

There are two types of docs.

- Code comments
- Written documentation

Sometimes written documentation is generated from the code comments, but I wouldn't advise it. Sure, you write it in just one place, so it's easy to keep both up to date. This may be appropriate for huge projects. But I think you'd benefit more from custom tailored documentation and code comments.

**Code comments** - I like when I see JSDoc style comments in code [http://usejsdoc.org/about-getting-started.html](http://usejsdoc.org/about-getting-started.html). Apply them to all functions. Imagine you're someone wanting to contribute to the code - what would you find helpful to know about this function to be able to contribute? That's your comment.

**Written documentation** - This should be a guide describing how to use your library. In my opinion, a solid documentation of a repo should include the following, in that order:

0. GitHub has this thing on top of the page where you can enter a short description and a website. Use it.
1. Title (which is linked to a website if there is one)
2. Short description - what it is, what it does, what problem does it solve?
3. Demo - link to a demo
4. Browser Support - if applicable
5. Dependencies - if there are other libs that your library depends on to work, list them here. Like, if you're creating a jQuery plugin, list jQuery here. If there are no dependencies, write that. It's important to know.
6. Quick Start / Install - instructions to install it via npm, bower or directly
7. Examples - include a few short code examples on how to use the library
8. Configuration - list the options that can be used to configure your library. Describe what each option does.
9. API - list the options and functions that can be used to interact with your library. Describe each of them, and provide a short code example on how to use it.
10. How it works (optional) - an overview of how your library does what it does. Did you make some interesting architecture decisions? Did you solve a problem in an interesting way? Did you use some ugly hacks? You might want to mention these things.
11. Drawbacks / Known issues - list negative things about your library that anyone using it should know about beforehand.
12. Contributing - Describe the guidelines for contributing to your project.
13. Licence - Which licence does the library have?

Check out the docs for this nice library [https://github.com/juliangarnier/anime](https://github.com/juliangarnier/anime). It does most of the these things right.

You can use a generator to create a documentation website from your readme, like this one does: [http://couscous.io/](http://couscous.io/). Note that this is different from generating documentation from your code comments. Here you already have written documentation, in markdown, and you want to generate a nice looking website from it.

## 10. Bower and NPM support

Publish your library on Bower and NPM. That means you need to find a name for your lib that's available on both. Keep in mind that when you register a name for your library, you are preventing anyone else from using it in the future. So make sure that you are really going to maintain that library of yours.

Provide descriptive and valid package.json and bower.json. Keep them in sync. When you make a new release, change it there too.

## 11. Demo on GitHub pages (or elsewhere)

There is nothing better than a demo to showcase what your library does. That doesn't mean that you don't need documentation though. The two compliment each other. What makes a good demo? Look at these three examples:

- Bad Example - [http://code.nath.co/mousetip](http://code.nath.co/mousetip)
- Good Example - [http://zurb.com/playground/tribute](http://zurb.com/playground/tribute)
- The Overkill - [http://ng-table.com/#/](http://ng-table.com/#/)

The bad example is a page that shows plugin's functionality. But it doesn't provide any context. 
The good example does provide context. Just by landing on that page you can say what is it and how it works. There are also some code examples. 
The last example would be an overkill for most libraries. Ng-Table has implemented and written guides on A LOT of use cases and different options. And I most certainly understand the need for that, as the library is complex to set up and use correctly. 

For your library, you most probably won't need to be this detailed as far as the demo is concerned. It's nice to see a few examples showcasing different options, but make it simple and meaningful. Unless you're creating some kind of a behemoth library that is complicated to understand. In that case, you'll need something like Ng-Table's demo page.

## 12. Up to date packages

Every so often, I come across a library that I install via bower or npm, and it gets it's dependencies. But it is depending on versions of packages from like a year ago. Since then a completely new version might have come out. A library can be deprecated in that time.

Or maybe you wrote a plugin for another library, like jQuery or Angular. When a new version of that library comes out, you need to update your library to keep up. Of course, you can have different releases that support different versions of the library. The point is - keep it up to date!

## 13. Don't abandon it!

Don't create something for people to use and then abandon and ignore it. Put some effort into maintaining it. Update the package versions. Answer to Issues. Promote it. Ask people how to make it better. Add a feature or two. It doesn't require too much time, and the benefits are great, both for yourself and others.

### Bonus
Include these additional files in your repo:
- Licence
- Contributing guidelines
- Change log (breaking changes, improvements, new features) - see [http://keepachangelog.com/](http://keepachangelog.com/)
- AUTHORS file

## Conclusion

Now, I won't be too harsh on you. If you are practicing at least 7 out of these 13, we can all agree that you're not a jerk. You're a pretty cool Open Source guy or gal.

At the end of the day, remember to feel good about yourself for making your Open Source projects nice and tidy. It really does make the world a better place!

