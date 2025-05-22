# Background and rationale for AI guidelines

## Main authors

* Paul Ivanov
* Matthew Brett

after a long an fruitful discussion at the [Scientific Python Developer Summit
2025](https://scientific-python.org/summits/developer/2025), with thanks to all
participants.

## A straightforward case

Let us say that we write a code file — call this `our_code.py` — to which
we attach a license that has only one clause (simplified from the BSD license):

> Copyright Paul Ivanov, Matthew Brett
>
> 1. Redistributions of source or binary forms must retain the above copyright notice.

Now let us say that you take `our_code.py`, copy it into your own project, and
claim this as your copyright.

This would be a straightforward breach of copyright.  If we were so inclined,
we might take legal action, but even if we were not so inclined, you have abused
our generosity in your act of removing our copyright and claiming our work as
your own.  We suspect that all open-source coders would accept that this was
wrong, and that we should do all we reasonably could to make sure we are not
doing that ourselves.

The situation does not change in any important way if you find and use some
software to remove our license before claiming your own copyright.

Now let us say that two colleagues have written code files for a similar
purpose.  Call these `joes_code.py` and `janes_code.py`.  Each has their own
license, identical to mine, but noting their own copyright — "Copyright Joe
Bloggs" and "Copyright Jane Doe".

Your software takes these three code files (`our_code.py`, `joes_code.py` and
`janes_code.py`) and uses an algorithm to fuse them together into one file:
`merged_code.py`.  It pulls off all three licenses and hands the code to you.
You claim copyright of the result.

In these simple cases, we continue to assert that most open-source coders would
see this as abuse of their copyright.

The last situation is a simplification of the process by which AI generates
code, with one important difference.  In the simplified case above, the
license-stripping software could tell you the set of licenses that could or
should apply to the output.  In general, AI-generated code results from
training on a massive body of code, with a huge number of different copyright
holders. A small proportion of the training code allows for re-use without
attribution (see below).  Therefore standard AI does not, and cannot, tell you
the copyright or license of the code from which the generated code is derived.
This makes it impossible for you, the user of AI code, to honor the licenses
and copyrights of the code from which the generated code derives.

## Upholding copyright before and after AI

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
attribution.  Most commercial models (see below) are likely to have "read"
Copyleft code, that imposes stricter requirements.  It is therefore not
possible to assert with any certainty that the generated code does not contain
similar or identical code fragments to which the original author's license will
apply.

## Copyright in AI training sets

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
license (such as MIT) and b) is itself developed with open code.  See the
[BigCode dataset card](
https://huggingface.co/datasets/bigcode/the-stack#dataset-card-for-the-stack).

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
training data.  Table 1 contains [our
analysis](https://github.com/matthew-brett/sp-ai-post/blob/main/open_source_licenses.ipynb)
of [Github
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

  ### Table 1. 2020 - 2024 GitHub contributors broken down by license type

| License type  |  Percent contributors   |
| ------------  |  ---------------------  |
| Attribution   |  64.7                   |
| Copyleft      |  18.7                   |
| No license    |  13.9                   |
| Public domain |   2.7                   |

It is therefore reasonable to assert that very little of the training data for
standard code LLMs is suitable for remixing without violating the terms of
their respective licenses.

See [Copilot's FAQ](https://github.com/features/copilot#faq) (under
"Responsible AI"), for Copilot's analysis of copyright infringement, at some threshold of detection. Specifically, it has:

> What about copyright risk in suggestions? In rare instances (less than 1%
based on GitHub’s research), suggestions from GitHub may match examples of code
used to train GitHub’s AI model.

It's difficult to know what "match examples" means, but nevertheless, 1% is
still too high a risk of license breach.

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

Put simply, this is the distinction between these two questions:

* "Will I be held liable for copyright infringement?" (the legal question
  / risk) and
* "Am I respecting the author's stated intentions for re-using this code?" (a
  moral or ethical question).

It is unlikely that any one particular use of AI will cause the original author
to pursue a copyright claim.  This is true for straightforward license abuse,
as it is for use of AI.  The author may not detect the abuse, because they are
not reading your code, or they may choose not to pursue the abuse, if they have
more productive ways to spend their time.  Nevertheless, the abuse has
occurred.  As we would not want our copyright abused, we should be careful to
avoid abusing the copyright of others, even if this would be unlikely to cause
us specific harm in terms of legal action, or the requirement to pull out the
offending code at some later date.

Understandably enough, Microsoft concentrates on the problem of legal liability in its Copilot Copyright Commitment.[^microsoft-legal]

[^microsoft-legal]: Microsoft partially indemnifies some of its customers
  against copyright infringement with AI - for example [see this
  announcement](https://blogs.microsoft.com/on-the-issues/2023/09/07/copilot-copyright-commitment-ai-legal-concerns)

## Enforcement

Enforcement is important to the degree that we believe that honor-based
methods, such as the proposed affirmation above, will not be effective.  If we
believe these will be effective, at least in part, then we will be less concerned
that formal enforcement would be difficult.  We have still achieved our aim to
reduce copyright abuse of open-source code.

## Use-cases

There have been several interesting edge-cases proposed that help to delineate
between acceptable and unacceptable uses of AI.

One [from Matt
Haberland](https://github.com/scientific-python/summit-2025/issues/35#issuecomment-2874656680)
was using AI to port code with a known license — say BSD — to another language
— say from MATLAB to Python.  Can one then honor the original license by
applying it to the port?

We think the answer is no.  Applying the "clean room" principle above, we know
that standard code LLMs have "read" a huge corpus of code with attribution or
even Copyleft licenses.  In asking the AI to port the original MATLAB code, we
cannot know the extent to which the AI has used other training code in the port.
For example, perhaps there is also a GPL implementation of this algorithm in
Python.  The AI porting process may use and incorporate part of the GPL code in
the port.

Another typical use of AI is to generate suggestions for possible code, and then
use that as the basis for writing one's own version of the same code.  From the
"clean room" principle, this also runs the risk of license leak, because the
contents of the AI suggestion has an unknowable set of applicable copyright.
As with our example of not looking at GPL code while contributing with a
permissive license, it is difficult for you to see whether your
re-implementation has used ideas and code from the AI suggestion.  We
should also require our contributors to forgo this use (see the suggested
wording above).

There are situations in which AI may suggest changes, such as bug-fixes, that
are so small as to be trivial (say, a few characters) and so obvious as to be
the only practical change to achieve the desired result.  In this case it's
difficult to imagine the generated code could reasonably be subject to
a license from the training set, any more than the same bug-fix would be
subject to the license of any original code with the same fix.

## References

* [Github innovation graph license
  file](https://github.com/github/innovationgraph/blob/3c4fee675980239ea5b17e1329f9945eab4202e4/data/licenses.csv)
