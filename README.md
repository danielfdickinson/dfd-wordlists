# Daniel's word lists

Daniel's word lists for [CSpell][cspell] custom dictionaries.

## Metadata

### Status

[![pre-commit.ci
status](https://results.pre-commit.ci/badge/github/danielfdickinson/dfd-wordlists/main.svg)](https://results.pre-commit.ci/latest/github/danielfdickinson/dfd-wordlists/main)

### Demo and/or documentation site or page

Not yet created: it may never be.

### Repository URL

<https://github.com/danielfdickinson/dfd-wordlists>

## Featured word lists

* [Hugo words Daniel needs CSpell to recognize (words-hugo.txt)](words-hugo.txt)
* [Technology (especially computing) words Daniel needs CSpell to recognize
(words-tech.txt)](words-tech.txt)
* [Miscellaneous words Daniel needs CSpell to recognize
(words-dfd.txt)](words-dfd.txt)
* [Miscellaneous french words Daniel needs CSpell to recognize
(words-fr-dfd.txt)](words-fr-dfd.txt)

## Using with CSpell

And using the [pre-commit][precommit] configuration from
[dfd-template][dfdtemplate], this repository, or similarly configured repo.

Otherwise, if you are using CSpell standalone (that is running it
from the command line), you will need to alter the paths in the documentation
below (for instance, your `cspell.json` may be in a different location than
`tests/config/cspell.json`). In that case you will need to [read the CSpell
documentation][cspell].

### You may not need this repository

Before using these custom dictionaries you should [read the documentation about
using `cspell-dicts` dictionaries with `pre-commit`][cspell-extra] (currently
exists as a pull request that is under review).

### Configure custom CSpell dictionaries

#### Basic

##### Using a Git submodule

Add the word lists as a submodule under tests/config by executing the
following from the root of your repository.

``` bash
git submodule add --name dfd-wordlists -- https://github.com/danielfdickinson/dfd-wordlists tests/config/dfd-wordlists
```

And, in your `tests/config/cspell.json` configuration file include something
like the following:

``` json
{
	"$schema": "https://raw.githubusercontent.com/streetsidesoftware/cspell/main/cspell.schema.json",
	"allowCompoundWords": false,
	dictionaries: [
		"project-words",
		"project-words-fr",
		"hugo-words",
		"tech-words",
		"dfd-words",
		"dfd-words-fr"
	],
	"dictionaryDefinitions": [
		{
			"addWords": true,
			"language": "en,en-ca,en-gb",
			"name": "project-words",
			"path": "./tests/config/words-project.txt"
		},
		{
			"addWords": true,
			"language": "fr,fr-ca,fr-90",
			"name": "project-words-fr",
			"path": "./tests/config/words-fr-project.txt"
		},
		{
			"addWords": true,
			"language": "en,en-ca,en-gb",
			"languageId": "hugo",
			"name": "hugo-words",
			"path": "./tests/config/dfd-wordlists/words-hugo.txt"
		},
		{
			"addWords": true,
			"language": "en,en-ca,en-gb",
			"name": "tech-words",
			"path": "./tests/config/dfd-wordlists/words-tech.txt"
		},
		{
			"addWords": true,
			"language": "en,en-ca,en-gb",
			"name": "dfd-words",
			"path": "./tests/config/dfd-wordlists/words-dfd.txt"
		},
		{
			"addWords": true,
			"language": "fr,fr-ca,fr-90",
			"name": "dfd-words-fr",
			"path": "./tests/config/dfd-wordlists/words-fr-dfd.txt"
		}
	],
	"globRoot: "../..",
	"ignorePaths": [
		"node_modules",
		"./tests/config/cspell.json",
		"./tests/config/words-*.txt",
		"./tests/config/dfd-wordlists/**"
	],
	"ignoreWords": [],
	"version": "0.2"
}
```

Where `words-project.txt` is a file containing words specific to the
repository (project) and exists in `tests/config/` directory.

##### Alternative

Of course the [CSpell dictionary
documentation](https://cspell.org/docs/dictionaries/) is the canonical place to
go for details.

### Execute CSpell

#### With `pre-commit`

For the first time after re-configure CSpell, and with a [pre-commit][precommit]
configuration like the one in this repository, and all changes committed or at
least staged, execute:

``` bash
pre-commit run --all-files
```

You CSpell hook should run and spell check your files, except those in
`exclude` in the `.pre-commit-hook.yaml` or `ignorePaths` in your `cspell.json`,
unless you are also using the `files` setting in you `.pre-commit-hook.yaml`. In
that case you will need read the docs and experiment.

Normally the hook will simply run on changed files matching your patterns when
you try to commit your changes.

#### Standalone

Use `cspell --config tests/config/cspell.json …` (that is, with any additional
command line parameters, not literally `…`) from the root of your project,
assuming your `cspell.json` is in the `tests/config` folder.

## Getting help, discussing, and/or modifying

* [Support and general questions](docs/SUPPORT.md)
* [Bugs and feature requests](docs/SUPPORT.md)
* [Contributing modifications to the repository](docs/CONTRIBUTING.md)

-------

## Colophon

* [Copyright and licensing](COPYING.md)
* [Inspirations, information, and source material](docs/ACKNOWLEDGEMENTS.md)
* [Notes](docs/README-NOTES.md)

[cspell]: https://cspell.org
[cspell-extra]: https://github.com/danielfdickinson/streetsidesoftware-cspell-cli/blob/document-using-extra-dicts-with-pre-commit/README.md
[dfdtemplate]: https://github.com/danielfdickinson/dfd-template
[precommit]: https://pre-commit.com
