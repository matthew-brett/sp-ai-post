# Background and rationale for AI guidelines

## A straightforward case

Let us say that I write a code file, call this `my_code.py`, to which I attach
a license that has only one clause (simplified from the BSD license):

> Copyright Matthew Brett
>
> 1. Redistributions of source or binary forms must retain the above copyright notice.

Now let us say that you take `mycode.py`, copy it into your own project, and
claim this as your copyright.

This would be a straightforward breach of copyright.  If I was so inclined,
I might take legal action, but even if I was not so inclined, you have abused
my generosity in taking my copyright.  I suspect that all open-source coders
would accept that this was wrong, and that we should do all that we can make
sure we are not doing that ourselves.

The situation does not change in any important way if you find and use some
software to remove my license before claiming your own copyright.

Now let us say that two colleagues have written code files for a similar
purpose.  Call these `joes_code.py` and `janes_code.py`.  Each has their own
license, identical to mine, but noting their own copyright — "Copyright Joe
Blogs" and "Copyright Jane Doe".

Your software takes these three code files (`mycode.py`, `joes_code.py` and
`janes_code.py`) and uses an algorithm to fuse them together into one file
`merged_code.py`.  It pulls off all three licenses and hands the code to you.
You claim copyright of the result.

In these simple cases, I continue to assert that most open-source coders would
see this as abuse of their copyright.

The last situation is a simplification of the process by which AI generates
code, with one important difference.  In the simplified case above, the
license-stripping software could tell you the set of licenses that could or
should apply to the output.  In general, AI-generated code results from
training on a massive body of code, all with different copyright, and very
little of which allows for re-use without attribution (see below).  Therefore
standard AI does not, and cannot, tell you the license of the code from with
the generated code is derived.  This makes it impossible for you, the user of
AI code, to honor the licenses of the code from which the generated code
derives.

## Upholding copyright before AI

