# Background and rationale for AI guidelines

## Glossary

* LLM — large language model.

## Copyright

Tools like Github Copilot, [Cursor](https://www.cursor.com) and
[StarCoder](https://huggingface.co/blog/starcoder) use LLMs trained on huge
bodies of code. Call these Code LLMs.  In the case of Github Copilot
specifically:

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
shows that most contributors (as measured by number of people pushing code [^on-pushes])
push code covered by attribution type licenses (such as BSD), with
a significant minority being Copyleft (such as GPL), and a tiny proportion
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

## Variations in models


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
