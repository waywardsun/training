# Chapter 5 Labs

## Lab 5-1

Analyze the malware found in the file Lab05-01.dll using only IDA Pro. The goal of this lab is to give you hands-on experience with IDA Pro. If you’ve already worked with IDA Pro, you may choose to ignore these questions and focus on reverse-engineering the malware.

### Questions
**1. What is the address of DllMain?**

```
0x1000D02E (Located in .text)
```

**2. Use the Imports window to browse to gethostbyname. Where is the import located?**

```
| Address  | Ordinal | Name          | Library |
|----------+---------+---------------+---------|
| 100163CC | 52      | gethostbyname | GDI32   |
```

**3. How many functions call gethostbyname?**

```
We learned that type 'p' is a reference and 'r' is a read-reference.
This causes IDA to double count the same references.
Because of this, we report there are only 9 function calls.

The five functions that call it are:
  sub_10001074, sub_10001365, sub_10001656, sub_1000208F, sub_10002CCE

| Direction | Type | Address                   | Text                     |
|-----------|------|---------------------------|--------------------------|
| Up        | p    | sub_10001074:loc_100011AF | call    ds:gethostbyname |
| Up        | p    | sub_10001074+1D3          | call    ds:gethostbyname |
| Up        | p    | sub_10001074+26B          | call    ds:gethostbyname |
| Up        | p    | sub_10001365:loc_100014A0 | call    ds:gethostbyname |
| Up        | p    | sub_10001365+1D3          | call    ds:gethostbyname |
| Up        | p    | sub_10001365+26B          | call    ds:gethostbyname |
| Up        | p    | sub_10001656+101          | call    ds:gethostbyname |
| Up        | p    | sub_1000208F+3A1          | call    ds:gethostbyname |
| Up        | p    | sub_10002CCE+4F7          | call    ds:gethostbyname |
| Up        | r    | sub_10001074:loc_100011AF | call    ds:gethostbyname |
| Up        | r    | sub_10001074+1D3          | call    ds:gethostbyname |
| Up        | r    | sub_10001074+26B          | call    ds:gethostbyname |
| Up        | r    | sub_10001365:loc_100014A0 | call    ds:gethostbyname |
| Up        | r    | sub_10001365+1D3          | call    ds:gethostbyname |
| Up        | r    | sub_10001365+26B          | call    ds:gethostbyname |
| Up        | r    | sub_10001656+101          | call    ds:gethostbyname |
| Up        | r    | sub_1000208F+3A1          | call    ds:gethostbyname |
| Up        | r    | sub_10002CCE+4F7          | call    ds:gethostbyname |
```

**4. Focusing on the call to gethostbyname located at 0x10001757, can you figure out which DNS request will be made?**

```
off_10019040 leads to '[This is RDO]pics.praticalmalwareanalysis.com'

I assume it will drop the leading text and request 'pics.praticalmalwareanalysis.com'
```

**5. How many local variables has IDA Pro recognized for the subroutine at 0x10001656?**

```
I determined that all variables with a negative offset are local variables.
Because of this, I calculate 23 local variables.

.text:10001656 ; =============== S U B R O U T I N E =======================================
.text:10001656
.text:10001656
.text:10001656 ; DWORD __stdcall sub_10001656(LPVOID lpThreadParameter)
.text:10001656 sub_10001656    proc near               ; DATA XREF: DllMain(x,x,x)+C8o
.text:10001656
.text:10001656 var_675         = byte ptr -675h
.text:10001656 var_674         = dword ptr -674h
.text:10001656 hModule         = dword ptr -670h
.text:10001656 timeout         = timeval ptr -66Ch
.text:10001656 name            = sockaddr ptr -664h
.text:10001656 var_654         = word ptr -654h
.text:10001656 Dst             = dword ptr -650h
.text:10001656 Str1            = byte ptr -644h
.text:10001656 var_640         = byte ptr -640h
.text:10001656 CommandLine     = byte ptr -63Fh
.text:10001656 Str             = byte ptr -63Dh
.text:10001656 var_638         = byte ptr -638h
.text:10001656 var_637         = byte ptr -637h
.text:10001656 var_544         = byte ptr -544h
.text:10001656 var_50C         = dword ptr -50Ch
.text:10001656 var_500         = byte ptr -500h
.text:10001656 Buf2            = byte ptr -4FCh
.text:10001656 readfds         = fd_set ptr -4BCh
.text:10001656 buf             = byte ptr -3B8h
.text:10001656 var_3B0         = dword ptr -3B0h
.text:10001656 var_1A4         = dword ptr -1A4h
.text:10001656 var_194         = dword ptr -194h
.text:10001656 WSAData         = WSAData ptr -190h
.text:10001656 lpThreadParameter= dword ptr  4
.text:10001656
```