Copyright has long been a concern in open-source coding.  One common problem is
avoiding the use of code with [Copyleft
licenses](https://en.wikipedia.org/wiki/Copyleft) (such as the GNU General
Public License (GPL), in projects with less-restrictive licenses, such as BSD
or MIT.

In order to avoid leak of copyright, one must use "clean room" methods; that
is, the person writing the BSD code *cannot read* the GPL code, because, if you
do read the GPL code, it will be very difficult to avoid the unconscious use of
the GPL implementation.  The BSD author must therefore keep themselves clean of
any possible influence of the code with an incompatible license.

This "clean room" principle applies to the use of AI-generated code.  As we
will see, standard AI models have "read" a huge body of code that requires
attribution, for most commercial models, is likely to have "read" Copyleft
code, with stricter requirements.  It is therefore not possible to assert with
any certainty that the generated code does not contain similar or identical
parts of code to which the original author's license will apply, and for which
you must apply their license terms.

## AI training sets and copyright

Tools like Github Copilot, [Cursor](https://www.cursor.com) and
[StarCoder](https://huggingface.co/blog/starcoder) use Large Language Models
(LLMs) trained on huge bodies of code. Call these Code LLMs.  In the case of
Github Copilot specifically:

> GitHub Copilot’s AI model was trained with the use of code from GitHub’s
public repositories

See the [Github Copilot section on IP and open
source](https://copilot.github.trust.page/faq#ip-and-open-source).

Starcoder is a set of models trained on data described at
[BigCode](https://www.bigcode-project.org).  BigCode is a research project to
develop a code LLM that a) uses code with an identified and "permissive"
license (such as MIT) and b) is itself developed with open code.  See
[https://huggingface.co/datasets/bigcode/the-stack#dataset-card-for-the-stack].

[Cursor defers to Claude and
GPT-4](https://forum.cursor.com/t/important-does-cursor-generate-copyrighted-code/74447).
It's very difficult to work out what Claude has trained on:

> Claude 3.7 Sonnet is trained on a proprietary mix of publicly available
information on the Internet, as well as non-public data from third parties,
data provided by data labeling services and paid contractors, and data we
generate internally.

[Claude 3.7 Sonnet system
card](https://assets.anthropic.com/m/785e231869ea8b3b/original/claude-3-7-sonnet-system-card.pdf).

It is similarly unclear for [GPT-4](https://arxiv.org/abs/2303.08774).

However, given Claude and GPT-4's abilities for code generation, and their
reference to "publicly available data on the internet", it is reasonable to
assume that Claude and GPT-4 do use public Github repositories, at least, as
training data.  An analysis of [Github
statistics](https://github.blog/news-insights/policy-news-and-insights/racing-into-2025-with-new-github-innovation-graph-data)
shows that most contributors (as measured by number of people pushing code
[^on-pushes]) push code covered by attribution type licenses (such as BSD),
with a significant minority being Copyleft (such as GPL), and a tiny proportion
being public-domain.  Only public-domain licenses allow use of the code without
applying license restrictions to the result.

[^on-pushes]: The [data file for this
  analysis](https://github.com/github/innovationgraph/blob/main/data/licenses.csv)
  groups by contributors (and country and year and quarter).  Quoting from [the
  license analysis
  description](https://innovationgraph.github.com/global-metrics/licenses):
  "The licenses metric represents the most popular software licenses in a given
  economy. It gives the total count of unique developers making at least one
  git push to a repository with a given license."

| License type  |  Percent contributions  |
| ------------  |  ---------------------  |
| Attribution   |  64.7                   |
| Copyleft      |  18.7                   |
| No license    |  13.9                   |
| Public domain |   2.7                   |

It is therefore reasonable to assert that very little of the training data for
standard code LLMs is suitable for remixing without violating the terms of
their respective licenses.

## A proposed response

As we would not allow code contributions that consist, in part, of code with
unacknowledged copyright, we should not accept code generated by AI.

We suggest that projects note this on their contribution pages and on their
pull-request templates, perhaps using something like:

> Code generated by AI from (for example) Github Copilot or Cursor, derives
from code with a wide variety of copyright terms, but, because of the nature of
the generation process, cannot tell you which of these terms might apply to the
AI output.  Therefore, as we cannot accept code that you have copied from
a project under another person's copyright, we cannot accept AI-generated code.
Please use the tick boxes below to confirm that you have turned off all AI code
generation in your editor, before writing your contribution, and that you have
not read any AI-generated code in the process of writing your submission.

## Distinction between legal and moral obligation

Previous discussions have revealed that there can be some confusion between
legal liability and a proper desire to honor the original license of code that
the AI uses for generation.

It is unlikely that any one particular use of AI will cause the original author
to pursue a copyright claim.  This is true for straightforward license abuse,
as it is for use of AI.  The author may not detect the abuse, because they are
not reading your code, or they may choose not to pursue the abuse, if they have
more productive ways to spend their time.  Nevertheless, the abuse has
occurred.  As we would not want our copyright abused, we should be careful to
avoid abusing the copyright of others, even if this would be unlikely to cause
us specific harm in terms of legal action, or the requirement to pull out the
offending code at some later date.

## Enforcement

Enforcement is important to the degree that we believe that honor-based
methods, such as the proposed affirmation above, will not be effective.  If we
believe these will be effective, at least in part, then it is difficult for us
to see why we would worry that formal enforcement would be difficult, or even
impractical.  We have still achieved at least part of our aim to reduce
copyright abuse of open-source code.

## Use-cases

There have been several interesting proposals for edge-cases in which the use
of AI may be acceptable.


## References

* [Github innovation graph license file](https://github.com/github/innovationgraph/blob/3c4fee675980239ea5b17e1329f9945eab4202e4/data/licenses.csv)

## Note in Caffe Milano

* Copilot's own IP description is in their [FAQ](https://github.com/features/copilot#faq) under "Responsible AI".   Specifically, it has:

  > What about copyright risk in suggestions? In rare instances (less than 1%
  based on GitHub’s research), suggestions from GitHub may match examples of
  code used to train GitHub’s AI model.

* In fact, Microsoft partially indemnifies some of its customers against
  copyright infringement with AI - for example [see this
  announcement](https://blogs.microsoft.com/on-the-issues/2023/09/07/copilot-copyright-commitment-ai-legal-concerns)

* We need to draw a distinction between:

  * "Will I be held liable for copyright infringement?" (the legal question
    / risk) and
  * "Am I respecting the author's stated intentions for re-using this code?"
    (ethical question).

* Describe the standard practice when dealing with code with incompatible
  license such as GPL.  "Clean room".
* We should consider AI code as code with an unknown license.  In particular,
  the code will (see analysis above) nearly invariably come (via the training
  data) from code that would, if used in your own project, apply further
  licensing constraints, such as attribution.
* Therefore we should employ a "clean room" approach to AI-generated code.
* It is therefore not acceptable to copy-paste AI-generated code into your own
  project (or pull-requests to another project that is publicly available).
* One typical use of AI is to generate suggestions for possible code, and then
  using that as the basis for writing one's own version of the same code.  On
  the "clean room" principle, this runs the risk of license leak, and we should
  not allow such use.
* Obviously - if one is not publishing or distributing the output from AI, one
  is not subject to generally subject to license terms.  You've always been
  able to take GPL code and do what you want with it, as long as you don't
  allow anyone else to use that code.
* There are situations in which AI may suggest changes, such as bug-fixes, that
  are so small as to be trivial (say, a few characters) and so obvious as to be
  the only practical change to achieve the desired result.  In this case it's
  difficult to imagine the generated code will be practically subject to
  a license from the training set.
* One use-case for AI that may have reduced license concern is translation of
  code written in one language to another, where there is a clear license for
  the original code for which one could meet the terms.  For example, imagine
  MATLAB code with an MIT license, translated by AI to Python.  One could give
  suitable attribution to the original author, conforming to the original
  license.  However, there is no way to be sure that the process of translation
  has not used training from code with other licenses.  Such code may be
  subject to those other licenses, but of course, the user would not be aware
  that was the case.  So we believe this case, though at the edge, is not safe
  in terms of respecting copyright.

## By

* Paul Ivanov
* Matthew Brett
