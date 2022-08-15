# Daniel's word lists

Daniel's word lists for [CSpell][cspell] custom dictionaries.

## Status

[![pre-commit.ci
status](https://results.pre-commit.ci/badge/github/danielfdickinson/dfd-wordlists/main.svg)](https://results.pre-commit.ci/latest/github/danielfdickinson/dfd-wordlists/main)

## Currently includes

* [Technology (especially computing) words Daniel needs CSpell to recognize
(words-tech.txt)](words-tech.txt)
* [Miscellaneous words Daniel needs CSpell to recognize
(words-dfd.txt)](words-dfd.txt)
* [Miscellaneous french words Daniel needs CSpell to recognize
(words-fr-dfd.txt)](words-fr-dfd.txt)

## Using with CSpell

### Basic

#### Using the word lists served from GitHub

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

#### Using a Git submodule

1. Add the word lists as a submodule under tests/config by executing the
	following from the root of your repository.

	``` bash
	git submodule add --name dfd-wordlists -- https://github.com/danielfdickinson/dfd-wordlists tests/config/dfd-wordlists
	```

2. And, in your `tests/config/cspell.json` configuration file include something
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

### Overriding default dictionaries

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

## Executing CSpell

Use `cspell --config tests/config/cspell.json …` (that is, with any additional
command line parameters, not literally `…`) from the root of your project.

## Copyright and licensing

Copyright © 2022 Daniel F. Dickinson

### Textual and media content

Except where otherwise noted, textual and media components in this repository
are licensed under the Creative Commons Attribution Share-Alike 4.0
International license. (Basically a 'share it forward' license).

See [LICENSE-TEXT-MEDIA](LICENSE-TEXT-MEDIA) in this repository for
that license.

### Code and configuration

Except where otherwise noted, and where applicable _([Note 2](#note-2))_, code
and configurations in this repository are licensed under an MIT license.

See [LICENSE-CODE-AND-CONFIGS](LICENSE-CODE-AND-CONFIGS) in this repository for
that license.

### Acknowledgements

Thank you to '@davidsneighbour' for introducing me to
[pre-commit](https://pre-commit.com) and whose configurations I have gleefully
extended (for example adding [CSpell][cspell] for spell checking).

Thank you to '@brycewray' for writing an excellent [article on the
accessibility argument for tabs vs spaces in code][tabaccess]. Hopefully I
haven't taken that _too_ far (_[Note 1](#note-1)_).

-------

## Notes

### Note 1

Uses EditorConfig for an editor neutral default styling

* Defaults to [using tabs where possible for accessibility
reasons][tabaccess]
* `root = false` so that the user can set their preferred (or required for
accessibility reasons) rendering of the tabs via a `.editorconfig` file in
a higher level directory, or their home directory. Not doing this defeats
the purpose of using tabs vs. spaces.
* `tab_width` is **not** set in this repository so that the user's config
will be used. (See above).

### Note 2

Configurations are not particularly copyrightable anyway, nor do I particularly
want to, but this makes it clear you can use them on an "AS-IS" basis (i.e.
please don't sue me if they break or cause breakage).

[cspell]: https://cspell.org
[tabaccess]: https://www.brycewray.com/posts/2022/06/accessibility-argument-tabs-spaces/
