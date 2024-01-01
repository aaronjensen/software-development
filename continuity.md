[← Articles](README.md#articles)

# The Goal: Continuity

If you've ever had the experience of working on a brand new, greenfield project you'll know what it feels like to have a test suite that runs in milliseconds, to have deploy times in the 30-120 second range, to have pull requests reviewed in minutes, and to generally *feel* productive. If you've worked in a greenfield server-rendered application using something like Rails, you'll likely have experienced an even greater feeling of productivity as you haven't been required to set up React Components, a server API, client API objects, and types just to render a list of widgets.

If you haven't experienced these things, you likely don't know what this feels like and you may think it's perfectly normal for it to take 10-15 minutes (when run on 10s or 100s of CI agents) to get feedback on whether or not tests still pass with your change, or for pull request feedback to take on the order of days or weeks, thus necessitating things like "stacked pull requests". You may also think it's normal to have hundreds, or even thousands of developers, most of whom are dedicated to things that do not add user value, and everything that does add user value being slowed down significantly by ["technical debt"](./technical-debt-vs-incomplete-work.md) or areas of the code that are too hard to change without causing significant production issues, etc. You may think it's normal for your CSS style guide to have 40 shades of blue, 75 shades of gray, and 23 button styles. You may even think it's normal to not be able to run your application on your local laptop and instead have to run it on a specially provisioned set of VMs or containers.

If you've ever experienced the greenfield scenario I've described, you've likely also experienced a transition towards (but perhaps not all the way to, depending on how long you worked on the project) the second scenario I've described. You've seen tests take longer and longer until you've needed to parallelize your build across multiple CI agents. You've seen the impact of adding more developers to the team decrease over time. You may have even seen your team's ability to add new functionality, especially complex functionality, decrease precipitously.

If only the description of greenfield projects resonates with you, then I would posit that one of two things is true: 1) You've never been on a project for more than a year or two, or, 2) You're on a very special project that has managed to stem the tide of what most think is inevitable in software projects.

Our goal, with all of the practices that we have put in place, and that I attempt to describe in my articles here, is to stem that tide. It is to maintain our productivity at a consistent level per developer through the life of the project. We call this "continuity", which is a term that Scott Bellware introduced to our team along with many of the techniques we employ to maintain it.

Software projects that are actively being worked on are either getting worse on this metric or better. No project can really stand still. It takes constant effort to prevent things from getting worse, which is why our most senior team members dedicate much of their time to maintaining continuity. We do this through design; coaching; establishment of norms, standards, and policies; tooling; etc. It's essentially a full time job, but the benefits are observable by every member of the team.

---

[Comments](https://github.com/aaronjensen/software-development/discussions/11)

[Subscribe to be notified of new articles](https://github.com/aaronjensen/software-development/discussions/8)

[All Articles](https://github.com/aaronjensen/software-development/blob/master/README.md#articles)

---

Copyright Aaron Jensen 2023-present
