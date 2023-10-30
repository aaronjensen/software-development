[← Articles](README.md#articles)

# The Mythical Monolith

I realized recently that I've never seen a monolith &mdash; majestic or
otherwise. Every time that I look at something someone else labels a monolith, I
find a `Gemfile`, `package.json`, or similar file teeming with dependencies.
Even `rails new` produces a web application with 74 dependencies. Adding the
applications itself, you get 75 modules. So, is a monolith an application that
only has 75 [partitions](partitions-and-compositions.md)?

While I acknowledge I'm playing with the word's definition, I think that this is
an interesting way to look at the issue. When we start a new project, we start
it with 75 partitions. We then proceed to add file after file, class after
class, module after module, and many we rarely even consider creating a new
package (RubyGem, NPM Package, etc.). We are effectively declaring that packages
are for "them" and "we" don't need them. Is it because they are open-source? Is
it because they are separate teams or separate people?

When you install `devise` to add authentication to your app, are you invoking
some form of black magic or lost art? How did Plataformatec manage to create a
package for authentication that served many companies for years? When you use
`simple_form` to build your forms, how is that different than the mass of
helpers you have in your `app/helpers` directory for some other purpose like
rendering lists or images?

If these teams or individuals can create an open-source package that addresses a
single facet of a large web application, why can't product teams? It should
actually be easier: they have fewer users of the package, they don't have to do
any marketing, and they have control over all of the efferents, which means they
can make breaking changes without causing problems for people they've never met.

Ultimately, I think that it's just a matter of ignoring one of the fundamental
constructs of structural design because it's easier (at first). Wouldn't it be
easy when you got home from the grocery store to simply turn each bag of
groceries over and fill a large bin? That's what we do every time that we add a
new class to our "monolith" &mdash; we don't bother asking the question: "Where
does this go?"

I will admit that it takes more effort, but that effort lessens over time as you
get more practiced at it. I will also admit that I spent many years of my career
ignoring and failing to practice my ability to create packages for the products
I worked on. The most I would do was separate the client (e.g., React) from the
server (e.g., Rails API) into their own repositories, which was actually its own
kind of mistake. I wish that I had learned the effectiveness of building
separate packages earlier in my career.

I recently watched [a talk from 2023 Rails
World](https://www.youtube.com/watch?v=wV1Yva-Dp4Y) where the speaker was
discussing their product's transition from a monolith, to separate services, and
then back to a monolith. One of the reasons they gave for their return to the
monolith was that the monolith had additional capabilities that were being
refined and improving over time that the separate services did not have. For the
services that were Java (their monolith was Ruby), I could understand this. For
their services that were Ruby, this made absolutely no sense. Why weren't those
capabilities that were developed for one Ruby application usable in another? The
only thing that I could imagine was that they fell prey to the problem I'm
attempting to point to in this article.

Contrast this with our team which has tens of separately deployed web
applications that all look the same and share similar capabilities. A brand new
web project (generated from a GitHub template repository) on our project has
more than 180 gems, 50+ of which are internal, and 25+ of which are from the
[Eventide project](https://github.com/eventide-project/). We didn't get that for
free, but the cost was incremental when compared to the cost to actually build
the capabilities that we needed anyway. By building them into separate packages
from the beginning, we are able to more easily leverage them across our array of
projects &mdash; web or otherwise.

When you use `rails new`, you get 75 separate packages. Why stop there?

[Comments](https://github.com/aaronjensen/software-development/discussions/7)

---

Copyright Aaron Jensen 2023-present
