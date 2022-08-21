# Using the word lists served from GitHub

In your `tests/config/cspell.json` configuration file include something like
the following:

``` json
{
	"$schema": "https://raw.githubusercontent.com/streetsidesoftware/cspell/main/cspell.schema.json",
	"allowCompoundWords": false,
	"dictionaryDefinitions": [
		{
			"addWords": true,
			"language": "en,en-ca,en-gb",
			"name": "project-words",
			"path": "./tests/config/words-project.txt"
		},
		{
			"addWords": true,
			"language": "en,en-ca,en-gb",
			"name": "tech-words",
			"path": "https://raw.githubusercontent.com/danielfdickinson/dfd-wordlists/main/words-tech.txt"
		},
		{
			"addWords": true,
			"language": "en,en-ca,en-gb",
			"name": "dfd-words",
			"path": "https://raw.githubusercontent.com/danielfdickinson/dfd-wordlists/main/words-dfd.txt"
		},
		{
			"addWords": true,
			"language": "fr,fr-ca,fr-90",
			"name": "dfd-words-fr",
			"path": "https://raw.githubusercontent.com/danielfdickinson/dfd-wordlists/main/words-fr-dfd.txt"
		}
	],
	"globRoot": "../..",
	"ignorePaths": [
		"node_modules",
		"./tests/config/words-*.txt",
	],
	"ignoreWords": [],
	"version": "0.2"
}
```

Where `words-project.txt` is a file containing words specific to the
repository (project) and exists in `tests/config/` directory.
