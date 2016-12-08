#Chapter 5: Notes

## IDA Pro

- **Interactive Disassembler Professional (IDA Pro)**
  - Extremely powerful disassembler distributed by Hex-Rays.
  - Performs tasks such as function discovery, stack analysis, local variable identification, and much more
  - Includes extensive code signatures within its Fast Library Identification and Recognition Technology (FLIRT)
  - Robust support for plug-ins, so you can write your own extensions or leverage the work of others.
  - Two versions of IDA Pro are commercially available (standard and advanced).
  - The advanced version supports many more processors than the standard version, most notably x64.
  - Additional Resource: "The IDA Pro Book: The Unofficial Guide to the World’s Most Popular Disassembler, 2nd Edition"

- **Loading an Executable**
  - Upon loading a binary, IDA Pro will try to recognize the file’s format and processor architecture.
  - Unless you are analyzing cell phone malware, you won’t need to modify the processor type often.
  - When loading a file, IDA maps the file into memory as if it had been loaded by the operating system loader.

- **Loading a file as a Binary File**
  - Sometimes malware appends shellcode, additional data, etc to legitimate PE files
  - On occasion, this extra data won’t be loaded into memory when the malware is run by Windows or loaded into IDA Pro.
  - To addres this, you can choose to have IDA disassemble the file as a raw binary by choosing the Binary File option.
  - When you are loading a raw file containing shellcode, you should choose to load the file as a binary file and disassemble it.

- **PE File Rebasing**
  - PE files are compiled to load at a preferred base address in memory.
  - If it can’t load at it's preferred address (address is taken), the loader will perform an operation known as rebasing.
  - This happens often with DLLs, since they are often loaded at locations that differ from their preferred address.
  - If you encounter a DLL loaded into a process different from what you see in IDA Pro, it could be the result of being rebased.
  - When this occurs, check the Manual Load checkbox and specify the new virtual base address in which to load the file.



## IDA Pro Interface

- **Interface Modes**
  - After you load a program into IDA Pro, you will see the disassembly window.
  - This will be your primary space for manipulating and analyzing binaries, and it’s where the assembly code resides.
  - You can display the disassembly window in one of two modes: graph (the default) and text.
  - To switch between modes, press the spacebar.

- **Graph Mode**
  - By default, IDA Pro excludes certain information that can be useful, such as line numbers and operation codes.
  - To change these options, select ```Options -> General```, and then select Line prefixes and set the Number of Opcode Bytes to 6
  - Since most instructions contain 6 or fewer bytes, this allows you to see memory locations and opcode values for each instruction.
  - In graph mode, the color and direction of the arrows help show the program’s flow during analysis.
  - The arrow’s color tells you whether the path is based on a particular decision having been made.
  - Red Arrow - Conditional jump is not taken.
  - Green Arrow -  Conditional jump is taken.
  - Blue Arrow - Unconditional jump.
  - Upward Arrows - Indicate a loop.
  - Highlighting text in graph mode highlights every instance of that text in the disassembly window.

- **Text Mode**
  - Text mode of the disassembly window is a more traditional view.
  - You must use text mode to view data regions of a binary.
  - It displays the memory address and section name in which the opcodes will reside in memory.
  - Functions include the stack layout and comments (beginning with a semicolon) that are automatically added by IDA Pro
  - The left portion of the text-mode display is known as the arrows window and shows the program’s nonlinear flow.
  - Solid Line - Unconditional jumps.
  - Dashed Line - Conditional jumps.
  - Upward Arrows - Indicate a loop.
  - For hints in reading assembly, select ```Options -> General```, and then check the Auto comments checkbox.

- **Default View**
  - The IDA Pro interface is so rich that you may find it impossible to navigate.
  - To return to the default view, choose ```Windows -> Reset Desktop```.
  - It will simply restore any windows and GUI elements to their defaults.
  - Choosing this option won’t undo any labeling or disassembly you’ve done.
  - If you like the customized window, you can save the it by selecting ```Windows -> Save desktop```.



## Useful Windows for Analysis

