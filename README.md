# great
The dataset for the variable-misuse task, used in the ICLR 2020 paper 'Global Relational Models of Source Code' [https://openreview.net/forum?id=B1lnbRNtwr]

This dataset was generated synthetically from the corpus of Python code in the
ETH Py150 Open dataset
[https://github.com/google-research-datasets/eth_py150_open].

The dataset is presented in 3 splits: the training split `train`, the validation
dataset `dev`, and the evaluation (test) dataset `eval`. Each of these was
derived from the corresponding split of ETH Py150 Open.

Each split is stored in JSON format, across a number of file shards, each named `<split>__VARIABLE_MISUSE__SStuB.json-<shard number>-of-<number of shards>`.
We chose numbers of shards to ensure no individual file is larger than the
GitHub-imposed 100MB per-file limit.

Each shard is a properly formatted JSON list. To reconstruct, parse each shard
into a list of distionaries, and then concatenate the lists of dictionaries
together into a single list. Shards of each split are placed in separate subdirectories.


Each example has the following fields:

* `source_tokens`: a list of strings; the original code (a Python function), split into tokens.

* `has_bug`: boolean; if True, a synthetic bug has been introduced, if False, this is the original code.

* `error_location`: integer; the token index into the code where a bug has been synthetically introduced.

* `repair_candidates`: a list of integers; the tokens of code that might be the correct tokens after the synthetically introduced bug has been repaired.

* `bug_kind`: a string; an integer; the type of bug introduced (always 1 in this dataset).

* `repair_targets`: a list of integers; all the tokens of code that constitute the correct repair of the synthetically introduced bug.

* `edges`: a list of triples of integers; has the form `[before_index, after_index, edge_type]`, where the first is an index into the code of the source of a graph edge, the second is an index into the code of the target of a graph edge, and the third is the numerical type of the edge. Types include control flow and data flow information.

* `provenances`: a json-formatted description of how this example was obtained. It contains the following fields:
  * `note`: a string; it explains how the license for the source code was detected (it can be 'bigquery_api', 'manual', or 'github_api')
  * `license`: a string; the applicable license (one of 'apache-2.0', 'lgpl-2.1', 'epl-1.0', 'isc', 'bsd-3-clause', 'bsd-2-clause', 'mit', 'gpl-2.0', 'cc0-1.0', 'lgpl-3.0', 'mpl-2.0', 'unlicense', 'gpl-3.0').
  * `datasetName`: a string; always ETHPy150Open.
  * `filepath`: a string; the GitHub repository name and file path from which this example was extracted.

Each example is released under the license of the originating GitHub repository
and project, as per the `license` field, described above. This means that the
dataset comprises individual files licensed under different terms. Please take
appropriate care when using this dataset.
