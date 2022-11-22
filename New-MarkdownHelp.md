---
external help file: -help.xml
Module Name:
online version:
schema: 2.0.0
---

# Get-MarkdownHelp.ps1

## SYNOPSIS
Creates a markdown Readme string from the comment based help of a command

## SYNTAX

```
Get-MarkdownHelp.ps1 [-CommandName] <String> [[-PSCodePattern] <String>] [[-AlternateEOL] <String>]
 [<CommonParameters>]
```

## DESCRIPTION
The \[Get-MarkdownHelp\]\[1\] cmdlet retrieves the \[comment-based help\]\[2\] and converts it to a Markdown page
similar to the general online PowerShell help pages (as e.g.
\[Get-Content\]).\
Note that this cmdlet *doesn't* support \`XML\`-based help files, but has a few extra features for the comment-based
help as opposed to the native \[platyPS\]\[3\] \[New-MarkdownHelp\]:

* **Code Blocks**\
To create code blocks, indent every line of the block by at least four spaces or one tab relative the **text indent**.
The **text indent** is defined by the smallest indent of the current - and the \`.SYNOPSIS\` section.\
Code blocks are automatically \[fenced\]\[4\] for default PowerShell color coding.\
The usual comment-based help prefix for code (\`PS.
\\\>\`) might also be used to define a code lines.
For more details, see the \[-PSCodePattern parameter\].

* **Titled Examples**\
Examples can be titled by adding an (extra) hash (\`#\`) in front of the first line in the section.
This line will be removed from the section and added to the header of the example.

* **Links**\
\> As Per markdown definititon, The first part of a \[reference-style link\]\[5\] is formatted with two sets of brackets.
\> The first set of brackets surrounds the text that should appear linked.
The second set of brackets displays
\> a label used to point to the link you're storing elsewhere in your document, e.g.: \`\[rabbit-hole\]\[1\]\`.
\> The second part of a reference-style link is formatted with the following attributes:
\> * The label, in brackets, followed immediately by a colon and at least one space (e.g., \`\[label\]:\` ).
\> * The URL for the link, which you can optionally enclose in angle brackets.
\> * The optional title for the link, which you can enclose in double quotes, single quotes, or parentheses.

For the comment-base help implementation, the second part should be placed in the \`.LINK\` section to automatically
listed in the end of the document.
The reference will be hidden if the label is an explicit empty string(\`""\`).

* **Quick Links**\
Any phrase existing of a combination alphanumeric characters, spaces, underscores and dashes between squared brackets
(e.g.
\`\[my link\]\`) will be linked to the (automatic) anchor id in the document, e.g.: \`\[my link\](#my-link)\`.

\> **Note:** There is no confirmation if the internal anchor really exists.

* **Parameter Links**\
**Parameter links** are similar to **Quick Links** but start with a dash and contain an existing parameter name possibly
followed by the word "parameter".
E.g.: \`\[-AlternateEOL\]\` or \`\[-AlternateEOL parameter\]\`.
In this example, the parameter link will refer to the internal \[-AlternateEOL parameter\].

* **Cmdlet Links**\
**Cmdlet links** are simular to **Quick Links** but contain a cmdlet name where the online help is known.
E.g.: \`\[Get-Content\]\`.
In this example, the cmdlet link will refer to the online help of the related \[Get-Content\] cmdlet.

## EXAMPLES

### EXAMPLE 1
```
# Display markdown help
This example generates a markdown format help page from itself and shows it in the default browser
```

.\Get-MarkdownHelp.ps1 .\Show-MarkDown.ps1 |Out-String |Show-Markdown -UseBrowser

### EXAMPLE 2
```
# Copy markdown help to a website
This command creates a markdown readme string for the `Join-Object` cmdlet and puts it on the clipboard
so that it might be pasted into e.g. a GitHub readme file.
```

Get-MarkdownHelp Join-Object |Clip

### EXAMPLE 3
```
# Save markdown help to file
This command creates a markdown readme string for the `.\MyScript.ps1` script and saves it in `Readme.md`.
```

Get-MarkdownHelp .\MyScript.ps1 |Set-Content .\Readme.md

## PARAMETERS

### -CommandName
Specifies the name of the cmdlet that contains the \[comment based help\]\[2\].

```yaml
Type: String
Parameter Sets: (All)
Aliases: Name

Required: True
Position: 1
Default value: None
Accept pipeline input: True (ByPropertyName, ByValue)
Accept wildcard characters: False
```

### -PSCodePattern
Specifies the PowerShell code pattern used by the get-help cmdlet.
The native \[\`Get-Help\`\] cmdlet automatically adds a PowerShell prompt (\`PS \\\>\`) to the first line of an example if not yet exist.
To be consistent with the first line you might manually add a PowerShell prompt to each line of code which will be converted to
a code block by this \`Get-MarkdownHelp\` cmdlet.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 2
Default value: PS.*\>
Accept pipeline input: False
Accept wildcard characters: False
```

### -AlternateEOL
The recommended way to force a line break or new line (\`\<br\>\`) in markdown is to end a line with two or more spaces but as that
might cause a _\[Avoid Trailing Whitespace\]\[7\]_ warning, you might also consider to use an alternate EOL marker.\
Any alternate EOL marker (at the end of the line) will be replaced by two spaces by this \`Get-MarkdownHelp\` cmdlet.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 3
Default value: \
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### String (command name)
## OUTPUTS

### String[]
## NOTES

## RELATED LINKS

[[1]: https://github.com/iRon7/Get-MarkdownHelp "Online Help"
[2]: https://learn.microsoft.com/powershell/module/microsoft.powershell.core/about/about_comment_based_help "About comment based help"
[3]: https://github.com/PowerShell/platyPS "PlatyPS MALM renderer"
[4]: https://www.markdownguide.org/extended-syntax/#fenced-code-blocks "Fenced Code Blocks"
[5]: https://www.markdownguide.org/basic-syntax/#reference-style-links "Reference-style Links"
[7]: https://learn.microsoft.com/powershell/utility-modules/psscriptanalyzer/rules/avoidtrailingwhitespace ""

https://www.markdownguide.org/basic-syntax/ "Markdown guide"]()
