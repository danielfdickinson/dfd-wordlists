# Daniel's word lists

Daniel's word lists for [https://cspell.org] custom dictionaries.

## Currently includes

* [Technology (especially computing) words Daniel needs CSpell to recognize (words-tech.txt)](words-tech.txt)
* [Miscellaneous words Daniel needs CSpell to recognize (words-dfd.txt)](words-dfd.txt)

## Using with CSpell

In your `cspell.json` configuration file include something like the following:

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
repository (project) and exists in the root of that repository.

--------

Copyright © 2022 Daniel F. Dickinson

Except where otherwise noted, this repository is licensed under the Creative
Commons Attribution Share-Alike 4.0 International license.

See [LICENSE](LICENSE) in this repository.
