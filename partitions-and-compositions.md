[← Articles](README.md#articles)

# Partitions and Compositions

## Exercise

I'm going to present two scenarios and I'd like you to consider which would take less overall effort to accomplish.

### Scenario 1

You have a monolithic web application that has been developed over the course of the last year. You would like to split this application into multiple applications, services, and libraries. They should be able to be developed and deployed separately, without changing the end-user's experience.

### Scenario 2

You have multiple applications, libraries, and services that are deployed and
developed separately. They provide a cohesive experience to the end-user and you
would like to combine them into a single deployable application.

### Questions

- Which of these do you think would be easier? Why?
- Think about your current application, assuming it has some amount of monolithism. What would it take to split it into several applications?
- What would it take to combine one of the open source libraries you rely on into your application (this is a bit of a trick question, because it is already in use by your application and likely deployed by it, but for the purposes of this exercise consider combination to be: "in the same repository")?

## Discussion

I'm quite sure that most people who have experience doing or trying these things would answer that combining things that are already separate is far easier than separating things that are already combined. The reason for this is typically coupling and entanglement. When things are developed and built together they are often entangled, or what designers refer to as "tightly coupled". Even if things are loosely coupled, those couplings may create a sprawling web that can be difficult to understand, and may even have cycles. You may have fallen into the trap of "Fat Model, Skinny Controller" and find that you have a single `User` or `Product` class that most of your code depends on. In all likelihood, it may be impossible to split an application into more than one part that was developed as a single monolithic application. At least, not without rewriting it.

Contrast that with combining things, which is often as easy as moving files around. There are also multiple ways to combine things. You can combine applications with libraries by taking on dependencies. You can combine applications with services by deploying them both separately and integrating the application with the service. You can combine web servers by deploying them separately and adding a proxy server like nginx. Or, you could combine them all into a single repository or even a single deployed application. The point is, once things are separate (or partitioned), it is easy to combine them. If they are entangled &mdash; I'm intentionally avoiding the word "combined" here, which implies that they are separate &mdash; they can be near impossible to separate.

I quite like this quote that was referenced in ["Object Thinking" by David
West](https://www.amazon.com/Object-Thinking-Developer-Reference-David-ebook/dp/B00JDMPOKM/ref=sr_1_1?crid=19TIKKMLRDGAL&keywords=object+thinking&qid=1697930301&sprefix=object+thinking%2Caps%2C104&sr=8-1):

> [First,] perceiving and bringing together under one Idea the scattered particulars, so that one makes clear ... the particular thing which he wishes [to do]... [Second,] the separation of the Idea into classes, by dividing it where the natural joints are, and not trying to break any part, after the manner of a bad carver. ... I love these processes of division and bringing together ... and if I think any other man is able to see things that can naturally be collected into one and divided into many, him will I follow as if he were a god. - Plato, circa 400 B.C.

What I like about it is that it stresses the importance both of bringing together and of separating. You cannot bring together unless you have separation. Separation can be done well, or it can be done poorly. Your partitions can either work for you, or against you. All of this is the essence of design. Things that are well designed stand on their own. They are useful on their own, in their own way, and they can be combined with other things that are well-designed to create more complicated and potent compositions.

Consider for a moment the humble screw. On its own, it doesn't do much. But it **does** stand on its own. It is its own thing. It does not need to be screwed into something to be a screw. Sitting on a desk, it is a screw. Now take that screw and consider all of the possible things that it can be used to build. They are limitless.

We may think that our job is to make the end product. We would be right, to an extent. But that extent would be missing the benefits of creating individual parts and composing them into a whole.

## Eventide Project

Let's look, as an example at the [Eventide Project packages](https://github.com/eventide-project). Eventide could have been a single Ruby Gem. Instead, Scott Bellware and Nathan Ladd built the libraries they needed in order to build Eventide. Those became part of the Eventide project. As a result, we now have several Ruby gems that have absolutely nothing to do with autonomous components but are part of the Eventide project. In other words, they needed to fasten two things together, so they invented a screw. They needed something to make sound, so they invented a speaker. We use several of these libraries in our web applications and libraries because they are generally useful.

Here are a few example packages, though I do encourage you to look around on your own:

- [Schema](https://github.com/eventide-project/schema) - Data structures with typed attributes
- [Set Attributes](https://github.com/eventide-project/set-attributes) - Bulk assignment of attributes
- [Settings](https://github.com/eventide-project/settings) - Settings class that can assign settings to objects
- [Try](https://github.com/eventide-project/try) - Attempt execution and return whether or not the operation succeeded

Again, none of these have anything directly to do with autonomous components any more than a screw has to do with a computer. Yet, they are used by the libraries that do support building autonomous components. They can, and are, also used by other libraries such as HTTP clients to third-party APIs. This is the benefit of partitioning.

## Our Project

We have followed suit in our project. As such, we have multiple, generally useful libraries that are composed into more specific applications and services. Some of them could even theoretically be open-sourced and used by other teams around the world in completely different domains than our application.

## Effort

It takes more work to build separate libraries than it does to build everything into a single application, but only initially. There are two dimensions that are more challenging. The first is that you must learn new skills do to this, but that's something you have already spent a lifetime doing. The second is that it takes more effort up front to establish patterns and libraries for your specific project. This gets easier and takes less effort as your team gets better at it. You will have to develop techniques for dealing with the boilerplate (e.g., template projects) and learn how to make changes across multiple repositories (e.g., with code-migration scripts).

Once you have done these things, the benefits start to become so apparent, they are impossible not to appreciate. The momentary slowdown is infinitesimal compared to the acceleration that will happen over the life of the project as a result of proper decomposition.

## Benefits

This is an incomplete list of the benefits that our team has experienced by taking the effort to create partitions with separate libraries, applications, services, and deployments:

- Most of our test suites take less than 1 second. Those that take longer are typically UI Interaction tests (via Capybara) and most of those take less than 30 seconds to run on a laptop. This contributes in our ability to be productive without having to run tests on a [continuous integration server](continuous-integration.md).
- All updates, whether they be Rails, Ruby or anything else can be done in small batches. We can update a single web application, deploy it, and test it without impacting any other application. Once we are satisfied with the update, we can do the same to our other applications, one-at-a-time, or in a divide-and-conquer approach where each pair on the team takes a few of them and updates them.
- Partitioning makes future partitioning easier. Rarely can you take a single thing and split it into two. You often need to split it into three, with the third thing being shared by both. By building things separate from the beginning, we are able to make use of individual parts in ways that we did not plan for because they are already separate.
- Smaller things are easier to understand. Each repository has, by definition, a fraction of the total code in our project. We know that each repository stands on its own and can be understood on its own. You can see what a package's dependencies are just by looking at its `gemspec` or `package.json`, which tells you a tremendous amount about what that thing does. Contrast this with the single `Gemfile` in the monolithic Rails application. Which code depends on `devise`, `sidekiq`, `dry-schema`, or anything else?
- We are very often working in different repositories. It is fairly rare for our team of more than 10 to be working in the same repository. At the time of writing, we have more than 400 repositories, and conflicts (merge, cognitive, or otherwise) are rare.
- We are very often doing work in a greenfield repository. This means we can commit directly to `master` and have no fear of anyone else working in the same place, which reduces coordination cost. We still have a few relatively high-churn repositories, but they are the exception, rather than the rule.
- Circular dependencies are practically impossible. RubyGems prevents them at the `gemspec` level, and through diligence and consideration (i.e., design) we prevent them and consider dependency direction (i.e., afference and efference).
- Violating boundaries is practically impossible. When things that are meant to be separate are located in one place (like a single repository) it is easy for a developer that is under pressure to "cheat" and depend on somethings directly that they should not. This can create entanglement that can be difficult or impossible to untangle later.
- By practicing this, we get better at it. Vince Lombardi said, "Practice does not make perfect. Perfect practice makes perfect." I'm not trying to imply that anything we do is perfect. Perfection is a direction, not a destination. I'm just trying to say that by practicing partitioning, we get better at partitioning. By seeing the partitions in the large (applications and packages) we also get better at seeing the partitions in the small (classes, modules, and methods).

## Implementation

This is not a guide for doing partitioning. I don't think that a useful guide could be written. It is [subtle knowledge](https://madabout.software/articles/subtle-knowledge-crude-knowledge/) and therefore difficult, or impossible, to teach in written form. It's something that has to be practiced. All I know how to do is describe it and point to its benefits. Ultimately, it comes down to following first-principles as stringently as possible. Read about and understand efference, afference, specialization, and generalization. As well as [my other articles](README.md#articles), Scott Bellware's blog provides several great articles that cover this subject and others:

- [Afference: The Silent Killer](https://madabout.software/articles/afference-the-silent-killer/)
- [SAGE: Early Warning System for Design Mistakes](https://madabout.software/articles/sage-early-warning-system-for-design-mistakes/)

[Comments](https://github.com/aaronjensen/software-development/discussions/5)

---

Copyright Aaron Jensen 2023-present
