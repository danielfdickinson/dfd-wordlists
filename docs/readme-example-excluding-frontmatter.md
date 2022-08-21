# Example of excluding frontmatter

<!--- cspell:ignore reforme htmlvalidate --->

In another repo, with `dfd-wordlists` as a git submodule as
`tests/config/dfd-wordlists`

Add a `tests/config/cspell.json`:

```json
{
	"$schema": "https://raw.githubusercontent.com/streetsidesoftware/cspell/main/cspell.schema.json",
	"allowCompoundWords": false,
	"dictionaries": [
		"project-words",
		"project-words-fr",
		"hugo-words",
		"tech-words",
		"dfd-words",
		"dfd-words-fr"
	]
	"dictionaryDefinitions": [
		{
			"addWords": true,
			"locale": "en,en-ca",
			"name": "project-words",
			"path": "./tests/config/words-project.txt"
		},
		{
			"addWords": true,
			"locale": "fr,fr-ca",
			"name": "project-words-fr",
			"path": "./tests/config/words-fr-project.txt"
		},
		{
			"addWords": true,
			"locale": "en,en-ca",
			"languageId": "hugo",
			"name": "hugo-words",
			"path": "./tests/config/dfd-wordlists/words-hugo.txt"
		},
		{
			"addWords": true,
			"locale": "en,en-ca",
			"name": "tech-words",
			"path": "./test/config/dfd-wordlists/words-tech.txt"
		},
		{
			"addWords": true,
			"locale": "en,en-ca",
			"name": "dfd-words",
			"path": "./tests/config/dfd-wordlists/words-dfd.txt"
		},
		{
			"addWords": true,
			"locale": "fr,fr-ca",
			"name": "project-words-fr",
			"path": "./tests/config/dfd-wordlists/words-fr-dfd.txt"
		}
	],
	"globRoot": "../..",
	"ignorePaths": [
		"./go.{mod,sum}",
		"./exampleSite/go.{mod,sum}",
		"./tests/config/cspell.json",
		"./tests/config/words-*.txt",
		"./tests/config/dfd-wordlists/**"
	],
	"ignoreRegExpList": [],
	"ignoreWords": [],
	"import": [
		"@cspell/dict-fr-fr/cspell-ext.json",
		"@cspell/dict-fr-reforme/cspell-ext.json"
	],
	"language": "en,en-gb,en-us",
	"overrides": [
		{
			"filename": [
				"./exampleSite/**/fr/**/*.md"
			],
			"ignoreRegExpList": [
				"frontMatter"
			],
			"language": "fr"
		},
		{
			"filename": [
				"./exampleSite/**/fr/**/*.md"
			],
			"includeRegExpList": [
				"frontMatter"
			],
			"language": "en,fr"
		},
		{
			"dictionaries": [
				"css",
				"html",
				"project-words",
				"tech-words"
			],
			"filename": [
				"./tests/config-action/htmlvalidate*.json"
			]
		},
		{
			"dictionaries": [
				"companies",
				"dfd-words",
				"project-words",
				"tech-words"
			],
			"filename": [
				"./config.toml",
				"./theme.toml",
				"./i18n/fr.toml",
				"./exampleSite/config.toml",
				"./.github/**/*.yml",
				"./.pre-commit-config.yaml"
			],
			"language": "en,en-gb,fr,fr-90"
		},
		{
			"dictionaries": [
				"dfd-words",
				"project-words",
				"tech-words"
			],
			"filename": [
				"./archetypes/*",
				"./layouts/**/*.html",
				"./README.md",
				"./docs/*.md"
			]
		},
		{
			"dictionaries": [
				"dfd-words",
				"project-words",
				"tech-words"
			],
			"filename": [
				"./content/en/**/*.md",
				"./content/en/**/*.html"
			],
			"includeRegExpList": [
				"frontMatter"
			]
		}
	],
	"patterns": [
		{
			"name": "frontMatter",
			"pattern": "/^(-{3}|[+]{3})$(\\s|\\S)*?^\\1$/gm"
		}
	],
	"version": "0.2"
}
```
