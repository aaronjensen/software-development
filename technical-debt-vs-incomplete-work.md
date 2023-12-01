[← Articles](README.md#articles)

# Technical Debt vs. Incomplete Work

The [debt metaphor](http://c2.com/doc/oopsla92.html) was introduced in 1992 by Ward Cunningham. Since then it has become commonly known as "Technical Debt" and is a term used (and misused) by many software teams. In [a video from Ward Cunningham](https://www.youtube.com/watch?v=pqeJFYwnkjE), it is described as well-written code that reflects your current understanding, with the knowledge that you will eventually refactor or update the code to reflect future understandings and updates to the design. It reflects the idea that the current version of the code might slow you down in the future, akin to paying interest.

Unfortunately, many teams have effectively turned the term into an excuse to write code poorly with the expressed, but not often realized, intent to "refactor" it later. I put "refactor" in quotes because it is another frequently misused word. Usually this goes along with a "just ship it" or "move fast and break things" attitude. Teams will often refer to the parts of their codebase that are problematic or resistant to changes as "technical debt". Often, these problems will not be addressed, and they will build on top of the code and encasement will occur, making it even more difficult to change later. Or, as they would call it, more technical debt would be added. Furthermore, introducing technical debt is sometimes described as an investment. When combined with changing the meaning to mean poorly written code, this is especially dangerous. Investments should not weigh you down.

We avoid this term entirely, and instead prefer to recognize that anything that has design problems, is written poorly, is unclear, or unnecessarily deviates from the team's norms, is simply, "incomplete work". This better reflects reality and works very well with the understanding that Lean and the software Kanban ideas have helped instill: The more work-in-progress you have, the longer it will take to complete work (effectively, Little's Law). Any work that is incomplete is, by definition, "in progress". Therefore, all of the things that we have left for later, or we recognize don't adhere to our norms but we choose not to fix, or that are poorly done, are work-in-progress.

Incomplete work can slow us down in many ways:

- At some point we may need to address it before we can proceed with another task, which means that we will be slowed down by the time it takes to address it.
- If we are lucky when we encounter incomplete work, we may remember that it is incomplete and we will act accordingly. This takes memorization, which is something I try to avoid necessitating. Alternatively, we may not, and we will be forced to check with our team, consult other resources, or conduct our own investigation to find out if the way things are is known incomplete, intentional, an undiscovered problem, or something else. In any case, it is a setback that takes time away from the current task.
- One of the worst problems with incomplete work occurs when it is not recognized as incomplete when it is encountered. In this instance, a developer may compound the problem by either duplicating the problem or by depending on it, which increases its afference, which makes it harder to change and will inevitably influence the design of the things depending on it. This is the sort of compounding problem with incomplete work. If not addressed, it leads to more and more incomplete work, which leads to more and more setbacks until, ultimately, the team's productivity drops precipitously.

I believe there is only one real answer to incomplete work: finish the work. This is often easier said than done. There are usually pressures from the business to produce more business value. It is often easier to ignore incomplete work and build on top of it in the short term. However, the short term is just the short term. Unless your business has little money left and must produce value to get more, or it has unlimited money in order to scale a development team exponentially, the medium and long term have to be considered. Otherwise development risks reaching the seemingly inevitable slowdown that almost all teams encounter.

There are two primary ways to complete the work. The first is to complete the work after the problem was introduced or recognized. The second is to never introduce the problem in the first place. Instead, we complete each task to the best of our team's ability and do not leave behind anything that is incomplete. Never introducing it is usually the best option. It may take longer to complete a work item, but once your team leaves the context of the current work item, it gets significantly more expensive to re-enter it. Not to mention the fact that you are opting in to the impacts described earlier. It will almost always be faster to complete the work initially than to pause and pick it back up later. There are very few exceptions to this in my experience.

Not all incomplete work will be able to be completed. I recommend writing it all down somewhere that your entire team can see. I don't recommend using your project management tool for this because I like to keep it clear what is value-added work and what is not. Instead, use a virtual whiteboard tool. Add a sticky note to it every time you encounter work that needs to be addressed, no matter how big or how small. Show it to your stakeholders (zoom out if you have to) and make sure they understand that as that list grows, your ability to deliver value in a timely fashion will drop and, eventually, it will stop. We maintain three lists: Trivial, Low Effort, and High Effort.

In software and in many other things in life, things are either getting better or they are getting worse. Very few things stand still. If your team is leaving behind incomplete work, they are leaving behind hazards and future setbacks. They are choosing short-term gain for long-term pain. Things will get worse. If your team is striving to complete work, things will get better. You will be able to build on past work by reusing both code and techniques. Your team will be able to do more with less, instead of less with more.

[Comments](https://github.com/aaronjensen/software-development/discussions/1)

[Subscribe to be notified of new articles](https://github.com/aaronjensen/software-development/discussions/8)

[All Articles](https://github.com/aaronjensen/software-development/blob/master/README.md#articles)

---

Copyright Aaron Jensen 2023-present
