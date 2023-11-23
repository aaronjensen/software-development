[← Articles](README.md#articles)

# Subject-First Commit Messages

Take a moment and scan, not read, the following list as quickly as you can:

```
Fix `OrderedOptions#dig` for array indexes
Handle outdated Marshal payloads in Cache::Entry with 6.1 cache_format
Fix time travel helpers to work when nested using with separate classes
Added rails/railtie requires to AS/i18n_railtie.rb and AS/railtie
Fixed even more missing requires
Fix active_support/*/conversions by requiring missing files
Fix file cache store to split url-encoded keys on encode-sequence boundaries
Use RDoc block quote syntax [ci-skip]
Use custom class for pending migrations connection
Typo fix in BigDecimal job arguments warning
Fix code example in the field_name method
Drop dependency on mutex_m
Include `ActiveModel::API` in `ActiveRecord::Base`
Update classic_to_zeitwerk_howto.md
Add description for error_highlight gem
Fix extra blank line when no error_highlight
Bump psych to 5.1.1.1
Fix failing linter in `guides/source`
[ci skip] Fix shard docs followup
[ci skip] Fix shard docs
Revert "Add psych to the bug report template"
Add psych to the bug report template
Whitespaces
Avoid __method__
We don't use `::` to denote class methods
```

Did you spot the line about the `field_name` method?

Then, do the same thing here with these lines. Again, scan quickly, don't read:

```
Snapshot interval build argument overrides any snapshot interval declared by the class macro
EntityStore build method records the specifier argument when given
Category macro is optional on EntityStore when a category is given to the constructor
Tests are clarified
Category can be configured when constructing a store
Category declaration test is moved
Specifier can be configured when constructing a store
Specifier macro is implemented
Instance configure is invoked before the instance is assured
Instance configure template method called from constructor
Store's project method is an alias for fetch
Title is changed
Parenthesis are added to assert_raises and refute_raises
Automated test runner supplies exclude file pattern directly into CLI
Test files are compatible with TestBench 2.0
Unbalanced parenthesis in a log output is corrected
Log tags are standardized
Library-level log tags reduced to 'entity_store'
Snapshot classes must implement assurance
Snapshot implementation assures snapshot
Default batch size is sourced from reader class
Default reader batch size is 1000
Superflous test details are removed
Update of entity in substitute is tested
Updating substitute with new entity is tested
```

Did you spot a message about the Store?

The first list is a sample of commit message from [Rails](https://github.com/rails/rails). The second is from the [`entity-store` project in Eventide](https://github.com/eventide-project/entity-store). Chances are, unless you are already in the orbit of the Eventide community the first commit message style is what you are used to. It's likely what your team uses, as it is the commit message style that is typically recommended as a ["best practice"](./best-practices.md).

The second style likely feels foreign, and possibly uncomfortable. It's passive voice and present tense &mdash; all the things that we aren't supposed to make our commit messages. So why do the Eventide project and many teams that use Eventide choose to use this subject-first style of commit messages? Because it is more scannable. It is optimized for human cognition. Humans don't tend to read when looking at lists unless they absolutely need to. We scan. And when we scan, we want to see the most important things come first. Furthermore, the subject-first commit message style makes the commit about the change, rather than it being about what the person did that made the change. It's not about the self. It's about the code.

## Check Your Own Repository

Try this in one of your repositories:

```sh
git log --oneline | grep -v Merge | cut -d' ' -f2 | head -50
```

What do you see? Imagine that's all you see when you scan. That's not a perfect simulation, as when we scan we may pattern match further into the string, we may read two words or so, we may teach ourselves that the first word is unimportant and try to skip it, but all of that requires additional effort. Our job is hard enough as it is, so we want to take every chance we can to make it easier on ourselves.

## Personal Experience

When I first encountered the subject-first naming style that the Eventide project uses, I didn't like it. I didn't like it because of my own bias and my preference to conform to what is "common". It didn't look like what I was used to and I argued against it initially. I eventually recognized the benefit of scannability and decided to try it on my current team. It took some time to get used to writing messages in that style, and every new team member requires some amount of training and reinforcement. We are now three years in to using this style and our team now has a strong preference for it.

I would recommend trying this style out in one of your projects. You might be surprised once you get over the initial reaction to it and you get accustomed to writing and reading messages in this style.

## Guidelines

Here are some guidelines that we follow:

- You don't always need a verb if you are introducing something new. For example, "Widget tests" is preferred over "Widget tests are added".
- We prefer to use "is corrected," rather than "is fixed". E.g., "Widget reconciliation is corrected"
- When something is refactored or improved in some way, we tend to use "is clarified". E.g., "Widget creation is clarified"
- When describing a rename, use "rather than". E.g., "Widget, rather than sprocket"
- When describing a version increase, be explicit about both the old and the new version. E.g., "Package version is increased from 1.1.1 to 1.2.0"
- Don't bother with the 50 character subject rule, make the first line as long as it needs to be. Brevity is useful, but 50 characters is too limiting in my experience.

[Comments](https://github.com/aaronjensen/software-development/discussions/4)

---

Copyright Aaron Jensen 2023-present
