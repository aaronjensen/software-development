[← Articles](README.md#articles)

# Special Cause Variation

## Manufacturing

The manufacturing world discusses [two types of variation](https://www.isixsigma.com/dictionary/special-cause-variation/): common cause variation and special cause variation. Common cause variation is variation within control limits (i.e., acceptable or expected variation), while special cause variation is variation that falls outside of those limits. It is typically considered a problem to be addressed.

As an example, imagine that the color of a bike's paint varies slightly based on the batch of paint used. The shade of red of a particular bike is never exactly the same, but it is within tolerances. Now, imagine that every Monday, red bikes end up slightly darker than they do on the other days. The variation falls outside of tolerances and it cannot be attributed to common batch variation. An investigation is conducted and the team finds that every Monday, a machinist named Gus pours the remaining half of his coffee into a bucket that ultimately gets mixed into the paint. This causes the paint to be darker than usual, hence special cause variation.

## Software Development

For the purpose of this article, I will use the abbreviated version of the term that our team typically uses in practice: "special variation".

The example given results in a variation of the finished good. It doesn't directly necessitate more work from the team unless you consider scrapping or repainting the bike that is the wrong shade or returns of the bike that the customer is unhappy with because it doesn't match the color they were promised. Other types of variation result directly in members of the team having to do more work or at least, more difficult work. Imagine that every once in a while the same machinist, Gus, liked to fabricate reverse threaded nuts. He just likes to do that. He is expressing his individuality. So what happens when those nuts get mixed into the parts bin and Sandra is attempting to install brake calipers? Sometimes she has to turn the bolt clockwise and all is good. Sometimes she tries and nothing happens. She has to throw away that nut and try again. This slows her down.

This is exactly what we do when we put our own personal stamp on the code that we write or the practices that we follow. If a team doesn't have a set of established norms, this will be considered "business as usual", and it will simply mean that the team cannot gain as much efficiency in how they scan, understand, or produce code. Every part of the system will be different. Productivity will drop over time because people won't be able to work anywhere other than where they are used to without significant investment. Significant investment, memorization, and relearning are likely to become more and more necessary for the team.

Now, imagine that you have a team with norms established. These norms are all rooted in design fundamentals and they do not reflect personal style choices. They must be defensible from a software design position, and not merely a reflection of who the most powerful team member is. You write tests in certain ways, you adhere to a particular code style, you use a common voice in your commit messages, you practice software design in particular ways, etc. In other words, you have some amount of predictability, and when you go from one area of the code to another, things look familiar. You start to gain some significant efficiency as a team. You can reuse patterns, you can better understand code at a glance, and you may even start to realize some predictability in the amount of time it takes to accomplish a task.

What happens when someone does something counter to the norms? Let's say they use a `_` in URL path, rather than a `-`, or they title-case the label of a button, rather than sentence-case it. When you encounter this, it should stop you in your tracks. You will be required to understand why this was done in this way. You likely need to `git blame` and ask the author. If you find that the deviation was intentional and necessary, you need to add a comment explaining it so that the next person that encounters it will not have to repeat the same essential inquiry and investigation. If it was a mistake, you will need to socialize it with the team so that the team can learn from the mistake and it can be avoided next time. All of this takes time and energy. If a team member is sent down an investigatory path that leads to a dead end, then we've wasted the coworker's time and the company's money. It's not only wasteful, but it's disrespectful to colleagues.

## Causes and Countermeasures

Special variation has a real cost on a project. It necessitates extra effort from everyone involved. Ultimately, in my experience, there are only a few proximate causes on a team that values norms and standards: lack of experience, lack of attention, and lack of care.

A team that values norms and standards is likely going to have some sort of documentation of them. They are also going to have examples in code that are relatively consistent &mdash; we call these "exemplars". When starting on a task, it should be relatively easy to find previous examples of how something similar is done. If a team member can't find them, they can always ask other members of the team. If there aren't any exemplars, then it is novel work and likely requires some consultation with senior members of the team so that new norms can be established.

### Lack of Experience

When a person lacks the experience to correctly execute on the team's norms and standards, it is the responsibility of the team to ensure that they are properly coached, mentored, and paired with so that their lack of experience does not result in the introduction of special variation. The blame for a failure to do this does not rest on the individual, but on the team culture, process, and management. It should be addressed by management and the team at large, by whatever means necessary, so that the next team member that joins has the support they need and learns what the team values from the beginning.

### Lack of Attention

All of this requires attention to detail. It means that you can't be on auto-pilot and just do things the way you have done them on past projects, or the way that you naturally do them (naturally here means "without thinking", which should make the problem self-evident). It means stopping yourself constantly and asking, "What could I be doing wrong right now?" Fortunately, we typically have a pair (or more) engaged in our work as well. The other people working with us add to our attention and should be catching the things that we are missing. If a person isn't paying attention, and their pair isn't paying attention, you will inevitably end up with special variation or other mistakes.

Solving lack of attention is a challenge. I've already mentioned one countermeasure: pair-programming, or ensemble (mob) programming. There are also checklists. Those checklists can be team-wide or personal. There are other personal ones as well, like having a wall of index cards to remind you of things you often forget. You can walk that wall every day to help to train your mind to look out for those things. You can take breaks, you can meditate, you can set a timer and re-read your code every time it goes off, or whatever else works for you and your work cell. This is where our individuality shows &mdash; how we address our own personal lack of attention and skill growth so that we can work together with as much consensus, both in decision making, and work artifact, as possible.

### Lack of Care

Lack of care is both easier and harder to solve. It's easier, because a person who truly doesn't care about the work product or about consistency ultimately doesn't care about the team. They don't care about the frustration they cause by leaving inconsistency in their wake or the productivity hits they affect on their team as long as they are able to complete their work item, get the credit, and move on to the next thing. When seen in that light, addressing the problem becomes more of a management or HR concern. If a person does not care about the team, they likely do not belong on the team and they will probably be happier elsewhere. The harder way to do it, but also potentially more rewarding for everyone, is to help them to see the impact they are having. In other words, to help them to develop empathy and respect for their team.

### Team Discussion

On our team, when a mistake is made, or when special variation is found, we discuss it at our daily sync up (we don't do a stand-up meeting, we do what amounts to a daily discussion about the things that matter in that moment). We talk about what was found, what problems it caused, and often who introduced it, and potentially why they introduced it. We also use the time as an opportunity to reinforce the importance of reducing special variation and various techniques that can be applied to do that. This is meant to be an exercise in learning, not an exercise in public shaming. People do sometimes feel shame, and that's okay. That is something they can draw on for the next work item they do. They may feel bad that they impacted their teammates, and that's okay too, as that's how we learn and develop empathy. The expectation isn't that we don't make any mistakes, the expectation is that we acknowledge when we do and do our best to learn from them. That is how we, as individuals, and as a team, get better.

### Automated Checks

We try to keep our reliance on automated checks to a minimum. Aside from the fact that [we don't run tests on continuous integration servers](continuous-integration.md), we also don't generally use linters or other checkers on our code. Checks for many of our norms could not be easily automated, and we want to encourage our team to pay attention continuously. Linters tend to do the opposite. People will often do what a linter tells them to do without stopping to consider whether or not the linter is correct in that context. People are expected to do the hard work of ensuring that what they produce is up to our current standards.

### Norms and Standards Change Over Time

As we grow as a team, discover new techniques, or realize old techniques were problematic, our norms and standards will change. When this happens, anything that reflects the old norm is considered [incomplete work](technical-debt-vs-incomplete-work.md) and should be addressed. We don't always have the time to do this right away, but we log it and try to get to it when we can. We attempt to develop large-scale code changes as a skill &mdash; whether that be with bash scripting, editor proficiency, or even code parsing and AST manipulation. We maintain a repository of code migrations that we have run which acts as a resource for the team when we need to make similar changes. It is very important to us to have consistency throughout our codebase. This reduces the amount of time it takes to find exemplars, and how reliable they are. It's a too common occurrence to find multiple ways to do things, and when it happens, we encourage conversations and decisions on which is our currently preferred technique so that a norm can be established and applied.

## Conclusion

It takes a lot of work to maintain and enforce norms and standards on a team. Each team will have their own challenges and their own ways of dealing with them. Our team has around a dozen people, which is important to keep in mind when considering what is written here. That's not to say that reducing special variation isn't viable for larger teams, it's just to say that different countermeasures would be required. We require different countermeasures than we did when our team was only 4 people.

By reducing special variation, you increase a team's cohesion, skill, and capability. Code gets easier to maintain (or at least doesn't get harder), and, as the number norms and standards grow, so do opportunities for abstractions, templates, documentation, scripts, or other tools to help the team deliver value faster. Because the team is actively engaged in applying the norms, they are also continually questioning them and staying open to opportunities to improve them.

Software doesn't have to get harder to maintain over time, but it takes intention to ensure that it does not.

[Comments](https://github.com/aaronjensen/software-development/discussions/6)

[Subscribe to be notified of new articles](https://github.com/aaronjensen/software-development/discussions/8)

---

Copyright Aaron Jensen 2023-present
