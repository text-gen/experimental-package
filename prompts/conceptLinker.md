---
promptId: conceptLinker
name: 🗞️conceptLinker
description: Generate notes and links them from the current note's words
author: Noureddine
tags:
  - notes
  - linking
  - brainStorming
version: 0.0.1
disableProvider: true
commands:
  - generate
---
```handlebars
```
***
***
{{#script}}
```js
    // Uses an external function 'gen' to generate concepts and their definitions
    async function extractAndDefineConcepts(text) {
        const prompt = `Extract concepts from the following content and define them. Do not refer to the current note. do not refer to already refered concepts(contained in []). Return a json Record<name, definition>. Ensure the 'name' is exactly as it appears in the text, without any modifications: \n${text.replace(/\[\[.*?\]\]/g, '')}`;
        
        const conceptData = await genJSON(prompt); // returns object

        return Object.entries(conceptData).map(([name, definition]) => ({name, definition}));
    }
    
    function replaceConceptsWithLinks(text, concepts) {
        let modifiedText = text;
        concepts.forEach(concept => {
            modifiedText = modifiedText.replace(new RegExp(concept.name, 'g'), `[[${concept.name}]]`);
        });
        return modifiedText;
    }
     
    async function createConceptPages(concepts) {
        const currentFolder = app.workspace.getActiveFile().parent.path;
        for (const concept of concepts) {
            const conceptFilePath = `${currentFolder}/${concept.name}.md`;
            if (!await app.vault.exists(conceptFilePath)) {
                await app.vault.create(conceptFilePath, `# ${concept.name}\n\n${concept.definition}`);
            }
        }
    }

    async function extractConcepts() {
            const activeFile = app.workspace.getActiveFile();
            if (!activeFile) return;

            const fileContent = (""+await app.vault.read(activeFile))
            
            const concepts = await extractAndDefineConcepts(fileContent);

            const modifiedContent = replaceConceptsWithLinks(fileContent, concepts);
            console.log({modifiedContent})
            await app.vault.modify(activeFile, modifiedContent);

            await createConceptPages(concepts);
        }

 await extractConcepts();
 return "";
```
{{/script}}