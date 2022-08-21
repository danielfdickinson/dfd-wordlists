# An example configuration for using French dictionaries

<!--- cspell:ignore reforme --->

In your `pre-commit-config.yaml`, use a section like:

```yaml
  - repo: "https://github.com/streetsidesoftware/cspell-cli"
    rev: v6.5.0
    hooks:
      - id: cspell
        additional_dependencies:
          - "@cspell/dict-fr-fr"
          - "@cspell/dict-fr-reforme"
        args:
          - "--config"
          - "tests/config/cspell.json"
          - "--no-must-find-files"
        exclude: ^(LICENSE$|tests/config/cspell.json) # yamllint disable-line
```

And in `tests/config/cspell.json`:

```json
{
	"$schema": "https://raw.githubusercontent.com/streetsidesoftware/cspell/main/cspell.schema.json",
	"allowCompoundWords": false,
	"import": [
		"@cspell/dict-fr-fr/cspell-ext.json",
		"@cspell/dict-fr-reforme/cspell-ext.json"
	],
	"globRoot": "../..",
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