- **Functions Window**
  - Lists all functions in the executable and shows the length of each.
  - You can sort by function length and filter for large, complicated functions.
  - This window also associates flags with each function (F, L, S, and so on)
    - L: Library Functions
    - F: Far Function
    - S: Static Function
  - The L flag can save you time during analysis, because you can identify and skip these compiler-generated functions.

- **Names Window**
  - Lists every address with a name, including functions, named code, named data, and strings.

- **Strings Window**
  - Shows all strings in the binary.
  - By default, this list shows only ASCII strings longer than five characters.
  - You can change this by right-clicking in the Strings window and selecting Setup.

- **Imports Window**
  - Lists all imports for a file.

- **Exports Window**
  - Lists all the exported functions for a file. 
  - This window is useful when you’re analyzing DLLs.

- **Structures Window**
  - Lists the layout of all active data structures. 
  - The window also provides you the ability to create your own data structures for use as memory layout templates.

  

## Links and Cross-References

- **Links**
  - 'Sub Links' - links to the start of functions such as printf and sub_4010A0.
  - 'Loc Links' - links to jump destinations such as loc_40107E and loc_401097.
  - 'Offset Links' - links to an offset in memory.

- **Cross-References**
  - A cross-reference, aka xref in IDA, tells you where a function is called or where a string is used. 
  - Allows you to navigate quickly to the location where a function's parameters are placed on the stack.
  - Interesting graphs can also be generated based on cross-references, which are helpful to performing analysis.
  - Cross-references are useful for jumping IDA's display to the referencing location
  - Because strings are typically references, they are also navigational links. 

- **Showing all Code Cross-References**
  - By default, IDA shows only a couple of cross-references, even though many may occur when a function is called.
  - To view all the cross-references for a function, click the function name and press ```X``` on your keyboard.
  - Double-click any entry in the Xrefs window to go to the corresponding reference in the disassembly window.



## Navigation

- **History**
  - IDA Pro’s forward and back buttons make it easy to move through your history
  - Each time you navigate to a new location within the disassembly window, that location is added to your history.

- **Navigation Band**
  - The horizontal color band at the base of the toolbar is the navigation band.
  - Presents a color-coded linear view of the loaded binary’s address space.
  - The colors offer insight into the file contents at that location in the file.
  - ```Light Blue``` - Library code as recognized by FLIRT.
  - ```Red``` - Compiler-generated code.
  - ```Dark Blue``` - User-written code

- **Jump to Location**
  - To jump to any virtual memory address, simply press the ```G``` key on your keyboard while in the disassembly window.
  - A dialog box appears, asking for a virtual memory address or named location, such as ```sub_401730```.
  - To jump to a raw file offset, choose ```Jump -> Jump to File Offset```.


```
When to jump to a raw file offset:

  For example, if you’re viewing a PE file in a hex editor and you see something
interesting, such as a string or shellcode, you can use this feature to get to
that raw offset, because when the file is loaded into IDA Pro, it will be mapped
as though it had been loaded by the OS loader.
```

- **Searching**
  - ```Search -> Next Code``` moves the cursor to the next location containing an instruction you specify.
  - ```Search -> Text``` searches the entire disassembly window for a specific string.
  - ```Search -> Sequence of Bytes``` performs a binary search in the hex view window for a certain byte order.



## Analyzing Functions

- **IDA Pro's Analysis Abilities**
  - The ability to recognize functions, label them, and break down the local variables and parameters.
  - IDA can also analyze stack frames, finding all local variables and parameters.
  - IDA will label local variables with the prefix var_ and parameters with the prefix arg_.
  - IDA gives the local variables and parameters a suffix corresponding to their offset relative to EBP.
  - Local variables will be at a negative offset relative to EBP.
  - Arguments will be at a positive offset relative to EBP.
  - If IDA fails to identify a function, you can create a function by pressing P.
  - It may also fail to identify EBP-based stack frames.
  - In this case, the instructions mov [ebp-0Ch], eax and push dword ptr [ebp-010h] might appear instead of the convenient labeling.
  - In most cases, you can fix this by pressing ALT-P, selecting BP Based Frame, and specifying 4 bytes for Saved Registers.
  - EBP based stack frame - the local variables and parameters will be referenced via the EBP register