**6. How many parameters has IDA Pro recognized for the subroutine at 0x10001656?**

```
I determined that all variables with a positive offset are function parameters.
Because of this, I calculate 1 function parameter.

.text:10001656 ; =============== S U B R O U T I N E =======================================
.text:10001656
.text:10001656
.text:10001656 ; DWORD __stdcall sub_10001656(LPVOID lpThreadParameter)
.text:10001656 sub_10001656    proc near               ; DATA XREF: DllMain(x,x,x)+C8o
.text:10001656
.text:10001656 var_675         = byte ptr -675h
.text:10001656 var_674         = dword ptr -674h
.text:10001656 hModule         = dword ptr -670h
.text:10001656 timeout         = timeval ptr -66Ch
.text:10001656 name            = sockaddr ptr -664h
.text:10001656 var_654         = word ptr -654h
.text:10001656 Dst             = dword ptr -650h
.text:10001656 Str1            = byte ptr -644h
.text:10001656 var_640         = byte ptr -640h
.text:10001656 CommandLine     = byte ptr -63Fh
.text:10001656 Str             = byte ptr -63Dh
.text:10001656 var_638         = byte ptr -638h
.text:10001656 var_637         = byte ptr -637h
.text:10001656 var_544         = byte ptr -544h
.text:10001656 var_50C         = dword ptr -50Ch
.text:10001656 var_500         = byte ptr -500h
.text:10001656 Buf2            = byte ptr -4FCh
.text:10001656 readfds         = fd_set ptr -4BCh
.text:10001656 buf             = byte ptr -3B8h
.text:10001656 var_3B0         = dword ptr -3B0h
.text:10001656 var_1A4         = dword ptr -1A4h
.text:10001656 var_194         = dword ptr -194h
.text:10001656 WSAData         = WSAData ptr -190h
.text:10001656 lpThreadParameter= dword ptr  4
.text:10001656
```

**7. Use the Strings window to locate the string \cmd.exe /c in the disassembly. Where is it located?**

```
| Address           | Length   | Type | String       |
|-------------------|----------|------|--------------|
| xdoors_d:10095B34 | 0000000D | C    | \\cmd.exe /c |
```

**8. What is happening in the area of code that references \cmd.exe /c?**

```
After using this string, the software calls recv on a socket.
This leads me to believe it created a reverse shell.
```

**9. In the same area, at 0x100101C8, it looks like dword_1008E5C4 is a global variable that helps decide which path to take. How does the malware set dword_1008E5C4? (Hint: Use dword_1008E5C4’s cross-references.)**

```
The value is set to the OS version number.
```

**10. A few hundred lines into the subroutine at 0x1000FF58, a series of comparisons use memcmp to compare strings. What happens if the string comparison to robotwork is successful (when memcmp returns 0)?**

```
It makes a call to:
  int __cdecl sub_100052A2(SOCKET s)

This function appears to modify the registry, or at least look at values stored inside of it.
```

**11. What does the export PSLIST do?**

