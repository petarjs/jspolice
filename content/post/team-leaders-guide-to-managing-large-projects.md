+++
date = "2016-09-23T10:05:59+02:00"
title = "Team Leader's Guide To Managing Large Projects"
description = "If you ask any experienced engineer how to build a really big and complex app, they'll tell you - don't. They'll tell you to start small and expand as needed."
image = "team-leaders-guide-to-managing-large-projects.jpg"
type = "post"

tags = [
  "managing",
  "teamleader",
]

categories = [
  "blog",
]

toc = false
+++

If you ask any experienced engineer how to build a really big and complex app, they'll tell you - don't. They'll tell you to start small and expand as needed.

But at some point, you're going to have to build a large app. You'll know from the start that it's a large undertaking, and there won't be any escaping it. You'll start small, but with a good foundation, and build your way up as the circumstances and requirements command.

But you're likely to have problems along the way if it's your first large app. Scaling your code. Making decisions that will impact you in the future, but you don't know what's the best path. You solve them, most likely in a suboptimal way. But then, when you are building your second large app, you use some of the experience gained in your first attempt. And you do it a bit better this time. The spiral continues, until eventually you know your shit. And a junior will come to you asking "How do I build a large app" and you'll just answer "Don't".

Let's take some time to face our fears of large apps. They can be like abstract scary monsters, lurking on the horizon and keeping you from embarking on a journey in that direction.

But they can also be tamed. If you are aware of how large the monster really is, you can begin to tackle it, bit by bit. You have to put some serious effort into getting to know your monster. You can take precautions and make your code flexible because you know that everything is susceptible to change. You need to think about each step as you take it. You can keep checking often to see how much the monster got smaller. It mainly feeds of unknown / not well defined requirements and rash decisions. Don't feed it.

In this article I will present several concrete ways that you can make the best foundation for your large project to succeed. It won't be easy at first, as you won't see much results, but later on, that effort will turn out to be the difference between a project succeeding or failing.

For the last 8 months I've been leading a big project. It consists of 8 front end apps that interact in various ways, fulfilling a complex set of business rules. The apps interact with a unified API, spread across multiple domains. Our team is 12 people strong, half front end people and half back end. This was my first experience leading a project of this scale, and I'll tell you about my mistakes and successes.

## Requirements Gathering

This is arguably the most important phase of the project. And while it's at its most intense in the beginning of the project, the truth is that it lasts pretty much over the course of the whole project. We cannot gather ALL of the requirement prior to development. Nor can the client know exactly what he wants then. As the project progresses, some new ideas and needs will emerge. And that's totally fine.

Unless you're using the waterfall methodology, that is. But you don't have to go full agile and obsess over scrums and sprints to benefit from a client's feedback regularly.

You should aim for weekly or bi-weekly progress review with the client, to show him what you've got and get their input. Daily scrums can be beneficial if kept short - up to 15 mins. Another type of meeting that we found important is what we call "Architecture meeting". This is where teams working on different components of the system can regularly sync up and discuss question and issues regarding integration of those components into the system. Aim for once a week schedule with this one. They can last anywhere from 10 minutes to hour and a half.

## Documenting

You should document the important things. It can seem boring a task, to write documentation when there is code to be written, but I assure you, it will pay off greatly.

First off, anything discussed verbally in a meeting must have a written counterpart. We forget what's said too easily. After a meeting, think about what were some important questions and answers that were discussed. Send a follow up email immediately after the meeting with the written representation of what was agreed upon. This is an easy and amazingly useful way to keep on top of things. But be sure to give the emails descriptive titles, so you can find them easily later on. "Meeting notes 10.10.2016." is bad. "Capacity management for active users" is much better.

But what about the real, boring documentation - the one that agile methodologies so fear?
I advocate that before the project starts, a document describing functional and non-functional requirements must be written. For it to be written, you will have to go deep in requirements gathering and engineering with the client. This will help you understand the project, the business rules, the domain. It will help highlight missing information.

Whenever possible, create flowcharts. I know, I know. Not a very sexy thing to do. But believe me, it's crucial. Create flowcharts that describe the business processes. This will make them easier to understand and will help in communicating both with the client and with the fellow developers. The flowcharts don't need to be formally described by UML or BPMN. It does help, but if used too much can become difficult to understand and follow. Just some rectangles, text and arrows should be enough.

## State Management

As you are probably aware, being a developer and all, data is central to your application. State is the current reflection of your data. Managing state is the most important thing to get right when building a large app. Because it can get messy. And if it gets messy, your project starts handing on a thread.

I've found that the best state management approach is using immutable data structures. The data flows in one way, and you always explicitly know when something's changed. That's opposed to two way data binding, like you'd be tempted to use in Angular.

But, of course, don't think that two way binding should be banished from your whole project. Use it for binding data to the interface and reflecting those changes both ways. But when you need to update the state, do not do it via two way data binding.

## Project Management Tools

Ah, project management tools. They can be most useful, or just add unnecessary bloat to your workflow. But it's more in how you use it with your team than the tool itself matters.

There are a lot of tools out there, free and paid, and there are two different types.

