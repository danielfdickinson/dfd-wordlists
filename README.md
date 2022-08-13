# Daniel's word lists

Daniel's word lists for [https://cspell.org](https://cspell.org) custom
dictionaries.

## Status

[![pre-commit.ci
status](https://results.pre-commit.ci/badge/github/danielfdickinson/dfd-wordlists/main.svg)](https://results.pre-commit.ci/latest/github/danielfdickinson/dfd-wordlists/main)

## Currently includes

* [Technology (especially computing) words Daniel needs CSpell to recognize
(words-tech.txt)](words-tech.txt)
* [Miscellaneous words Daniel needs CSpell to recognize
(words-dfd.txt)](words-dfd.txt)

## Using with CSpell

### Using the word lists served from GitHub

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

### Using a Git submodule

1. Add the wordlists as a submodule under tests/config by executing the
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

## Executing CSpell

Use `cspell --config tests/config/cspell.json …` (that is with any additional
command line parameters) from the root of your project.

--------

Copyright © 2022 Daniel F. Dickinson

Except where otherwise noted, this repository is licensed under the Creative
Commons Attribution Share-Alike 4.0 International license.

See [LICENSE](LICENSE) in this repository.