```
I got this one wrong.....

The correct answer:
  The PSLIST export sends a process listing across the network or finds a
  particular process name in the listing and gets information about it.
```

**12. Use the graph mode to graph the cross-references from sub_10004E79. Which API functions could be called by entering this function? Based on the API functions alone, what could you rename this function?**

```
API Calls:
  GetSystemDefaultLangID
  sprintf
  strlen

I would rename this function getLanguage()
```

**13. How many Windows API functions does DllMain call directly? How many at a depth of 2?**

```
I got this one wrong.....

The correct answer:
  DllMain calls strncpy, strnicmp, CreateThread, and strlen directly. At a depth
  of 2, it calls a variety of API calls, including Sleep, WinExec, gethostbyname,
  and many other networking function calls.
```

**14. At 0x10001358, there is a call to Sleep (an API function that takes one parameter containing the number of milliseconds to sleep). Looking backward through the code, how long will the program sleep if this code executes?**

```
30000 milliseconds or 30 seconds
```

**15. At 0x10001701 is a call to socket. What are the three parameters?**

```
socket(2, 1, 6)

.text:100016FB 6A 06                             push    6     ; protocol
.text:100016FD 6A 01                             push    1     ; type
.text:100016FF 6A 02                             push    2     ; af
.text:10001701 FF 15 F8 63 01 10                 call    ds:socket
```

**16. Using the MSDN page for socket and the named symbolic constants functionality in IDA Pro, can you make the parameters more meaningful? What are the parameters after you apply changes?**

```
socket(AF_INET, SOCK_STREAM, IPPROTO_TCP)

.text:100016FB 6A 06                             push    IPPROTO_TCP     ; protocol
.text:100016FD 6A 01                             push    SOCK_STREAM     ; type
.text:100016FF 6A 02                             push    AF_INET         ; af
.text:10001701 FF 15 F8 63 01 10                 call    ds:socket
```


**17. Search for usage of the in instruction (opcode 0xED). This instruction is used with a magic string VMXh to perform VMware detection. Is that in use in this malware? Using the cross-references to the function that executes the in instruction, is there further evidence of VMware detection?**

```
Found instruction with usage of magic string:
  .text:100061C7 B8 68 58 4D 56                    mov     eax, 'VMXh'
  .text:100061CC BB 00 00 00 00                    mov     ebx, 0
  .text:100061D1 B9 0A 00 00 00                    mov     ecx, 0Ah
  .text:100061D6 BA 58 56 00 00                    mov     edx, 'VX'
  .text:100061DB ED                                in      eax, dx
  .text:100061DC 81 FB 68 58 4D 56                 cmp     ebx, 'VMXh'     ; Compare Two Operands

Cross reference leads to the following proof of VMWare detection:
  .text:1000D87A C7 04 24 88 4F 09+                mov     [esp+8+Format], offset aFoundVirtualMa ; "Found Virtual Machine,Install Cancel."
```


**18. Jump your cursor to 0x1001D988. What do you find?**

