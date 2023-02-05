# Process

This repository contains the development version of a recommended process for
incorporating Opinionated Development into a project. This isn't the only way
to do it, but the goal is to be a generally acceptable way.

## Non-goals

This process is not intended to enforce specific opinions. Where examples
exist, they may be freely used, but the purpose of these examples is 
illustrative, not prescriptive.

### Why is everything in Python?

As it exists right now, much of this process is centered around Python code.
While the process is designed to be language-agnostic, Python is the primary
illustrative language so far. Additional examples in other languages are
highly encouraged as pull requests. (Please note the `LICENSE-CODE` document
in this repository.)

<details><summary>Why Python is used</summary>

1. In gaining its reputation as "executable pseudocode," the core developers
of Python intended the language to be highly readable, whether one knows the
language or not. This often (but not always) makes it a good choice for 
illustrating concepts that apply across languages.
2. The Python community is welcoming and open to new developers and ideas, and 
it has a rich tapestry of differing opinions. This can be used to illustrate 
both the strengths and the weaknesses of specific methods.
3. Unlike many newer languages such as go, rust and elixir, Python has a 
messy history that makes many decisions harder. This history is apparent with
joke [Python Enhancement Proposals](https://peps.python.org/pep-0401/) that
gently poke fun at disagreements within the community.
4. The original author of this process is most familiar with Python and has
been heavily influenced by discussions within the Python community.

</details>

As with everything in the Opinionated Development Drive, discussions and
disagreements are encouraged, and additional examples in different languages
are also encouraged.

## Basic steps

Opinionated Development exists for the purpose of improving code quality. This
means that anything in this process that won't improve code quality in a
specific project should be adapted, modified, or skipped.

Opinionated Development is also an ongoing process. It is not, and never should
be, something applied "just once" and then allowed to languish. Maladaptive
standards like this can make both code quality and developers' lives worse,
not better.

### Ongoing process

As such, it's important to first understand the "end goal" of implementing
Opinionated Development. The ability to efficiently implement the process in 
this subsection is itself the end goal of the onboarding process below, but the
end goals of this process are:

1. Better code quality.
2. Happier, more productive developers.
3. A project that is easier for new developers to contribute to.

In order to achieve this, Opinionated Development and software tooling must be
considered a part of a project's regular maintenance cycle. The cadence for this
depends on the specific project, but some recommended guidelines are:

1. Neither too frequent nor too rare. If your development works on 2-week
sprints, iterating this process every sprint is far too frequent. On the
other end of the spectrum, an application that gets a new version every two
years might consider multiple process updates per release. Ultimately, it's
up to those who own the software to choose a cadence, but it is recommended
that updating the cadence be one of the things considered in each cycle.
2. Try to avoid doing it "in the middle of things." If your project has a `main`
branch and release branches, updating the `main` branch could be one of the
first things done after a release branch is forked. This might mean that the
major decisions are made before the new branch is forked, but applied 
immediately afterwards.
3. Code changes should always be small steps. If you're, for example,
implementing a dozen new linting rules, put the addition of each one and its
related code changes in its own commit. Depending on how much has to be changed
for a new rule, it may even make sense to enable that rule progressively for
different parts of a project.

#### The process itself

That's all well and good, but a process needs to exist in order to implement it
correctly. The steps of the process are documented in 
[ONGOING_PROCESS.md](ONGOING_PROCESS.md).

### Onboarding

Before a project can run the ongoing process, it must take a much bigger, much
scarier onboarding step. This onboarding step is often the reason a project
doesn't end up making changes, even ones everyone involved agrees on.
[ONBOARDING.md](ONBOARDING.md) contains steps to make this easier.