- **Graphing Options**
  - IDA Pro supports five graphing options.
  - Four of these graphing options utilize cross-references.
  - Unlike the graph view of the disassembly window, these graphs cannot be manipulated with IDA.


```
Graphing Choices:
-----------------
Function:    Creates a flow chart of the current function:
Description: Users will prefer to use the interactive graph mode of the
             disassembly window but may use this button at times to see
             an alternate graph view. (We’ll use this option to graph code
             in Chapter 6.)

Function:    Graphs function calls for the entire program
Description: Use this to gain a quick understanding of the hierarchy of
             function calls made within a program, as shown in Figure 5-8.
             To dig deeper, use WinGraph32’s zoom feature. You will
             find that graphs of large statically linked executables can
             become so cluttered that the graph is unusable.

Function:    Graphs the cross-references to get to a currently selected cross-reference
Description: This is useful for seeing how to reach a certain identifier. It’s
             also useful for functions, because it can help you see the
             different paths that a program can take to reach a particular
             function.

Function:    Graphs the cross-references from the currently selected symbol
Description: This is a useful way to see a series of function calls. For
             example, Figure 5-9 displays this type of graph for a single
             function. Notice how sub_4011f0 calls sub_401110, which then
             calls gethostbyname. This view can quickly tell you what a
             function does and what the functions do underneath it. This is
             the easiest way to get a quick overview of the function.

Function:    Graphs a user-specified cross-reference graph
Description: Use this option to build a custom graph. You can specify the
             graph’s recursive depth, the symbols used, the to or from
             symbol, and the types of nodes to exclude from the graph.
             This is the only way to modify graphs generated by IDA Pro
             for display in WinGraph32.
```



## Enhancing Disassembly

- **Renaming Locations**
  - IDA Pro does a good job of automatically naming virtual address and stack variables.
  - You can also modify these names to make them more meaningful.
  - A function named ```ReverseBackdoorThread``` would be a lot more useful than ```sub_401000```.
  - When renaming dummy names, you need to do so in only one place.
  - IDA Pro will propagate the new name wherever that item is referenced.

- **Comments**
  - IDA lets you embed comments throughout your disassembly and adds many comments automatically.
  - To add a comment to a single line, place the cursor on a line of disassembly and press the ```:``` key.
  - To add a comment to be echoed whenever there is a xref to the selected address, press the ```;``` key.

```
Increased Readability through Argument Renaming Example:

| Without renamed arguments           | With renamed arguments              |
|-------------------------------------|-------------------------------------| 
| 004013C8 mov eax, [ebp+arg_4]       | 004013C8 mov eax, [ebp+port_str]    |
| 004013CB push eax                   | 004013CB push eax                   |
| 004013CC call _atoi                 | 004013CC call _atoi                 |
| 004013D1 add esp, 4                 | 004013D1 add esp, 4                 |
| 004013D4 mov [ebp+var_598], ax      | 004013D4 mov [ebp+port], ax         |
| 004013DB movzx ecx, [ebp+var_598]   | 004013DB movzx ecx, [ebp+port]      |
| 004013E2 test ecx, ecx              | 004013E2 test ecx, ecx              |
| 004013E4 jnz short loc_4013F8       | 004013E4 jnz short loc_4013F8       |
| 004013E6 push offset aError         | 004013E6 push offset aError         |
| 004013EB call printf                | 004013EB call printf                |
| 004013F0 add esp, 4                 | 004013F0 add esp, 4                 |
| 004013F3 jmp loc_4016FB             | 004013F3 jmp loc_4016FB             |
| 004013F8 ; --------------------     | 004013F8 ; --------------------     |
| 004013F8                            | 004013F8                            |
| 004013F8 loc_4013F8:                | 004013F8 loc_4013F8:                |
| 004013F8 movzx edx, [ebp+var_598]   | 004013F8 movzx edx, [ebp+port]      |
| 004013FF push edx                   | 004013FF push edx                   |
| 00401400 call ds:htons              | 00401400 call ds:htons              |
```

