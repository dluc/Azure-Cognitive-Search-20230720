# Bringing Memory to your AI Apps with Azure Cognitive Search! | Intro to Semantic Kernel

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/4bvnDf0F6yk/0.jpg)](https://www.youtube.com/watch?v=4bvnDf0F6yk)

# Python Setup

Recommended: [Python 3.8+](https://github.com/pyenv/pyenv)

# .NET Setup

Recommended: [.NET 7+](https://dotnet.microsoft.com/download/dotnet)

[VS Code](https://code.visualstudio.com/download) +
[Polyglot extension](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.dotnet-interactive-vscode)

# Sneak peek

## Python

Packages:

* semantic-kernel 0.3.4.dev0

```python
kernel.import_skill(TextMemorySkill())

sk_prompt = """
Considering these facts

About me: {{recall 'where did I grow up?'}}
About me: {{recall 'where do I live?'}}

Question: {{$input}}

Provide a concise answer ('Answer: ') and a separate explanation ('Explanation: '), in two lines.
"""

sk_function = kernel.create_semantic_function(prompt_template=sk_prompt, max_tokens=200)
```
```python
context= kernel.create_new_context()
context[TextMemorySkill.COLLECTION_PARAM] = "aboutMeUser002";

result = await sk_function.invoke_async(input="Do I live in the same town where I grew up?", context=context)
print(result)
```
```
Answer: No.
Explanation: The fact that the family is from New York and the person has been living in Seattle since 2005 suggests that they did not grow up in Seattle.
```

## C#

Nugets:

* Microsoft.SemanticKernel, 0.18.230725.3-preview
* Microsoft.SemanticKernel.Connectors.Memory.AzureCognitiveSearch, 0.18.230725.3-preview

```csharp
kernel.ImportSkill(new TextMemorySkill(kernel.Memory));

const string skPrompt = @"
Considering these facts

About me: {{recall 'where did I grow up?'}}
About me: {{recall 'where do I live?'}}

Question: {{$input}}

Provide a concise answer ('Answer: ') and a separate explanation ('Explanation: '), in two lines.
";

var skFunction = kernel.CreateSemanticFunction(skPrompt, maxTokens: 200);
```
```csharp
var context = kernel.CreateNewContext();
context[TextMemorySkill.CollectionParam] = "aboutMeUser001";

var result = await skFunction.InvokeAsync("Do I live in the same town where I grew up?", context);
Console.WriteLine(result);
```
```
Answer: No.
Explanation: The fact that the family is from New York and the person has been living in Seattle since 2005 suggests that they did not grow up in Seattle.
```