There are tools, like Jira, that are very complicated and structured. I think these kind of tools add more overhead in using them than they give value in a fast paced project.

On the other end of the spectrum, there are almost totally unstructured tools, like Basecamp, Trello, or a To Do list. While these tools are good for certain uses, they cannot withstand the more complex of projects. (well, maybe Basecamp)

But, as it often is, the best ones are in the middle. I found that GitHub issues and Milestones are a great way for keeping track of the project.

## API Documentation

API is the touching point between front end and back end. As such, it is of great importance to document and clearly define all those points of integration. But, just as important is keeping that documentation up to date.

There are some tools that can automatically generate this kind of documentation for you, and keep it in sync with your code. We used Swagger. It works by looking into comments of your API endpoints and models. You do need to write those comments using special Swagger annotations, and often the comment will be longer than the method itself, but it's worth it. So every time you change your method, you need to update the comment to reflect those changes.

In addition to generating documentation that is concise and up to date, Swagger gives you a kind of an API playground where you can try out all those documented requests on your code and database.

This kind of tools are indispensable in communicating information about the API in a concise and structured way, that is always up to date with the code. This project has over 200 API methods. Imagine if front end devs needed to ask the back end devs "What was the type of this parameter of this method?". The backend dev would have to track down the method code to check it, because he doesn't remember either. It would slow everything down and make everyone miserable.

## API Relationships, Filters, Sorting

I have seen this concept in one form or another in several frameworks. Notably in OData and GraphQL, and the concept of HATEOAS. I never used those tools as at the time they all seemed quite alpha. I did see the usefulness of a such system.

The backend team implemented their own version of this concept - to allow clients to specify what data they want to get, how to sort it, to filter it by any field. This was a mean of reducing the number of endpoints required for API, so that the system would be simpler. Right now, there's over 200 api methods. I am afraid to imagine how many there would be had we not used this approach.

To get a clear picture of how helpful this is, let's explore a simple scenario. Say we wanted to get a list of artists for the admin to see. So we follow RESTful api design and create an endpoint GET /artists/index.

But then we realise that we need some related data to show there - artists' info for different job types. So we include that data in the response.

But in another place, we need a list of artists that have the status Pending. So we may add a new endpoint GET artist/index/pending or make it a query parameter like GET artists/index?status=pending, which would be more beneficial since it will allow us to use that same endpoint for filtering other statuses as well.

But then we get into a situation where we need a list of all artists, but without the embedded job type info. Here we need to have their list of jobs embedded. So we might create GET artist/jobs?type={jobType}.

And if we go on and on in this manner, we will end up with hundreds of API endpoints that all do a very similar thing. This will become a nightmare for backend developers. There is no method to adding variations of the same action. Somewhere we need this, somewhere we need that. The more endpoints are created, the more time will be spent in maintaining the existing ones.

The solution? Use one endpoint and allow clients to specify what they need. If we apply this to our examples above, we get:

- Get a list of artists - GET /artist/index
- Get a list of artists with job type info - GET /artist/index?with=['jobType']
- Get a list of pending artists - GET /artist/index?filter[status]=Pending
- Get a list of artists with a list of jobs of specific type - GET /artist/index?with=['jobs']&filter[jobs::type]={jobType}

Now we can access all those variations through a single endpoint by just specifying what we want. How? This was implemented by using PHP Traits. We had a trait for getting related objects (with parameter), filtering (filter parameter), sorting, pagination, etc. Those traits could then be applied to any endpoint with a single line of code. Or be added to a group of related endpoints.

We recognised this need from the beginning, which was awesome. Of course, implementing this took some time up front. But it kept paying for it self literary every day. And of course, as the project progressed, we refined those traits so that they would become more flexible and support a wider range of use cases. 

For example, the filter trait could only be applied to properties of the object we were querying. So if we were doing GET /artist/index, we could only filter artists by their fields. But after some time we realised we needed to filter the objects by data in their related entities, like in the example above - filtering the artists by data in their job lists.

A few more examples - the relationship trait at first could only fetch objects one level deep. But in many cases we needed to go deeper, so it was improved to allow for GET artist/index?with=['jobs', 'jobs.jobType', 'jobs.jobType.stats'].

The filter trait later become able to filter ranges as well as single values, like so: GET /artist/index?filter[created_at]=['2016-02-02', '2016-07-02']

The flexibility of this approach is amazing, especially provided that we could mix all those traits in any single request. Time spent implementing these features - since it's not exactly trivial - was well worth it. It made our day to day work much more pleasurable, since we didn't have to ask Backend team to implement a route for every single variation of data that we needed. We had the ability to get it instantly.

## System Wide Access Control

Permissions, Roles. Applied to API routes and Front End pages and actions. How? Also protecting S3 on backend by controlling who can do what.

Well, security in general is tricky. I hope you find solid ways to implement it. But an aspect of security not often talked about, yet very important, is access control. It's the answer to the question `"Who can do what, and with what data?"`. You will want to restrict access control, even if you don't see how it could possibly be breached. 

A general rule of thumb is - give everyone the least logical amount of permissions. The least logical amount of permissions is - editing your own data, and reading public data. Then, if needed, give more permissions, for roles like admins or whatnot.