```
Looks like random data:
  .data:1001D988                 db  2Dh ; -
  .data:1001D989                 db  31h ; 1
  .data:1001D98A                 db  3Ah ; :
  .data:1001D98B                 db  3Ah ; :
  .data:1001D98C                 db  27h ; '
  .data:1001D98D                 db  75h ; u
  .data:1001D98E                 db  3Ch ; <
  .data:1001D98F                 db  26h ; &
  .data:1001D990                 db  75h ; u
  .data:1001D991                 db  21h ; !
  .data:1001D992                 db  3Dh ; =
  .data:1001D993                 db  3Ch ; <
  .data:1001D994                 db  26h ; &
  .data:1001D995                 db  75h ; u
  .data:1001D996                 db  37h ; 7
  .data:1001D997                 db  34h ; 4
  .data:1001D998                 db  36h ; 6
  .data:1001D999                 db  3Eh ; >
  .data:1001D99A                 db  31h ; 1
  .data:1001D99B                 db  3Ah ; :
  .data:1001D99C                 db  3Ah ; :
  .data:1001D99D                 db  27h ; '
  .data:1001D99E                 db  79h ; y
  .data:1001D99F                 db  75h ; u
  .data:1001D9A0                 db  26h ; &
  .data:1001D9A1                 db  21h ; !
  .data:1001D9A2                 db  27h ; '
  .data:1001D9A3                 db  3Ch ; <
  .data:1001D9A4                 db  3Bh ; ;
  .data:1001D9A5                 db  32h ; 2
  .data:1001D9A6                 db  75h ; u
  .data:1001D9A7                 db  31h ; 1
  .data:1001D9A8                 db  30h ; 0
  .data:1001D9A9                 db  36h ; 6
  .data:1001D9AA                 db  3Ah ; :
  .data:1001D9AB                 db  31h ; 1
  .data:1001D9AC                 db  30h ; 0
  .data:1001D9AD                 db  31h ; 1
  .data:1001D9AE                 db  75h ; u
  .data:1001D9AF                 db  33h ; 3
  .data:1001D9B0                 db  3Ah ; :
  .data:1001D9B1                 db  27h ; '
  .data:1001D9B2                 db  75h ; u
  .data:1001D9B3                 db    5
  .data:1001D9B4                 db  27h ; '
  .data:1001D9B5                 db  34h ; 4
  .data:1001D9B6                 db  36h ; 6
  .data:1001D9B7                 db  21h ; !
  .data:1001D9B8                 db  3Ch ; <
  .data:1001D9B9                 db  36h ; 6
  .data:1001D9BA                 db  34h ; 4
  .data:1001D9BB                 db  39h ; 9
  .data:1001D9BC                 db  75h ; u
  .data:1001D9BD                 db  18h
  .data:1001D9BE                 db  34h ; 4
  .data:1001D9BF                 db  39h ; 9
  .data:1001D9C0                 db  22h ; "
  .data:1001D9C1                 db  34h ; 4
  .data:1001D9C2                 db  27h ; '
  .data:1001D9C3                 db  30h ; 0
  .data:1001D9C4                 db  75h ; u
  .data:1001D9C5                 db  14h
  .data:1001D9C6                 db  3Bh ; ;
  .data:1001D9C7                 db  34h ; 4
  .data:1001D9C8                 db  39h ; 9
  .data:1001D9C9                 db  2Ch ; ,
  .data:1001D9CA                 db  26h ; &
  .data:1001D9CB                 db  3Ch ; <
  .data:1001D9CC                 db  26h ; &
  .data:1001D9CD                 db  75h ; u
  .data:1001D9CE                 db  19h
  .data:1001D9CF                 db  34h ; 4
  .data:1001D9D0                 db  37h ; 7
  .data:1001D9D1                 db  75h ; u
  .data:1001D9D2                 db  6Fh ; o
  .data:1001D9D3                 db  7Ch ; |
  .data:1001D9D4                 db  64h ; d
  .data:1001D9D5                 db  67h ; g
  .data:1001D9D6                 db  66h ; f
  .data:1001D9D7                 db  61h ; a
```


**19. If you have the IDA Python plug-in installed (included with the commercial version of IDA Pro), run Lab05-01.py, an IDA Pro Python script provided with the malware for this book. (Make sure the cursor is at 0x1001D988.) What happens after you run the script?**

