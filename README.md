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

### Configure

#### Basic

##### Using the word lists served from GitHub

In your `tests/config/cspell.json` configuration file include something like
the following:

``` json
"dictionaries": [
	"dfd-words",
	"tech-words",
	"project-words"
],
"dictionaryDefinitions": [
	{
		"addWords": true,
		"name": "project-words",
		"path": "./words-project.txt"
	},
	{
		"addWords": true,
		"name": "tech-words",
		"path": "https://raw.githubusercontent.com/danielfdickinson/dfd-wordlists/main/words-tech.txt"
	},
	{
		"addWords": true,
		"name": "dfd-words",
		"path": "https://raw.githubusercontent.com/danielfdickinson/dfd-wordlists/main/words-dfd.txt"
	}
],
"ignorePaths": [
	"node_modules",
	"/project-words.txt"
]
```

Where `words-project.txt` is a file containing words specific to the
repository (project) and exists in `tests/config/` directory.

##### Using a Git submodule

Add the word lists as a submodule under tests/config by executing the
following from the root of your repository.

``` bash
git submodule add --name dfd-wordlists -- https://github.com/danielfdickinson/dfd-wordlists tests/config/dfd-wordlists
```

And, in your `tests/config/cspell.json` configuration file include something
like the following:

``` json
"dictionaries": [
	"dfd-words",
	"tech-words",
	"project-words"
],
"dictionaryDefinitions": [
	{
		"addWords": true,
		"name": "project-words",
		"path": "./words-project.txt"
	},
	{
		"addWords": true,
		"name": "tech-words",
		"path": "./dfd-wordlists/words-tech.txt"
	},
	{
		"addWords": true,
		"name": "dfd-words",
		"path": "./dfd-wordlists/main/words-dfd.txt"
	}
],
"ignorePaths": [
	"node_modules",
	"tests/config/words-*.txt"
]
```

Where `words-project.txt` is a file containing words specific to the
repository (project) and exists in `tests/config/` directory.

#### Overriding default dictionaries

Starting with a configuration such as the following (which includes disabled
french dictionaries):

``` json
{
	"$schema": "https://raw.githubusercontent.com/streetsidesoftware/cspell/main/cspell.schema.json",
	"allowCompoundWords": false,
	"dictionaries": [
		"dfd-words",
		"tech-words",
		"project-words",
		"!dfd-words-fr",
		"!project-words-fr"
	],
	"dictionaryDefinitions": [
		{
			"addWords": true,
			"name": "project-words",
			"path": "./words-project.txt"
		},
		{
			"addWords": true,
			"locale": "fr_CA",
			"name": "project-words-fr",
			"path": ".words-fr-project.txt"
		},
		{
			"addWords": true,
			"name": "tech-words",
			"path": "../../words-tech.txt"
		},
		{
			"addWords": true,
			"name": "dfd-words",
			"path": "../../words-dfd.txt"
		},
		{
			"addWords": true,
			"name": "dfd-words-fr",
			"path": "../../words-fr-dfd.txt"
		}
	],
	"ignorePaths": [
		"node_modules",
		"**/tests/config/words-*.txt",
		"**/words-*.txt"
	],
	"ignoreWords": [],
	"version": "0.2"
}
```

You can override the disabling of the french dictionary for certain paths,
using an override section like the following:

``` json
	"overrides": [
		{
			"dictionaries": [
				"!dfd-words",
				"!tech-words",
				"!project-words",
				"!!dfd-words-fr"
				"!!project-words-fr"
			],
			"filename": "**/exampleSite/**/fr/**/*.md",
			"language": "fr_CA"
		},
		{
			"dictionaries": [
				"!!dfd-words-fr",
				"!!project-words-fr"
			],
			"filename": "**/{i18n/fr.toml,config.toml}",
			"language": "*"
		}
	]
```

The first example uses only the french dictionaries and the second example uses
all the dictionaries from the config sample.

A single bang (`!`) disables a dictionary, a double-bang (`!!`) re-enables a
disabled dictionary. You can even re-disable with a triple bang (`!!!`) but that
gets confusing in my opinion.

Of course the [CSpell dictionary
documentation](https://cspell.org/docs/dictionaries/) is the canonical place to
go for details.

##### Remote dictionaries overrides

We don't repeat the docs for remote dictionaries, since the only change is that
instead of using a local path (e.g. `../../words-fr-dfd.txt`), as with the Basic
configuration, one uses a URL (e.g.
`https://raw.githubusercontent.com/danielfdickinson/dfd-wordlists/main/words-fr-dfd.txt`)

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
[dfdtemplate]: https://github.com/danielfdickinson/dfd-template
[precommit]: https://pre-commit.com