Usually you'll have some system for managing this kind of concern, and it will be implemented with concepts of roles and permissions. Roles are groupings of permissions and we allow or forbid access based on permissions (or roles). Users have roles. They could have more than one. A permission can be in more than one role. It all depends on how you decide to organise this into a system.

So, where do you apply these security measures? On both front end and back end, of course!

On back end, you protect API routes, so that only a certain user type access it. We also had an interesting feature - since we used PHP as a proxy to S3, which exposed a kind of a file system interface, we were also able to protect access to files based on rules on roles and permissions. For example, in addition to one user having access to only his data (that's in the database), he also had access to only his files.

On the front end, we also need to protect routes and actions based on roles and permissions. This could be overridden by a savvy user though, so it's natural to have the main measures implemented in backend. On the front end, you'll want to restrict access to certain pages and hide some UI elements based on the user's role.

## Configurable Environments

So you have finished coding a project, and it's time to put it online. But whoa, wait a second! The servers require a slightly different configuration than your local environment. No problem, you might think, I'll just change the code and upload it. But wait! Now when you want to do some more development, you need to change the configuration code again, and remember to put it back before deploying. And what on Earth will you do when a project has multiple environments, like local, dev, staging, production?

What you need to do is separate the configuration from the code. There are a few ways to do that, depending on your programming language. Two common ones are:

1. Store configuration in `.env` files, and have a different `.env` file for each environment. These files don't go into source control because of obvious reasons. The code reads the `.env` file and uses the configuration data from there.
2. Use an environment variable to determine the environment you're in. Here, you export an environment variable, let's say `ENV=staging`, and the code will load an appropriate configuration based on that. Here configuration for multiple environments is stored in one place.

Generally the `.env` file approach is preferred.

## Automated Builds & Deployment

You shouldn't have to do manual builds and deploys, really. Depending on the stack and the project complexity, the deployment can be quite a process. Long and slow, sometimes. You will want to automate this part.

One reason is that it's a tiresome and boring thing to do all the time. But the second, more important reason is that any manual process is prone to human error. So imagine you have to do a deployment to production at the end of a long day, and you forget to set the right environment. Or install the new plugins. Or any small step of the process really, and it all goes to hell. Why risk this situation becoming a reality, when we can automate?

## Task Automation Tools

We can all agree that it's impossible to imagine starting a big JavaScript project without any task automation tools nowadays. For better or for worse, a modern JavaScript workflow has become quite complex (read pain in the ass). You have to combine and consolidate a significant number of tools and technologies in order to give yourself a productive and enjoyable environment. 

Setting up transpilers, CSS preprocessors, live browser reloads, injecting scripts installed via package managers... You wouldn't imagine doing this sorta thing manually, on every save. It'd be madness. So while the whole development workflow may take time and effort to first set up, it's crucial. You can hardly start doing any work without some automation tools in place!

Gulp, Grunt, Brocoli. Use whatever you like, but I'd vote for Gulp. It's much less annoying than Grunt in my experience.

## Code Style Guide

You can't have people in your team writing code in different styles. They might prefer one style or the other, but consistency within a project's code shouldn't be broken because of personal preferences. I feel a big annoyance when I see that one person used spaces and the other tabs.

You can use some dictatory tools to make people confront to style guides. Guys, don't think I'm Hitler for saying this. It's a really important point.

Use a plugin called EditorConfig to make everyone use the same editor settings (spaces, line endings...). Use ESLint to make sure people are writing their JavaScript consistently. If you're in a particularly dictatory mood, you can setup Git pre-commit hooks that won't let code be committed if it doesn't pass those checks.

## Code Reviews

Pull requests, or just looking at your team's code on a regular basis is a great way to ensure everyone is using the style guide and that the code is of desired quality. You can gain valuable insight on how your team mates are doing, and provide feedback to them so that they can further improve. You know, just having a friendly talk, that can end in refactoring - by either you or them.

## Aspects

Aspects in a program are concerns that span over the whole application. They are not features that you can implement in one place, but they are interwoven into the core of your application. It's things like authentication, error handling and API request transformations.

Coming up with a way of implementing these in you language of choice is very important for large projects. Imagine that in the middle of the project, you find out that you have to throttle all the data coming via sockets and the API. You could manually implement it in all needed places, but that would not be very smart or efficient. What you should do is find a way to implement this feature in one place, but in such a way that it can affect all the needed code parts based on configuration.

In the example above, you'd want to create a throttling service and route all socket communication through it. It can then decide if the incoming data needs to be throttled and act accordingly.

## Conclusion

While there are many aspects that can make or brake a project, I believe that the most important one is passion. You can do all the things said above and still fail pretty hard. Nothing beats passion. If there's a team of people who really like what they are doing, who are passionate about solving particular problems in the project's domain, you can bet they'll do a great job. Never mind following all the rules. They are only there to aid and streamline what is already a determined and strong willed team. Focus on invoking passion in your team first and foremost.

How do you do that? Well, that's an exploration meant for another blog post, but I'll just say this - you need to lead by example. Be the most passionate person you've ever met. It may very well be contagious.