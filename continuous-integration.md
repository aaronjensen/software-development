[← Home](README.md)

# We Don't Run Tests on a Continuous Integration Server

I and the teams I have been on have used continuous integration (CI) servers to
run tests at least since the first version of TeamCity was released in 2006. I,
and many others considered this a ["best practice"](./best-practices.md). My
current team does not use CI servers to run tests. We have hundreds of software
repositories and we only run tests on our local machines.

This is a slightly adapted version of an article that I originally wrote for
newcomers on my current team.

## Problems That Continuous Integration Is Meant to Address

We do not use CI to run tests or checks because we do not have the problems that
CI is meant to address. CI is meant to catch bugs for which there are already
automated tests written making their way to production. It is also often used to
enforce code styling rules.

### Automated Style Checks

Let's look at those in reverse order. Our Ruby code is not subject to any
automated style checks. We do not use RuboCop, so we do not have anything to
run. We expect everyone on the team to adhere to team norms as best as they can
and to always be looking to improve understandability and scannability of code,
which is a skill that goes above that of which an automated tool can enforce.

Our legacy TypeScript code is subject to a handful of eslint rules at the time
of writing and prettier is used to enforce consistent styling. These are
developer tools and developers are expected to run them on their machine. If a
styling problem is pushed to `master` then it is too late — the problem has
already occurred, and a CI server would only serve to alert us of the problem,
not fix it. That alert may seem helpful, but is it? What does it serve to
prevent? Styling errors will not cause bugs for our users. They will likely be
noticed the next time that a developer is in that codebase. We have successfully
noticed when newcomers to the team do not use prettier to format their code and
have instructed them to do so without need for automated checks. Of note is that
our newly authored JavaScript code does not use TypeScript, eslint, or prettier.

The checks for styling do not prevent bugs, and they do not provide any
additional notification to problems that we do not already have by working as a
team and paying attention to what we are working on. They could likely provide
more timely feedback, but we must evaluate whether or not that more timely
feedback provides more value than the cost of maintaining CI infrastructure and
training ourselves to spot mistakes at a glance.

### Automated Tests

Next, we have the common practice of CI running automated tests. By running
automated tests, CI will flag when a test that should be passing is not passing,
thereby alerting the team so that they can repair the code so that the test will
pass. This will likely prevent the code from being deployed to staging or or a
higher environment. Let's rephrase that as an imperative: "Run the automated
tests before deploying to staging" (deploying to staging could be "publishing a
package").

Both a human and a CI server are well suited to this task. A CI server does not
tend to forget, but why should a human? A human is expected to run the tests
before pushing and allowing the CI server to run the tests, which makes the CI
server strictly redundant unless we have forgetful humans. So, we try and focus
on not being forgetful. We do this by expanding our imperative to: "Validate
your work before publishing it". It is not enough to run automated tests. Many
of our packages have interactive tests as well. These are just as essential to
validating our work, and they cannot be run by CI servers.

#### Slow Tests

In the past, some on our team have used CI to alleviate the pain of running long
test suites on developer machines. Very fast machines with complex
parallelization were employed to turn 20 minute test runs to 5 minute test runs.
This team focuses on smaller batches of publishing and therefore validation.
That is, we have many small repositories that are either software libraries or
deployments. The smaller the batch, the easier it is for a person to validate it
and the faster the test suite will run. Aside from the test suites that run
against slow 3rd-party services, or UI tests, most test suites complete in a
matter of single digit seconds. We simply do not have the circumstances that
would begin to excuse not running tests locally, so we expect it.

## Cost of Continuous Integration

Most teams set up Continuous Integration without even thinking about it. It is
seen as the cost of doing business, but rarely is that cost ever analyzed. There
are several costs worth considering.

### Reinforces Wrong Behavior

The [Ironies of Automation paper by Lisanne
Bainbridge](https://ckrybus.com/static/papers/Bainbridge_1983_Automatica.pdf) is
worth reading. There is a cost to automation that is often unrecognized. The
paper points to people losing the ability to take manual control when they have
relied on automation. In the case of CI, it has been observed that people are
less likely to run their tests locally when they know that they will be run by
the server. If people do not have that safety net, they are more likely to learn
to do the thing that they should be doing with or without the CI server in
place.

### Context Switching and Queueing

When you push work that is validated by CI, there is some period of time before
results are communicated back. A person must either wait patiently for the
notification and/or monitor the run. More likely than that is that they will
move on to another task so that if they do get a notification of a problem they
must context switch back to the original task to correct the work. The waiting
and context switching are not free.

### Maintenance Overhead

Even with the advent of yaml based and re-usable CI configuration, this
infrastructure must be maintained. It must be paid for both in a monthly service
cost and in time spent configuring, tuning, and automating. We have 100s of
repositories with tests, all of which would be subject to CI if that were part
of our standard practice. That could be a significant amount of work to both set
up and keep running over time.

### Encourages Automation for the Sake of Automation

As previously mentioned, our team values interactive tests. When CI is
available, a developer (automator) will have a natural instinct to want to
automate everything. Tests that should have been interactive because they are
best run with eyes-on will be automated and much of their value will be
squandered. Tests that cannot be automated will be discarded or never written in
the first place. In short, automation becomes the goal and anything less than
that is seen as inferior and unnecessary.

## Notes

- Our team does use a CI server for deployment. This is a technical necessity
  and we would stop doing it if we could.
- We started without CI servers for tests, so our team culture grew around that.
  If a team were to shut off their CI server that they had relied on for years,
  there would likely be a lot of challenges, regressions, and necessary
  learning. I believe that if a team went through this process they would get
  better, but every team is going to vary in its ability to do this and the time
  it would take to accomplish it.
