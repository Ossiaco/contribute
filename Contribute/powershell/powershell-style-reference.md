---
title: Specific guidance for writing cmdlet reference
description: This article provides specific rules for formatting PowerShell code samples. This applies to conceptual articles with examples, as well as cmdlet reference.
ms.topic: contributor-guide
ms.prod: non-product-specific
ms.custom: external-contributor-guide
author: sdwheeler
ms.author: sewhee
ms.date: 10/09/2019
---
# Updating reference articles

Cmdlet reference articles have a specific structure. This structure is defined by [PlatyPS][].
PlatyPS is the tool we use to generate cmdlet help for PowerShell modules. PlatyPS creates the base
Markdown file for a cmdlet. After editing the Markdown files, PlatyPS is used create the MAML help
files used by the `Get-Help` cmdlet.

PlatyPS has a hard-coded schema for cmdlet reference that is written into the code. The
[platyPS.schema.md][] document attempts to describe this structure. Schema violations cause build
errors that must be fixed before we can accept your contribution.

## General guidelines

- Do not remove any of the header structures. PlatyPS expects a specific set of headers.
- The **Input type** and **Output type** headers must have a type. If the cmdlet does not take input
  or return a value then use the value "None".
- Fenced code blocks are only allowed in the [Examples](#format-for-examples) section.
- Inline code spans can be used in any paragraph.

## Formatting About_ files

`About_*` files are now processed by [Pandoc][], instead of PlatyPS. `About_*` files are formatted
for the best compatibility across with all versions of PowerShell and with the publishing tools.
Please do not alter the formatting of `about_*` files without checking in with a repository
maintainer.

Basic formatting guidelines:

- Limit lines to 80 characters
- Code blocks, block quotes, and tables are limited to 76 characters because Pandoc indents these by
  four spaces during conversion
- Tables need fit within 76 characters
  - Manually wrap contents of cells across multiple lines
  - Use opening and closing `|` characters on each line
  - See a working example in [about_Comparison_Operators][about-example]
- When using Pandoc's special characters `\`,`$`,`` ` ``, and `<`
  - Within a header - these characters must be escaped using a leading `\` character
  - Within a paragraph - these characters should be put into code spans. For example:

    ~~~markdown
    ### The purpose of the \$foo variable

    The `$foo` variable is used to store ...
    ~~~

## Format for examples

In the PlatyPS schema, the **EXAMPLES** header is an H2 header and each example is an H3 header.

Within an example, the schema does not allow code blocks to be separated by paragraphs. The valid
schema is:

```
### Example #X title

0 or more paragraphs
1 or more code blocks
0 or more paragraphs.
```

Number each example and add a brief title.

For example:

~~~markdown
### Example 1: Get cmdlets, functions, and aliases

This example gets the PowerShell cmdlets, functions, and aliases that are installed on the
computer.

```powershell
Get-Command
```
~~~


[PlatyPS]: https://github.com/powershell/platyps
[platyPS.schema.md]: https://github.com/PowerShell/platyPS/blob/master/platyPS.schema.md
[issue1806]: https://github.com/PowerShell/PowerShell-Docs/issues/1806
[about-example]: https://github.com/MicrosoftDocs/PowerShell-Docs/blob/staging/reference/6/Ossiaco.PowerShell.Core/About/about_Comparison_Operators.md
[Pandoc]: https://pandoc.org