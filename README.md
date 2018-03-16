![](https://github.com/senselogic/BATCHED/blob/master/LOGO/batched.png)

# Batched

Batch text file editor.

## Description

Batched allows to conditionally apply text editing operations on several files at once.

## Sample

```bash
SetInputFolder IN/
SetOutputFolder OUT/

ReadFiles /*.hpp

SetTabulationSpaceCount 4
ReplaceTabulations 0 $
RemoveLastSpaces 0 $
RemoveLastEmptyLines 0 $
AddEmptyLines $ 1

IgnoreFirstSpaces
IgnoreLastSpaces
FindLines% 0 $
    `#ifndef __\Uib_HPP__`
    `#define __\Uib_HPP__`
FindLines~% 0 $
    `#ifndef __\Uib__`
    `#define __\Uib__`
SetLines^ [ ]
    #pragma once
RemoveFirstSpaces^ 0 $ 4
FindLines^% $-2 1
    #endif
RemoveLines^ [ ]

PrintLines

CreateFolders
WriteFiles
```

### Commands

```bash
:label
EnableQuotation
DisableQuotation
CheckFirstSpaces
IgnoreFirstSpaces
CheckLastSpaces
IgnoreLastSpaces
CheckInnerSpaces
IgnoreInnerSpaces
SetTabulationSpaceCount tabulation_space_count
SetFolder INPUT_OUTPUT_FOLDER/
SetInputFolder INPUT_FOLDER/
SetOutputFolder OUTPUT_FOLDER/
RemoveFiles {file_paths}
MoveFiles source_file_path target_file_path
CopyFiles source_file_path target_file_path
ReadFiles {input_file_path_filters}
IncludeFiles {input_file_path_filters}
ExcludeFiles [{input_file_path_filters}]
CreateFiles {input_file_paths}
CreateFolders {folder_paths}
WriteFiles
Print expression
PrintRanges
PrintIntervals
PrintLines [line_index post_line_index]
PrintSelectedLines
PrintChangedLines [near_line_count]
PrintArguments
PrintVariables
SetFilePath file_path
SetLineIndex line_index
SetLineCount line_count
SetLineRange line_index line_count
SetPostLineIndex post_line_index
SetLineInterval line_index post_line_index
ReplaceTabulations line_index post_line_index
ReplaceSpaces line_index post_line_index
ReplaceText line_index post_line_index old_text new_text
ReplaceIdentifier line_index post_line_index old_text new_text
ReplaceUnquotedText line_index post_line_index old_text new_text
ReplaceUnquotedIdentifier line_index post_line_index old_text new_text
ReplaceQuotedText line_index post_line_index old_text new_text
ReplaceQuotedIdentifier line_index post_line_index old_text new_text
ReplaceExpression line_index post_line_index old_expression new_text
SelectFiles {input_file_path_filters}
IgnoreFiles {input_file_path_filters}
MarkFiles {input_file_path_filters}
UnmarkFiles {input_file_path_filters}
FindText line_index post_line_index text
ReachText post_line_index text
FindLines line_index post_line_index {lines}
ReachLines post_line_index {lines}
FindPrefixes line_index post_line_index {prefixes}
ReachPrefixes post_line_index {prefixes}
FindSuffixes line_index post_line_index {suffixes}
ReachSuffixes post_line_index {suffixes}
FindExpressions line_index post_line_index {expressions}
ReachExpressions post_line_index {expressions}
InsertLines line_index character_index {lines}
AddLines line_index {lines}
AddEmptyLines line_index line_count
RemoveLines line_index post_line_index
RemoveFirstEmptyLines line_index post_line_index [line_count]
RemoveLastEmptyLines line_index post_line_index [line_count]
RemoveEmptyLines line_index post_line_index
RemoveDoubleEmptyLines line_index post_line_index
SkipLines
SetLines line_index post_line_index {lines}
CopyLines buffer_letter line_index post_line_index [character_index post_character_index]
CutLines buffer_letter line_index post_line_index [character_index post_character_index]
PasteLines buffer_letter line_index [character_index]
AddText line_index post_line_index character_index text
RemovePrefix line_index post_line_index prefix
RemoveSuffix line_index post_line_index suffix
RemoveText line_index post_line_index character_index post_character_index
RemoveSideText line_index post_line_index character_index post_character_index
AddSpaces line_index post_line_index character_index space_count
RemoveFirstSpaces line_index post_line_index [space_count]
RemoveLastSpaces line_index post_line_index [space_count]
PushIntervals
PullIntervals
PopIntervals
PushSelections
PullSelections
PopSelections
PushMarks
PullMarks
PopMarks
Set variable_name assignment_operator expression
Go label|line_offset [condition]
Repeat label|line_offset
Call label|line_offset {arguments}
Return
Exit
Include script_file_path
Execute script_file_path {arguments}
Do shell_command {arguments}
```

### Command modifiers

```
% : select the matching files
^ : process only the selected files
~ : process only the ignored files
# : mark the matching files
? : process only the marked files
\ : process only the unmarked files
! : don't process the files
```

### File path filter

```
* : zero, one or several unknown characters (*.txt)
? : one unknown character (*.?pp)
// : in this folder and all of its subfolders (FOLDER//*.?pp)
```

### Quotation

```
`` : empty string
`\\` : backslash
`\`` : backtick
`\r` : return
`\n` : newline
`\t` : tab
`\d` : backtab
`\b` : backspace
`\ ` : line indentation
`\L` : convert to lowercase
`\U` : convert to uppercase
`\N` : convert to minorcase
`\M` : convert to majorcase
`\C` : convert to camelcase
`\S` : convert to snakecase
`\&` : all input file paths
`\^` : selected input file paths
`\~` : ignored input file paths
`\?` : marked input file paths
`\:` : unmarked input file paths
`\$0` to `\$9` : script arguments
`\%0` to `\%9` : function arguments
`\$a` to `\$z` : script variables
`\%a` to `\%z` : file variables
`\iP` `\oP` : input/output folder path
`\if` `\of` : input/output file path
`\ip` `\op` : input/output file folder path
`\is` `\os` : input/output file sub folder path
`\in` `\on` : input/output file name
`\ib` `\ob` : input/output file name without extension
`\ie` `\oe` : input/output file extension
`\ix` `\ox` : input/output file extension without dot character
```

### Line index

```
index : line index (starting at 0)
[ : start of selection
[+offset : positive offset to the start of selection
[-offset : negative offset to the start of selection
] : end of selection
]+offset : negative offset to the end of selection
]-offset : positive offset to the end of selection
$ : end of file
$-offset : negative offset to the end of file
```

### Character index

```
index : character_index (starting at 0)
$ : end of line
$-offset : negative offset to the end of line
```

### Assignment operators

```
:= : set
~= : concatenate
$= : append
= : assign
+= : add
-= : substract
*= : multiply
/= : divide
%= : modulo
&= : binary and
|= : binary or
^= : binary xor
<<= : left shift
>>= : right shift
```

### Operators

```
< : lower
<= : lower or equal
== : equal
!= : not equal
>= : higher or equal
> : higher
+ : add
- : substract
* : multiplay
/ : divide
% : modulo
& : binary and
| : binary or
^ : binary xor
<< : left shift
>> : right shift
```

### Comment

```
# this is a comment
```

## Installation

Install the [DMD 2 compiler](https://dlang.org/download.html).

Build the executable with the following command line :

```bash
dmd -m64 batched.d
```

## Command line

```bash
batched [options] script_file.batched
```

### Options

```bash
--verbose : show the processing messages
--preview : preview the changes without applying them
```

### Examples

```bash
batched --verbose --preview script_file.batched
```

Test the changes, showing 3 neighboring lines around each fixed line.

```bash
batched script_file.batched
```

Apply the changes to the files.

## Version

1.0

## Author

Eric Pelzer (ecstatic.coder@gmail.com).

## License

This project is licensed under the GNU General Public License version 3.

See the [LICENSE.md](LICENSE.md) file for details.