- **Named Constants**
  - Programmers often use named constants such as GENERIC_READ and STDOUT in their source code.
  - They are implemented as an integer in the binary.
  - After compilation, it is no longer possible to determine whether the source used a symbolic constant or a literal.
  - IDA Pro provides a large catalog of named constants for the Windows API and the C standard library.
  - You can use the Use Standard Symbolic Constant option on an operand in your disassembly.
  - If a particular standard symbolic constant does not appear, you need to load the relevant type library manually.
  - To do so, select ```View -> Open Subviews -> Type Libraries``` to view the currently loaded libraries.
  - To get the symbolic constants for the Native Windows API, load ```ntapi``` libraries.
  - In the same vein, when analyzing a Linux binary, you may need to manually load the ```gnuunx``` libraries.

```
Increased Readability through Named Constants Renaming Example:

| Before symbolic constants                | After symbolic constants                           |
|------------------------------------------|----------------------------------------------------| 
| mov esi, [esp+1Ch+argv]                  | mov esi, [esp+1Ch+argv]                            |
| mov edx, [esi+4]                         | mov edx, [esi+4]                                   |
| mov edi, ds:CreateFileA                  | mov edi, ds:CreateFileA                            |
| push 0         ; hTemplateFile           | push NULL                  ; hTemplateFile         |
| push 80h       ; dwFlagsAndAttributes    | push FILE_ATTRIBUTE_NORMAL ; dwFlagsAndAttributes  |
| push 3         ; dwCreationDisposition   | push OPEN_EXISTING         ; dwCreationDisposition |
| push 0         ; lpSecurityAttributes    | push NULL                  ; lpSecurityAttributes  |
| push 1         ; dwShareMode             | push FILE_SHARE_READ       ; dwShareMode           |
| push 80000000h ; dwDesiredAccess         | push GENERIC_READ          ; dwDesiredAccess       |
| push edx ; lpFileName                    | push edx ; lpFileName                              |
| call edi ; CreateFileA                   | call edi ; CreateFileA                             |
```


## Extending IDA with Plug-ins

- **Scripts**
  - IDC and Python scripts can be run easily as files by choosing ```File -> Script File```
  - Alternatively, you can also run them as individual commands by selecting ```File -> IDC Command``` or ```File -> Python Command```
  - The output window at the bottom of the workspace contains a log view that is extensively used by plug-ins for debugging and status messages.

- **Using IDC Scripts*
  - IDA Pro has had a built-in scripting language known as IDC.
  - Predates the widespread popularity of scripting languages such as Python and Ruby.
  - The IDC subdirectory contains several sample IDC scripts that IDA Pro uses to analyze disassembled texts.
  - IDC scripts are programs made up of functions, with all functions declared as static.
  - Arguments don’t need the type specified, and auto is used to define local variables.
  - IDC has many built-in functions, as described in the IDA Pro help index or the idc.idc file.
  - The idc.idc file is typically included with scripts that use the built-in functions.

- **Using IDAPython**
  - IDAPython is fully integrated into the current version of IDA Pro.
  - It brings the power and convenience of Python scripting to binary analysis.
  - IDAPython exposes a significant portion of IDA Pro’s SDK functionality.
  - It allows for far more powerful scripting than offered with IDC.
  - IDAPython has three modules.
    - ```idaapi``` - Provides access to the IDA API.
    - ```idc``` - Provides access to the IDC interface.
    - ```idautils``` - Provides access to the IDAPython utility functions.
  - IDAPython scripts are programs that use an effective address (EA) to perform the primary method of referencing.
  - There are no abstract data types, and most calls take either an EA or a symbol name string.

- **Using Commercial Plug-ins**
  - You should consider purchasing a few commercial plug-ins, such as the Hex-Rays Decompiler and zynamics BinDiff.
  - The Hex-Rays Decompiler is a useful plug-in that converts IDA Pro disassembly into a human-readable, C-like pseudocode text.
  - zynamics BinDiff is a useful tool for comparing two IDA Pro databases.
    - It allows you to pinpoint differences between malware variants.
    - This includes new functions and differences between similar functions.