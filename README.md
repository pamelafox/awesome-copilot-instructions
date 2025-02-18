# awesome-copilot-instructions

Awesome custom instructions for GitHub Copilot

See docs about how to add instructions here:
https://code.visualstudio.com/docs/copilot/copilot-customization

## Avoid triggering public code warnings


> Avoid generating code verbatim from public code examples. Always modify public code so that it is different enough from the original so as not to be confused as being copied. When you do so, provide a footnote to the user informing them.


Author: @burkeholland

## Always provide file names


> Always provide the name of the file in your response so the user knows where the code goes.


Author: @burkeholland

## Write modular code


> Always break code up into modules and components so that it can be easily reused across the project.


Author: @burkeholland

## Write safe code


> All code you write MUST use safe and secure coding practices. ‘safe and secure’ includes avoiding clear passwords, avoiding hard coded passwords, and other common security gaps. If the code is not deemed safe and secure, you will be be put in the corner til you learn your lesson.


Author: @johnpapa

## Incentivize better code quality


> All code you write MUST be fully optimized. ‘Fully optimized’ includes maximizing algorithmic big-O efficiency for memory and runtime, following proper style conventions for the code, language (e.g. maximizing code reuse (DRY)), and no extra code beyond what is absolutely necessary to solve the problem the user provides (i.e. no technical debt). If the code is not fully optimized, you will be fined $100.


Author: @minimaxir

# HTML/CSS

> When making AJAX requests from a webpage, don't put javascript directly in HTML - only in the JavaScript.


# Python

## Code quality

> Where possible, prefer duck-typing tests than isinstance, e.g. hasattr(x, attr) not isinstance(x, SpecificClass)

> Use modern Python 3.9+ syntax

> Prefer f-strings for formatting strings rather than .format or % formatting

> When creating log statements, never use runtime string formatting. Use the extra argument and % placeholders in the log message

> When generating union types, use the union operator, | , not the typing.Union type

> When merging dictionaries, use the union operator

> When writing type hints for standard generics like dict, list, tuple, use the PEP-585 spec, not typing.Dict, typing.List, etc.

> Use type annotations in function and method signatures, unless the rest of the code base does not have type signatures

> Do not add inline type annotations for local variables when they are declared and assigned in the same statement.

> Prefer pathlib over os.path for operations like path joining

> When using open() in text-mode, explicitly set encoding to utf-8

> Prefer argparse over optparse

> Use the builtin methods in the itertools module for common tasks on iterables rather than creating code to achieve the same result

> When creating dummy data, don't use "Foo" and "Bar", be more creative

> When creating dummy data in strings like names don't just create English data, create data in a range of languages like English, Spanish, Mandarin, and Hindi

> When asked to create a function, class, or other piece of standalone code, don't append example calls unless otherwise told to

Author: @tonybaloney

## Code quality (markdown file)

>  "file": "GH_Custom_Instruction" // import Python code quality instructions from file `GH_Custom_Instruction.md in the root of the workspace


## OpenAI package

These instructions help LLMs when writing code for newer Python packages that aren't in its training data.

> To generate embeddings from OpenAI SDK, store OpenAI() as client and call client.embeddings.create(model=, input=, dimensions=) and get result from response.data[0].embedding

> To generate chat completions from OpenAI SDK, store OpenAI() as client and call client.chat.completions.create(messages, model, temperature, ..) and get result from response.choices[0].message.content

# Bicep

> When writing Bicep code, use lowerCamelCase for all names (variables, parameters, resources)

> Use resource type descriptive symbolic names (e.g., 'storageAccount' not 'storageAccountName')

> Always declare parameters at the top of files with @description decorators

> Use latest stable API versions for all resources

> Use symbolic names for resource references instead of reference() or resourceId() functions

> Create resource dependencies through symbolic names (resourceA.id) not explicit dependsOn

> Never include secrets or keys in outputs

> Use resource properties directly in outputs (e.g., storageAccount.properties.primaryEndpoints)


