# Opinionated Development: Ongoing process

This document contains the ongoing process for Opinionated Development.
It is separated out in order to provide an easy reference for anyone who is
currently in charge of a specific iteration.

## Steps

Below are the steps of the process, with discussion below that.

1. Research or discover possible improvements
2. Gather consensus about changes
3. Implement changes
4. Gather consensus about the implementation
5. Apply the changes consistently

The first step, researching and discovering possible improvements, should be
permanently ongoing. There should be a central place to collect these
suggestions on an ongoing basis. For a workplace team, an open task to which
any member of the team may add suggestions is one way to handle it. Suggestions
should often include links, even if they're just to blog posts or articles
about the change. In this step, you're simply collecting ideas. At some point,
you will cut off that collection to go to the next steps, but when you do so
a new basket should be provided immediately, so an idea that "just missed the
window" can still be included in the next round.

Once you have a list of ideas, it's time for one person to research them and
come up with recommendations. In this step, the person who is assigned the
research should attempt to be as unopinionated and neutral as possible. Collect
the positives and negatives of each change, ready to present them to the team
in as unbiased a manner as you can. (NOTE: A future project for the
Opinionated Development Drive is to collect recommendations to help with this
research.) Present these recommendations to everyone appropriate and consider
feedback. This is time for consensus-building, not democracy. That means that if
one person feels strongly and disagrees with everyone else, who have only weak
opinions on the matter, the strong opinion wins. Be conservative, too. If
there's a disagreement, it's better to delay a change until the next cycle
than to implement something people dislike. But, with that said, ensure the 
dislike is for valid reasons.

Step 2 is by far the most difficult, especially for engineers. It's not a
straightforward process. It takes compromise and a willingness to adjust, and
there will seldom be a single correct answer, even when some people think there
is. In fact, people may strongly disagree about what the correct answer is.
Listen to everyone. Collect examples. Perhaps the answer is that a particular
standard, rule, or tool is appropriate for a portion of a project, but wholly
inappropriate for another portion. This is fine too, as long as it's documented.

Implementation is mostly pretty straightforward. Create a series of tasks for
implementing each change. In an open source project, these can be great to
leave open, labelled as a "good first task" for a newbie who wants to get
contribute. If implementing a particular change is not straightforward, it
should be done by a core maintainer or senior developer. The biggest advocate
for a specific change is often the worst person to implement it, as they may
become personally attached to it. Rather, try to find someone indifferent or
even mildly opposed to the change to implement it.

Before a change from this process goes into the main branch of a project, it
should meet stricter requirements than the normal requirements for code
changes. It should get more sets of eyes. It should be an opportunity for
people to say "now that I've seen this, I'm not sure I like it." Remember,
criticism should be for the change itself, not for the person making it.

Finally, part of the reason for stricter requirements on these changes is that
they should be consistent. It's often okay to use disable comments, to set
a linter to only warn (not error) on certain rules, and even to have rules
enabled or disabled in different sections of a project. (For example, in
Python, documentation strings are often not needed in test code.)

## Ownership

As mentioned in the introduction, one person should be in charge of an iteration
from start to finish. This doesn't mean they have to implement the changes.
Rather, this person should be guiding the discussion and moderating
disagreements. Preferably, each iteration will be owned by a different person
so many views, research styles, and perspectives can be included.
