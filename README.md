# great
The dataset for the variable-misuse task, described in the ICLR 2020 paper 'Global Relational Models of Source Code' [https://openreview.net/forum?id=B1lnbRNtwr]

This is the public version of the dataset used in that paper. The original, used to produce the graphs in the paper, could not be open-sourced due to licensing issues. See the public associated code repository [https://github.com/VHellendoorn/ICLR20-Great] for results produced from this dataset.

This dataset was generated synthetically from the corpus of Python code in the
ETH Py150 Open dataset
[https://github.com/google-research-datasets/eth_py150_open].

The dataset is presented in 3 splits: the training dataset `train`, the validation
dataset `dev`, and the evaluation (test) dataset `eval`. Each of these was
derived from the corresponding split of ETH Py150 Open.

Each dataset split is stored in a sharded text file. Each shard is named `<split>__VARIABLE_MISUSE__SStuB.txt-<shard number>-of-<number of shards>`.
Each of these files is a regular text file, in which every line contains a JSON-encoded example. Reading each line separately and then decoding it as JSON will reconstitute one example per line.

We chose numbers of shards to ensure no individual file is larger than the
GitHub-imposed 100MB per-file limit.

Shards of each split are placed in separate subdirectories.


Each example has the following fields:

* `source_tokens`: a list of strings; the original code (a Python function), split into tokens.

* `has_bug`: boolean; if True, a synthetic bug has been introduced, if False, this is the original code.

* `error_location`: integer; the token index into the code where a bug has been synthetically introduced.

* `repair_candidates`: a list of integers or strings; the tokens of code that might be the correct tokens after the synthetically introduced bug has been repaired. The integers capture the location of the tokens that constitute valid candidates. Bug-free examples also contain the string content of candidate tokens. For this Variable-Misuse dataset, it's safe to ignore the string candidates.

* `bug_kind`: an integer; the type of bug introduced (always 1 in this dataset).

* `bug_kind_name`: a string; the text type name of the bug (always "VARIABLE_MISUSE" in this dataset).

* `repair_targets`: a list of integers; all the tokens of code that constitute the correct repair of the synthetically introduced bug. Empty if there is no bug.

* `edges`: a list of triples of integers; has the form `[before_index, after_index, edge_type, edge_type_name]`, where the first is an index into the code of the source of a graph edge, the second is an index into the code of the target of a graph edge, the third is the numerical type of the edge, and the fourth is the text form of the edge type. Types include control flow and data flow information. The full list is
  * `"enum_UNSPECIFIED", 0`, used for debugging, hopefully none of those exist in the dataset;
  * `"enum_CFG_NEXT", 1`, control flow edge;
  * `"enum_LAST_READ", 2`, data flow edge;
  * `"enum_LAST_WRITE", 3`, data flow edge;
  * `"enum_COMPUTED_FROM", 4`, data flow edge;
  * `"enum_RETURNS_TO", 5`, control flow edge;
  * `"enum_FORMAL_ARG_NAME", 6`, semantic edge;
  * `"enum_FIELD", 7`, syntactic edge;
  * `"enum_SYNTAX", 8`, syntactic edge;
  * `"enum_NEXT_SYNTAX", 9`, syntactic edge;
  * `"enum_LAST_LEXICAL_USE", 10`, syntactic edge;
  * `"enum_CALLS", 11`, control flow edge.

* `provenances`: a json-formatted description of how this example was obtained. It contains the following fields:
  * `note`: a string; it explains how the license for the source code was detected (it can be 'bigquery_api', 'manual', or 'github_api')
  * `license`: a string; the applicable license (one of 'apache-2.0', 'lgpl-2.1', 'epl-1.0', 'isc', 'bsd-3-clause', 'bsd-2-clause', 'mit', 'gpl-2.0', 'cc0-1.0', 'lgpl-3.0', 'mpl-2.0', 'unlicense', 'gpl-3.0').
  * `datasetName`: a string; always ETHPy150Open.
  * `filepath`: a string; the GitHub repository name and file path from which this example was extracted.

Each example is released under the license of the originating GitHub repository
and project, as per the `license` field, described above. This means that the
dataset comprises individual files licensed under different terms. Please take
appropriate care when using this dataset.

Example code that uses the data is available in a separate repository [https://github.com/VHellendoorn/ICLR20-Great].
