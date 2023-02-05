# Onboarding

This document presumes you have an existing project with multiple developers
who agree in principle that some form of Opinionated Development is a good
idea, or that a team lead (a project manager, maintainer of an open source 
project, or similar person with authority) decides to implement Opinionated
Development regardless of the opinions of others. (This is often not a great
idea, but can sometimes be necessary.)

## Basic Steps

The high level onboarding process looks as follows:

1. Set up meta-tooling. (That is, tooling that helps you maintain, update
and install your tooling.)
2. Document the use of that meta-tooling and switch everyone over to it.
3. Move your existing tooling over to the meta-tooling.
4. Coordinate the first iteration of the ongoing process.

Looks simple? Maybe, but there are tricks to it.

### Meta-tooling

What is meta-tooling? Meta-tooling is tooling that exists for the purpose of
maintaining other tooling. An example of this in the Python world is 
[tox](https://tox.wiki/). Arguably, the original meta-tool is 
[make](https://en.wikipedia.org/wiki/Make_(software)). Some ecosystems come with
a standard meta-tool, making much of this onboarding easier as it's already done
when setting up a project in the first place. Some examples of these standard
meta-tools are [rustup](https://rustup.rs/) (and related tools like `cargo`), 
the `dotnet` CLI (and Microsoft's related tools built into Visual Studio), and
Apple's XCode suite. In each case, the tool isn't absolutely mandatory (while 
the `dotnet` CLI isn't mandatory for its meta-tooling features — it's pretty 
much required for writing .Net code), but by the fact that it's so tightly tied
into the environment for that platform, very few projects exist without them.

Not everything that looks like a meta-tool necessarily is, though, and some
environments have a suite of software that combines to be the meta-tool.
Python falls into this category. Tox is a glue layer on top of pip, virtualenv,
and several other projects to provide an environment that mostly "just"
requires tox to be installed. (Python also has other meta-tools, some of
them with a broader focus than others.)

A meta-tool should, at minimum, provide the following functionality:

1. It (and its dependencies) should be everything (or close to everything) a
new contributor needs to install to set up an environment. Perhaps this
meta-tool can't handle every tool used by your project (e.g. `tox` alone
doesn't control multiple Python versions on a machine or install tools such
as pyright), but it should be able to tell you what you're missing.
2. It should provide a way for developers to integrate the tools of their
choice rather than being the "everything and nothing more" tool. In environments
where there's a standard meta-tool, that can come in the form of plugins. In
more heterogeneous environments such as Python and C, the meta-tool should
provide a way to configure and manage other tools.
3. A meta-tool shouldn't itself be highly opinionated (though some level of
being opinionated is fine). Instead, it should get out of a developer's way and
allow the developer to choose their opinionated tools. (In the case of an
environment's standard meta-tool, it can be highly opinionated by default, as
long as it doesn't force the developers into things they don't want.)
4. A meta-tool should be at least somewhat self-bootstrapping and independent
of the environment in which your code runs.

A detailed breakdown of tox as a metatool can be found in the 
[examples](examples/TOX.md).

### Documentation

It's a good practice in most software development projects to have at least
two pieces of developer documentation: a `HACKING` file and a `CONTRIBUTING` 
file.

The distinction between these files is minor, but important. The HACKING file
is a `how-to` for setting up a development environment and checking code. It
should consist of a clear set of requirements of what the developer needs
installed and a brief introduction to how to use the tools for your project.

The CONTRIBUTING file, on the other hand, is a set of policies for how to
interact with the project. This can include technical things (such as
commit and PR formatting), but also non-technical things like reminders about
the project's code of conduct.

Example [HACKING](examples/HACKING.md) and [CONTRIBUTING](examples/CONTRIBUTING.md)
files are available.

### Migrating your tooling

It's important to migrate all of your tooling to a meta-tool as soon as 
possible after selecting one. The only thing more confusing to a new contributor
than a series of wildly-varying tools to use is when most things use the
meta-tool but one very important step doesn't. This is part of why a meta-tool
needs to be flexible — it needs to be able to act as a single coherent interface
to development on your project.
