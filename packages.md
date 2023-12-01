[← Articles](README.md#articles)

# The Four Cs of Software Packages

A software package is a collection of code that is contained and distributed as a single unit. Most modern programming languages include a packaging mechanism. For Ruby, this is Ruby Gems, and for Node.js, it's NPM. Almost every project using one of these languages is going to use a number of these packages. It's so typical that it's hardly worth mentioning. What is less typical, however, is software teams building and privately distributing their own packages for use in their own project or projects.

The reasons for this are many. I've written about [monoliths](./monoliths.md) and about the [importance and benefits of partitioning](./partitions-and-compositions.md), so I will not rehash any of that here. Instead, I'll attempt to address what I believe is one of the most significant factors in software teams not building their own packages: they don't know how to do it. Said another way, it's unfamiliar or even hard.

In Rich Hickey's must-watch [Simple Made Easy](https://www.youtube.com/watch?v=SxdOUGdseq4) talk, he talks about the difference between hard and complex. I'd encourage you to watch it, but I'll summarize the part that's relevant to this article. Hard things can become easy through study and practice. Said another way, we all know how to learn. We were not born knowing how to program. We didn't know this language or that, or object-oriented design, or how to test, or much else. We learned those things. Building software packages is no different. This article is my attempt to make available the very basics of building software packages from a design perspective. I won't cover the technical aspects as those are going to vary language-to-language and I venture you could learn that in an afternoon.

I propose a handful of guidelines to get you started with how you think about partitioning software into packages. Packages should be cohesive, coherent, complete, and certified. The four Cs of software packages.

## Cohesive

When a consumer of your package installs it, they should not be surprised by anything within it. If they installed the package to get an API client for DocuSign, they would not be surprised for HTTP related code to be included. They would, however, be surprised if email related modules were included for sending emails when an API call fails. They would be even more surprised if the package contained blockchain-related modules, which clearly have nothing to do with DocuSign.

Said another way, everything in the package should be cohesive. The email-on-error code mentioned before may be perfectly reasonable behavior that some people may want. That should go in another package. That package would then be cohesive.

As an exercise, try to write a description of what is contained within your package. When deciding on introducing a new package, you might start with this. Pay special attention to any use of "and" in that description and consider whether or not you have a problem with cohesion. Also, pay attention to something that is overly general. A package that "Contains utilities used by applications" may not include the word "and", but "utilities" isn't very specific and thus this package will expand to contain this, that, and the other thing, and cohesion quickly goes out the window. These are sometimes called "junk drawer" packages.

## Coherent

What I mean by coherent is that it must stand on its own. You must be able to look at the description of it and not scratch your head. It must be useful on its own. For example, if I came across a package with a description of "Provides the left and top border style CSS for the text input", I would immediately be looking for the package that styles the rest of the text input.

The exception to this is extensions of another package. The email-on-error package referenced above only makes sense when used with the API client it is designed to extend. That should give you some pause, however. What if the email-on-error package could be further generalized? It could be used with every other API client library. You may have just stumbled on a better design, so it's worth considering. Don't take this too far. You have to be careful not to turn something that is meant to be specialized into something that is overly-generalized. That's a topic for another article.

## Complete

Along the lines of each package standing on its own, it must also contain everything that a user of that package needs. This includes, but is not limited to:

- Documentation &mdash; This should be self-evident, but it's worth mentioning that the amount of documentation is going to vary based on the particular package, its audience, and how afferent it is. It may be that the well-structured tests in the project are sufficient, or it may be that it needs an extensive README or even documentation site.
- Controls &mdash; A user of the package needs to be able to quickly try the package out and build tests with known-good data, examples, or anything else that's necessary to integrate or experiment with the package. We call these controls, named after "scientific controls". This is a large enough subject to deserve its own article, but here is a [video of a presentation](https://www.youtube.com/watch?v=jsMxMV2QW78) that a team member did.
- Diagnostic Substitutes &mdash; While the software community seems to be split on whether mock objects are must-use or must-avoid, we embrace the Liskov substitution principle by providing diagnostic substitutes for all of our classes that are used as afferent dependencies and warrant it. This allows users of our packages to test efferent objects of the package code without needing to couple tests to the particulars of the package code (i.e., mock objects). This is also an article on its own, but I would point you to the source material for this and much of how we do our object-oriented design, [The Doctrine of Useful Objects](http://docs.eventide-project.org/user-guide/useful-objects.html).

## Certified

Finally, we have to sign off on our package. We need to ensure that it is fully tested in all of the ways that we would anticipate our consumers using our package. This likely means some combination of automated tests, interactive tests, purpose-built test fixtures, etc. For example, if our package includes a UI control, we should have an example application that is capable of rendering that UI control so that we can test it.

If you ever find that you need to install your package into another project in order to fully test it (performing final inspection is the one exception to this), then that's a signal that you may be missing some testing capability in the package project itself. The package must stand on its own, and that includes its own testing and certification.

We typically indicate the first certification of a package by increasing its version number to `1.0.0`. That said, every new version release requires certification. That must be kept in mind when designing the certification process. The next developer working on the package needs to be able to certify it as well, which means they need to know how, and it needs to not be particularly onerous. Note that each certification is inherently different. A typo in some UI text does not require the same level of certification as a rewrite of a significant portion of the package. It is up to the developer doing the certification to determine exactly what they need to do.

## In Conclusion

This is only scratching the surface of the knowledge it takes to build packages. There is hidden depth in each of these points that will only be discovered and realized with continued practice. It does get easier. You will start to develop further intuition. It will actually start to feel unnatural to "just put more code in your monolith/monorepo".

I should also note that if you are the Ruby world, I'm talking about Ruby Gems here, rather than things like Packwerk packages. I've not used Packwerk, and in general, I would recommend separate repositories and the hard partitioning that Ruby Gems enforces rather than the speculative "partitioning" that Packwerk allows and encourages.

---

[Comments](https://github.com/aaronjensen/software-development/discussions/9)

[Subscribe to be notified of new articles](https://github.com/aaronjensen/software-development/discussions/8)

[All Articles](https://github.com/aaronjensen/software-development/blob/master/README.md#articles)

---

Copyright Aaron Jensen 2023-present