```
It converts all the byts to readable ASCII characters:
  .data:1001D988                 db  78h ; x
  .data:1001D989                 db  64h ; d
  .data:1001D98A                 db  6Fh ; o
  .data:1001D98B                 db  6Fh ; o
  .data:1001D98C                 db  72h ; r
  .data:1001D98D                 db  20h
  .data:1001D98E                 db  69h ; i
  .data:1001D98F                 db  73h ; s
  .data:1001D990                 db  20h
  .data:1001D991                 db  74h ; t
  .data:1001D992                 db  68h ; h
  .data:1001D993                 db  69h ; i
  .data:1001D994                 db  73h ; s
  .data:1001D995                 db  20h
  .data:1001D996                 db  62h ; b
  .data:1001D997                 db  61h ; a
  .data:1001D998                 db  63h ; c
  .data:1001D999                 db  6Bh ; k
  .data:1001D99A                 db  64h ; d
  .data:1001D99B                 db  6Fh ; o
  .data:1001D99C                 db  6Fh ; o
  .data:1001D99D                 db  72h ; r
  .data:1001D99E                 db  2Ch ; ,
  .data:1001D99F                 db  20h
  .data:1001D9A0                 db  73h ; s
  .data:1001D9A1                 db  74h ; t
  .data:1001D9A2                 db  72h ; r
  .data:1001D9A3                 db  69h ; i
  .data:1001D9A4                 db  6Eh ; n
  .data:1001D9A5                 db  67h ; g
  .data:1001D9A6                 db  20h
  .data:1001D9A7                 db  64h ; d
  .data:1001D9A8                 db  65h ; e
  .data:1001D9A9                 db  63h ; c
  .data:1001D9AA                 db  6Fh ; o
  .data:1001D9AB                 db  64h ; d
  .data:1001D9AC                 db  65h ; e
  .data:1001D9AD                 db  64h ; d
  .data:1001D9AE                 db  20h
  .data:1001D9AF                 db  66h ; f
  .data:1001D9B0                 db  6Fh ; o
  .data:1001D9B1                 db  72h ; r
  .data:1001D9B2                 db  20h
  .data:1001D9B3                 db  50h ; P
  .data:1001D9B4                 db  72h ; r
  .data:1001D9B5                 db  61h ; a
  .data:1001D9B6                 db  63h ; c
  .data:1001D9B7                 db  74h ; t
  .data:1001D9B8                 db  69h ; i
  .data:1001D9B9                 db  63h ; c
  .data:1001D9BA                 db  61h ; a
  .data:1001D9BB                 db  6Ch ; l
  .data:1001D9BC                 db  20h
  .data:1001D9BD                 db  4Dh ; M
  .data:1001D9BE                 db  61h ; a
  .data:1001D9BF                 db  6Ch ; l
  .data:1001D9C0                 db  77h ; w
  .data:1001D9C1                 db  61h ; a
  .data:1001D9C2                 db  72h ; r
  .data:1001D9C3                 db  65h ; e
  .data:1001D9C4                 db  20h
  .data:1001D9C5                 db  41h ; A
  .data:1001D9C6                 db  6Eh ; n
  .data:1001D9C7                 db  61h ; a
  .data:1001D9C8                 db  6Ch ; l
  .data:1001D9C9                 db  79h ; y
  .data:1001D9CA                 db  73h ; s
  .data:1001D9CB                 db  69h ; i
  .data:1001D9CC                 db  73h ; s
  .data:1001D9CD                 db  20h
  .data:1001D9CE                 db  4Ch ; L
  .data:1001D9CF                 db  61h ; a
  .data:1001D9D0                 db  62h ; b
  .data:1001D9D1                 db  20h
  .data:1001D9D2                 db  3Ah ; :
  .data:1001D9D3                 db  29h ; )
  .data:1001D9D4                 db  31h ; 1
  .data:1001D9D5                 db  32h ; 2
  .data:1001D9D6                 db  33h ; 3
  .data:1001D9D7                 db  34h ; 4
```


**20. With the cursor in the same location, how do you turn this data into a single ASCII string?**

```
By pressing 'a' on the first character, it reads the data as a single string.
  .data:1001D988 aXdoorIsThisBac db 'xdoor is this backdoor, string decoded for Practical Malware Analysis Lab :)1234',0
```


**21. Open the script with a text editor. How does it work?**

```
The script does a bitwise XOR of the next 0x50 bytes with the hex value 0x55.
```

