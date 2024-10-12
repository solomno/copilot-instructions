# copilot-instructions
Copilot instructions to match code style
Inspired by https://github.com/fielding/copilot-instructions

## How to

1. Clone the repository
2. in vscode, set the following in settings.json
```json
  "github.copilot.chat.experimental.codeGeneration.instructions" : [
    {
      "file": "/path/to/rootfolder/copilot-instructions/profiles/default/copilot-codegeneration.md"
    }
  ],
  "github.copilot.chat.experimental.codeFeedback.instructions": [
    {
      "file": "/path/to/rootfolder/copilot-instructions/profiles/default/copilot-codefeedback.md"
    }
  ],
  "github.copilot.chat.experimental.testGeneration.instructions": [
    {
      "file": "/path/to/rootfolder/copilot-instructions/profiles/default/copilot-testgeneration.md"
    }
  ],
```
3. Copy the content which is relevant for you to use from the language folder to the defult profile file(s)
 - cat ./instructions/language/terraform/type/codegeneration/rules.md >> ./profiles/default/copilot-codegeneration.md