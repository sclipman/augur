# __NEXT__


# 4.0.0 (24 April 2019)

## Features

* distance: New interface for specifying distances between sequences.  This is
  a **backwards-incompatible** change.  Refer to `augur distance --help` for
  all the details.

* export: Add a `--minify-json` flag to omit indentation in Auspice JSONs.

## Bug fixes

* frequencies: Emit one-based coordinates (instead of zero-based) for KDE-based
  mutation frequencies

## Data

* Include additional country lat/longs in base data


# 3.1.8 (13 February 2019)

## Bug fixes

* titers: fix calculation of `mean_potentency` for model export

# 3.1.7 (5 February 2019)

## Bug fixes

* Update to TreeTime 0.5.3
* tree: Fix bug in printing causing errors in Python versions <3.6
* tree: Alter site masking to not be so memory intensive

# 3.1.6 (29 January 2019)

## Features

* filter: Allow negative matches to `--exclude-where`. For example,
 `--exclude-where country!=usa` would exclude all samples where metadata `country` does
 not equal `usa`.
* tree: Allow `--exclude-sites` to work with FASTA input. Ensure that indexing of input
 sites is one-based.

## Bug fixes

* fix loading of strains when loading titers from file, previously strains had not been
 filtered to match the tree appropriately

# 3.1.5 (13 January 2019)

## Features

* frequencies: Add `--ignore-char` and `--minimal-clade-size` as options.
* frequencies: Include `--stiffness` and `--inertia` as options.
* titers: Allow multiple titer date files in `--titers` import.

## Bug fixes

* filter: Fix `--non-nucleotide` call to include `?` as allowed character.
* tree: Fix `--method raxml` to properly delimit interim RAxML output so that
  simultaneous builds don't conflict.

## Data

* Include additional country lat/longs in base data  

# 3.1.4 (1 January 2019)

## Bug fixes

* frequencies: Include `counts` in `augur frequencies` output JSON to support
  downstream plotting.

## Data

* Include additional country lat/longs in base data

# 3.1.3 (29 December 2018)

## Features

* filter: Add `--non-nucleotide` option to remove sequences with non-conforming
  nucleotide characters.

## Bug fixes

* Revise treatment of `-`, ` ` in `augur parse` to leave `-` as is and remove white
  space. Also delimit `[` and `]` to `_`.
* Fix bug in naming of temp IQTREE fixes to prevent conflicts from simultaneous builds.

## Data

* Include additional country lat/longs in base data

## Development

* Remove non-modular measles build in favor of [nextstrain/measles](https://github.com/nextstrain/measles) repo.

# 3.1.2 (21 December 2018)

## Bug fixes

* Update dependencies

# 3.1.1 (21 December 2018)

## Bug fixes

* filter: Fix `--include-where`. Adds an `all_seq` variable needed by the logic to
  include records by value. This was previously working for VCF but threw an exception
  for sequences in FASTA format.
* Update flu reference viruses and lat longs.
* Update dependencies

# 3.1.0 (18 December 2018)

## Features

* reconstruct-sequences: Include `augur reconstruct-sequences` module that reconstructs
  alignments from mutations inferred on the tree
* distance: Include `augur distance` module that calculates the distance between amino
  acid sequences across entire genes or at a predefined subset of sites
* lbi: Include `augur lbi` module that calculates local branching index (LBI) for a
  given tree and one or more sets of parameters.
* frequencies: Include `--method kde` as option to `augur frequencies`, separate from the
  existing `--method diffusion` logic. KDE frequencies are faster and better for smaller
  clades but don't extrapolate as well as diffusion frequencies.
* titers: Enable annotation of nodes in a tree from the substitution model

# 3.0.5.dev1 (26 November 2018)

## Bug fixes

* translate: Nucleotide ("nuc") annotation for non-bacterial builds starts at 0
  again, not 1, fixing a regression.

## Documentation

* Schemas: Correct coordinate system description for genome start/end
  annotations.


# 3.0.4.dev1 (26 November 2018)

## Bug fixes

* validate: Fix regression for gene names containing an asterisk.

## Development

* Fix Travis CI tests which were silently not running.


# 3.0.3.dev1 (26 November 2018)

## Features

* refine: Add a `--clock-std-dev` option

* traits: Add a `--sampling-bias-correction` option for mugration model

* validate: Gene names in tree annotations may now contain hyphens.  Compatible
  with Auspice version 1.33.0 and later.

* All JSON is now emitted with sorted keys, making it easier to diff and run
  other textual comparisons against output.

## Bug fixes

* filter: Only consider A, T, C, and G when calculating sequence length for the
  `--min-length` option.

* filter: Allow comments in files passed to `--exclude`.

* filter: Ignore case when matching trait values against excluded values.

* Normalize custom geographic names to lower case for consistent matching.

## Data

* Fix typo in geographic entry for `netherlands`.

* Schemas: Reconcile naming patterns used in gene definitions and tree
  annotations.

## Development

* Upgrade TreeTime dependency to 0.5.x and at least 0.5.1.

* Add an `environment.yml` file for use with `conda env create`.

* Stop testing under Python 2.7 on Travis CI.


# 3.0.2.dev1 (27 September 2018)

## Bug fixes

* translate: Fix broken `--help` message


# 3.0.1.dev1 (27 September 2018)

## Features

* align and tree: The --nthreads option now accepts the special value "auto" to
  automatically set the number of threads to the number of CPU cores available.

* Alias `augur --version` to `augur version`

## Bug fixes

* tree: The --nthreads option is now respected.  Previously all tree builders
  were ignoring the value and using either 2 threads (RAxML, IQ-TREE) or as
  many threads as cores (FastTree, if the OpenMP version).

* translate: Check for and, if necessary pad, nucleotide sequences which aren't
  a multiple of 3 earlier to avoid errors later.

* export: Optionally write inferred nucleotide and amino acid sequences (or
  mutations) to a separate file.

* export: Omit genes with no amino acid mutations.

* validate: Allow underscores in gene names.

* refine: Remove unused --nthreads argument.

* ancestral, filter, tree, refine: Exit 1 instead of -1 on error.

* Print the help message, instead of throwing an exception, when `augur` is run
  without arguments.

## Documentation

* Briefly describe each command in its `--help` output and in the global `augur
  --help` output.

* Revamp README to emphasize new, modular augur and make it suitable for
  inclusion on PyPi.

* Reconciled conflicting license declarations; augur is AGPLv3 (not MIT)
  licensed like the rest of Nextstrain.

* Include URLs for bug reports, the change log, and the source on PyPi.

## Data

* Geographic coordinates added for the Netherlands and the Philippines.

## Development

* Reset the `release` branch when rewinding a failed local release process.

* Refactor the augur program and command architecture for improved
  maintainability.


# 3.0.0.dev3 (4 September 2018)

## Development

* Use an allowed Topic classifier so we can upload to PyPi

* Ignore distribution egg-info build files


# 3.0.0.dev2 (4 September 2018)

## Features

* Export: Add safety checks for optional annotations and geo data

* Include more lat/longs in the default geo data

## Development

* Add release tooling

* Document the release process and a few development practices

* Travis CI: Switch to rebuilding the Docker image only for new releases

* Remove ebola, lassa, tb, WNV, and zika builds now in their own repos.  These
  builds are now available at URLs like <https://github.com/nextstrain/ebola>,
  for example.


# 3.0.0.dev1 (unreleased)

## Development

* Start versioning augur beginning with 3.0.0.  A new `augur version` command
  reports the running version.
