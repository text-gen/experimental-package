---
promptId: summary
name: summary
author: Noureddine
title: Summarizes Text
description: Summarizes Big chunk of text into a sentence
mode: insert
chain.type: map_reduce
splitter.chunkSize: 1000
splitter.chunkOverlap: 100
max_tokens: 1000
temperature: 0
chain.maxTokens: 1000
---
{{tg_selection}}
***
{{output}}