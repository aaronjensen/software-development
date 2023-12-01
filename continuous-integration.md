[← Articles](README.md#articles)

# We Don't Run Tests on a Continuous Integration Server

I and the teams I have been on have used continuous integration (CI) servers to run tests at least since the first version of TeamCity was released in 2006. I, and many others considered this a ["best practice"](./best-practices.md). My current team does not use CI servers to run tests. We have hundreds of software repositories and we only run tests on our local machines.

## Problems That Continuous Integration Is Meant to Address

We do not use CI to run tests or checks because we do not have the problems that CI is meant to address. CI is meant to catch bugs for which there are already automated tests written making their way to production. It is also often used to enforce code styling rules. Let's examine these in reverse order.

### Automated Style Checks

Our Ruby code is not subject to any automated style checks. We do not use RuboCop, so we do not have anything to run. We expect everyone on the team to adhere to team norms as best as they can and to always be looking to improve understandability and scannability of code, which is a skill that goes above that of which an automated tool can enforce.

Our legacy TypeScript code is subject to a handful of eslint rules at the time of writing and prettier is used to enforce consistent styling. These are developer tools and developers are expected to run them on their machine. If a styling problem is pushed to `master` then it is too late — the problem has already occurred, and a CI server would only serve to alert us of the mistake, not fix it. That alert may seem helpful, but is it? What does it serve to prevent? Styling errors will not cause bugs for our users. They will likely be noticed the next time that a developer is in that codebase. We have successfully noticed when newcomers to the team do not use prettier to format their code and have instructed them to do so without need for automated checks. Of note is that our newly authored JavaScript code does not use TypeScript, eslint, or prettier.

If that sounds insane to you, then consider these two things: 1. Our team doesn't need these tools to **thoughtfully** adhere to our standards or be productive. As a matter of fact, we are more productive without them. 2. Our team employs **specific countermeasures for specific circumstances** and we do not currently have the circumstances that necessitate any of those tools. Your team may or may not.

Our team does not benefit from them because we continually invest in our people and their mistake detection capabilities. Our norms are instilled in all our team members, whether junior or senior. We go faster when we do not make the mistakes in the first place. Tooling that catches them is unnecessary if we catch them ourselves while we are attentively doing our work.

### Automated Tests

Next, we have the common practice of CI running automated tests. By running automated tests, CI will flag when a test that should be passing is not passing, thereby alerting the team so that they can repair the code so that the test will pass. This will likely prevent the code from being deployed to staging or or a higher environment. Let's rephrase that as an imperative: "Run the automated tests before deploying to staging" (deploying to staging could be "publishing a package").

Both a human and a CI server are well suited to this task. A CI server does not tend to forget, but why should a human? A human is expected to run the tests before pushing and allowing the CI server to run the tests, which makes the CI server strictly redundant unless we have forgetful humans. So, we try to focus on not being forgetful. We do this by expanding our imperative to: "Validate your work before publishing it". It is not enough to run automated tests. Many of our packages have interactive tests as well. These are just as essential to validating our work, and they cannot be run by CI servers.

In the rare instances where a contributor does not validate their work before publishing it, we address it as a mistake and a lapse of attention. We discuss the incident as a team or with individuals so that we can find and solve the root causes of these types of issues. This leads to not only improvement in the specific thing being addressed, but across the gamut of skills that are required to do our work.

#### Slow Tests

In the past, some on our team have used CI to alleviate the pain of running long test suites on developer machines. Very fast machines with complex parallelization were employed to turn 20 minute test runs to 5 minute test runs. This team focuses on smaller batches of publishing and therefore validation. That is, we have many small repositories that are either software libraries or deployments. The smaller the batch, the easier it is for a person to validate it and the faster the test suite will run. In other words, we solve the cause of slow tests with design and architecture, rather than brute force hardware.

Aside from the test suites that run against slow 3rd-party services, or UI tests, most test suites complete in a matter of single digit seconds. We simply do not have the circumstances that would begin to excuse not running tests locally, so we expect it.

## Cost of Continuous Integration

Most teams set up Continuous Integration without even thinking about it. It is seen as the cost of doing business, but rarely is that cost ever analyzed. There are several costs worth considering.

### Reinforces Wrong Behavior

The [Ironies of Automation paper by Lisanne Bainbridge](https://ckrybus.com/static/papers/Bainbridge_1983_Automatica.pdf) is worth reading. There is a cost to automation that is often unrecognized. The paper points to people losing the ability to take manual control when they have relied on automation. In the case of CI, it has been observed that people are less likely to run their tests locally when they know that they will be run by the server. If people do not have something to catch their mistakes, they are more likely to learn to do the thing that they should be doing with or without the CI server in place. This leads to them not making the mistakes in the first place, which leads to less rework and faster delivery.

### Context Switching and Queueing

When you push work that is validated by CI, there is some period of time before results are communicated back. A person must either wait patiently for the notification and/or monitor the run. More likely than that is that they continue work on something related, further encasing any mistakes that they are waiting for feedback on. Or, they may move on to another task so that if they do get a notification of a problem they must context switch back to the original task to correct the work. The waiting, encasement, and context switching are not free.

### Maintenance Overhead

Even with the advent of yaml based and re-usable CI configuration, this infrastructure must be maintained. It must be paid for both in a monthly service cost and in time spent configuring, tuning, and automating. We have 100s of repositories with tests, all of which would be subject to CI if that were part of our standard practice. That could be a significant amount of work to both set up and keep running over time.

### Encourages Automation for the Sake of Automation

As previously mentioned, our team values interactive tests. When CI is available, a developer will have a natural instinct to want to automate everything. As discussed in the Bainbridge paper, this often makes the system worse, rather than better. Tests that should have been interactive because they are best run with eyes-on will be automated and much of their value will be squandered. Tests that cannot be automated will be discarded or never written in the first place. In short, automation becomes the goal and anything less than that is seen as inferior and unnecessary.

## Notes

- Our team does use a CI server for deployment. This is a technical necessity and we would stop doing it if we could.
- We started without CI servers for tests, so our team culture grew around that. If a team were to shut off their CI server that they had relied on for years, there would likely be a lot of challenges, regressions, and necessary learning. I believe that if a team went through this process they would get better, but every team is going to vary in its ability to do this and the time it would take to accomplish it.

---

[Comments](https://github.com/aaronjensen/software-development/discussions/3)

[Subscribe to be notified of new articles](https://github.com/aaronjensen/software-development/discussions/8)

[All Articles](https://github.com/aaronjensen/software-development/blob/master/README.md#articles)

---

Copyright Aaron Jensen 2023-present
