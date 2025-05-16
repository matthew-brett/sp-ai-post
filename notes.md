# Background and rationale for AI guidelines

## Glossary

* LLM — large language model.

## Copyright

Tools like Github Copilot, [Cursor](https://www.cursor.com) and
[StarCoder](https://huggingface.co/blog/starcoder) use LLMs trained on huge
bodies of code.  In the case of Github Copilot specifically:

> GitHub Copilot’s AI model was trained with the use of code from GitHub’s
public repositories

See the [Github Copilot section on IP and open
source](https://copilot.github.trust.page/faq#ip-and-open-source).

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

License type     Percent contributions
------------     ---------------------
Attribution      64.7
Copyleft         18.7
No license       13.9
Public domain     2.7

It is therefore reasonable to assert that very little of the training data for
standard code LLMs is suitable for remixing without violating the terms of
their respective licenses.

## Variations in models

Consider [BigCode](https://www.bigcode-project.org), a research project to
develop a code LLM that a) uses code with an identified and "permissive"
license (such as MIT) and b) is itself developed with open code.  See
[https://huggingface.co/datasets/bigcode/the-stack#dataset-card-for-the-stack].


## References

* [Github innovation graph license file](https://github.com/github/innovationgraph/blob/3c4fee675980239ea5b17e1329f9945eab4202e4/data/licenses.csv)
