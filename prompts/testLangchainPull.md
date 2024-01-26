---
promptId: testLangchainPull
name: Test Langchain Pull
description: test Langchain Pull
commands:
  - generate
disableProvider: true
type: wrapper
---

This is running the text generation with `gitmaxd/onboard-email` template,
the json you see in there, is from their example.
```handlebars
{{#run "simpleGen"}}
	{{#runLang "rlm/text-to-sql"}}
		{
			"input": "{{escp2 tg_selection}}"
		}
	{{/runLang}}
{{/run}}
```

***
***
# Output:
This is the output of {{name}} template.
## testing run lang:
	this is the result of the generate template, from the previews shown json. 


{{get "simpleGen"}}


