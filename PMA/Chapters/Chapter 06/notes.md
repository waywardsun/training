#Chapter 6: Notes

## Recognizing C Code Constructs in Assembly

- **Code Constructs**
  - Code abstraction level that defines a functional property but not the details of its implementation.
  - Code constructs include loops, if statements, linked lists, switch statements, and so on.
  - Programs can be broken down into individual constructs that implement the overall functionality of the program.
  - Your goal as a malware analyst will be to go from disassembly to highlevel constructs.
  - Compiler versions and settings can impact how a particular construct appears in disassembly.
  - switch statements, function calls, and others can be compiled differently using different compilers.
  - Your goal is to understand the functionality of a program, not to analyze every single instruction.

## Global vs Local Variables.

- **Global Variables**
  - Can be accessed and used by any function in a program.
  - In assembly, global variables are referenced by memory addresses.
  - In the example below, the global variable ```x``` is signified by ```dword_40CF60```, a memory location at ```0x40CF60```.
  - Notice that ```x``` is changed in memory when eax is moved into ```dword_40CF60```.
  - All subsequent functions that utilize this variable will be impacted.

####Sample Global Variable Program

```
int x = 1;
int y = 2;

void main(){
  x = x+y;
  printf("Total = %d\n", x);
}
```

####Sample Global Variable Program Disassembly

```
00401003 mov eax, dword_40CF60
00401008 add eax, dword_40C000
0040100E mov dword_40CF60, eax
00401013 mov ecx, dword_40CF60
00401019 push ecx
0040101A push offset aTotalD ;"total = %d\n"
0040101F call printf
```

- **Local Variables**
  - Can be accessed only by the function in which they are defined.
  - In assembly, local variables are referenced by the stack addresses.
  - In the example below, , the local variable ```x``` is located on the stack at a constant offset relative to ebp.
  - Memory location ```[ebp-4]``` is used consistently throughout this function to reference the local variable ```x```.
  - This tells us that ```ebp-4``` is a stack-based local variable that is referenced only in the function in which it is defined.

####Sample Local Variable Program

```
void main(){
  int x = 1;
  int y = 2;

  x = x+y;
  printf("Total = %d\n", x);
}
```

####Sample Local Variable Program Disassembly

```
00401006 mov dword ptr [ebp-4], 0
0040100D mov dword ptr [ebp-8], 1
00401014 mov eax, [ebp-4]
00401017 add eax, [ebp-8]
0040101A mov [ebp-4], eax
0040101D mov ecx, [ebp-4]
00401020 push ecx
00401021 push offset aTotalD ; "total = %d\n"
00401026 call printf
```

## Disassembling Arithmetic Operations

####Sample Arithmetic Program

```
int a = 0;
int b = 1;
a = a + 11;
a = a - b;
a--;
b++;
b = a % 3;
```

####Sample Arithmetic Program Disassembly

```
00401006 mov [ebp+var_4], 0     ; int a = 0
0040100D mov [ebp+var_8], 1     ; int b = 1
00401014 mov eax, [ebp+var_4]   ; Put a into eax --,
00401017 add eax, 0Bh           ; Add 11 to eax    |--> a = a + 11
0040101A mov [ebp+var_4], eax   ; Put eax into a --'
0040101D mov ecx, [ebp+var_4]   ; Put a into ecx  -----,
00401020 sub ecx, [ebp+var_8]   ; Subtract b from ecx  |--> a = a - b
00401023 mov [ebp+var_4], ecx   ; Put ecx into a ------'
00401026 mov edx, [ebp+var_4]   ; Put a into edx ------,
00401029 sub edx, 1             ; Subtract 1 from edx  |--> a = a - 1  (a--)
0040102C mov [ebp+var_4], edx   ; Put edx into a ------'
0040102F mov eax, [ebp+var_8]   ; Put b into eax ----,
00401032 add eax, 1             ; Add 1 to eax       |--> b = b + 1  (b++)
00401035 mov [ebp+var_8], eax   ; Put eax into b ----'
00401038 mov eax, [ebp+var_4]   ; Put a into eax --------------,
0040103B cdq                    ; Extend eax to edx:eax        |
0040103C mov ecx, 3             ; Put 3 into ecx               |--> b = a % 3
00401041 idiv ecx               ; Divide edx:eax by ecx        |
00401043 mov [ebp+var_8], edx   ; Put edx (remainder) into b --'
```

## Recognizing if Statements

####Sample Conditional Program

```
int x = 1;
int y = 2;
if (x == y) {
  printf("x equals y.\n");
} else {
  printf("x is not equal to y.\n");
}
```

####Sample Conditional Program Disassembly

```
00401006     mov [ebp+var_8], 1            ; int y = 1;
0040100D     mov [ebp+var_4], 2            ; int x = 2;
00401014     mov eax, [ebp+var_8]          ; Put y into eax 
00401017     cmp eax, [ebp+var_4]          ; Check if x and eax are the same.
0040101A     jnz short loc_40102B          ; If y is not the same as eax, jump
0040101C     push offset aXEqualsY_        ; Put "x equals y.\n" on the stack
00401021     call printf                   ; Call printf, printing the value on the stack.
00401026     add esp, 4                    ; Add 4 to the stack pointer. (Bookkeeping)
00401029     jmp short loc_401038          ; Jump over the next block of code.
0040102B loc_40102B:                       ; 
0040102B     push offset aXIsNotEqualToY   ; Put "x is not equal to y.\n" on the stack
00401030     call printf                   ; Call printf, printing the value on the stack.
```

## Recognizing Nested if Statements

####Sample Nested Conditional Program

```
int x = 0;
int y = 1;
int z = 2;
  if(x == y){
    if(z==0){
      printf("z is zero and x = y.\n");
    }else{
      printf("z is non-zero and x = y.\n");
    }
  }else{
    if(z==0){
      printf("z zero and x != y.\n");
    }else{
      printf("z non-zero and x != y.\n");
  }
}
```

####Sample Nested Conditional Program Disassembly

```
00401006     mov [ebp+var_8], 0            ; int x = 0
0040100D     mov [ebp+var_4], 1            ; int y = 1
00401014     mov [ebp+var_C], 2            ; int z = 2
0040101B     mov eax, [ebp+var_8]          ; Put x in eax
0040101E     cmp eax, [ebp+var_4]          ; Compare y to eax
00401021     jnz short loc_401047          ; If they arent the same, jump to loc_401047
00401023     cmp [ebp+var_C], 0            ; Compare z to 0
00401027     jnz short loc_401038          ; If z is not the same as 0, jump to loc_401038
00401029     push offset aZIsZeroAndXY_    ; Push message  "z is zero and x = y.\n"
0040102E     call printf                   ; Print message "z is zero and x = y.\n"
00401033     add esp, 4                    ; Add 4 to the stack pointer. (Bookkeeping)
00401036     jmp short loc_401045          ; Jump to loc_401045
00401038 loc_401038:                       ; 
00401038     push offset aZIsNonZeroAndX   ; Push message  "z is non-zero and x = y.\n"
0040103D     call printf                   ; Print message "z is non-zero and x = y.\n"
00401042     add esp, 4                    ; Add 4 to the stack pointer. (Bookkeeping)
00401045 loc_401045:                       ; 
00401045     jmp short loc_401069          ; Jump to loc_401069
00401047 loc_401047:                       ; 
00401047     cmp [ebp+var_C], 0            ; Compare z to 0
0040104B     jnz short loc_40105C          ; If z is not the same as 0, jump to loc_40105C
0040104D     push offset aZZeroAndXY_      ; Push message  "z zero and x != y.\n"
00401052     call printf                   ; Print message "z zero and x != y.\n"
00401057     add esp, 4                    ; Add 4 to the stack pointer. (Bookkeeping)
0040105A     jmp short loc_401069          ; Jump to loc_401069
0040105C loc_40105C:                       ; 
0040105C     push offset aZNonZeroAndXY_   ; Push message  "z non-zero and x != y.\n"
00401061     call printf00401061           ; Print message "z non-zero and x != y.\n"
```

## Recognizing Loops

#### Sample for loop Program

```
int i;
for(i=0; i<100; i++) {
  printf("i equals %d\n", i);
}
```

#### Sample for loop Program Disassembly

```
00401004     mov [ebp+var_4], 0      ; int i = 0
0040100B     jmp short loc_401016    ; Jump to loc_401016
0040100D loc_40100D:                 ; 
0040100D     mov eax, [ebp+var_4]    ; Put i in eax
00401010     add eax, 1              ; Add 1 to eax
00401013     mov [ebp+var_4], eax    ; Put eax in i
00401016 loc_401016:                 ; 
00401016     cmp [ebp+var_4], 64h    ; Compare i to 64h (100)
0040101A     jge short loc_40102F    ; If i is greater than or equal to 100, jump to loc_40102F
0040101C     mov ecx, [ebp+var_4]    ; Put i in ecx
0040101F     push ecx                ; Push ecx onto the stack
00401020     push offset aID         ; Push message  "i equals %d\n"
00401025     call printf             ; Print message "i equals %d\n"
0040102A     add esp, 8              ; Add 4 to the stack pointer. (Bookkeeping)
0040102D     jmp short loc_40100D    ; Loop back to loc_40100D
```

#### Sample while loop Program

```
int status=0;
int result = 0;
while(status == 0){
  result = performAction();
  status = checkResult(result);
}
```

#### Sample while loop Program Disassembly

```
00401036     mov [ebp+var_4], 0      ; x = 0
0040103D     mov [ebp+var_8], 0      ; y = 0
00401044 loc_401044:                 ; 
00401044     cmp [ebp+var_4], 0      ; Compare x to 0
00401048     jnz short loc_401063    ; If x is not the same as 0, jump to loc_401063
0040104A     call performAction      ; Call the performAction function.
0040104F     mov [ebp+var_8], eax    ; Put eax in y.
00401052     mov eax, [ebp+var_8]    ; Put y in eax.
00401055     push eax                ; Push eax on the stack.
00401056     call checkResult        ; Call the checkResult function.
0040105B     add esp, 4              ; Add 4 to the stack pointer. (Bookkeeping).
0040105E     mov [ebp+var_4], eax    ; Put eax in x.
00401061     jmp short loc_401044`   ; Jump to loc_401044
```

## Understanding Function Call Conventions

- **Function calls**
  - The stack and the ```call``` instruction are used for function calls.
  - Calling conventions govern the way the function call occurs.
    - The order in which parameters are placed on the stack or in registers
    - Whether the caller or the function called is responsible for cleaning up the stack when the function completes.
  - The calling convention used depends on the compiler, among other factors.
  - The three most common calling conventions you will encounter are ```cdecl```, ```stdcall```, and ```fastcall```.

- **cdecl**
  - Parameters are pushed onto the stack from right to left.
  - The caller cleans up the stack when the function is complete.
  - The return value is stored in the eax register.

- **stdcall**
  - Parameters are pushed onto the stack from right to left.
  - Requires the callee to clean up the stack when the function is complete.
  - The return value is stored in the eax register.
  - The standard calling convention for the Windows API.

- **fastcall**
  - Varies the most across compilers, but it generally works similarly in all cases.
  - The first few arguments (typically two) are passed in registers, with the most commonly used registers being EDX and ECX.
  - Additional arguments are loaded from right to left.
  - The calling function is usually responsible for cleaning up the stack.


#### Sample Function Call Psuedocode

```
int test(int x, int y, int z);
int a, b, c, ret;
ret = test(a, b, c);
```

#### Sample Function Call ```cdecl``` Disassembly

```
push c           ; --,
push b           ;   |---> Parameters pushed right to left
push a           ; --'
call test        ;
add esp, 12      ; ------> Caller cleans up the stack
mov ret, eax     ; ------> Return value stored in eax
```

#### Sample Function Call ```stdcall``` Disassembly
```
push c           ; --,
push b           ;   |---> Parameters pushed right to left
push a           ; --'
call test        ;
                 ; ------> Nothing here. Caller cleans up the stack
mov ret, eax     ; ------> Return value stored in eax
```

#### Push vs. Move
- Compilers may also choose to use different instructions to perform the same operation.
- A common example is when the compiler decides to move rather than push things onto the stack.
- Remember that even when the same compiler is used, there can be differences in calling conventions.

#### Differences in Calling Conventions

```
Assembly Code for a Function Call with Two Different Calling Conventions

,-----------------------------------------------------------------------------------,
| Visual Studio version                 | GCC version                               |
+---------------------------------------+-------------------------------------------+
| 00401746 mov [ebp+var_4], 1           | 00401085 mov [ebp+var_4], 1               |
| 0040174D mov [ebp+var_8], 2           | 0040108C mov [ebp+var_8], 2               |
| 00401754 mov eax, [ebp+var_8]         | 00401093 mov eax, [ebp+var_8]             |
| 00401757 push eax                     | 00401096 mov [esp+4], eax                 |
| 00401758 mov ecx, [ebp+var_4]         | 0040109A mov eax, [ebp+var_4]             |
| 0040175B push ecx                     | 0040109D mov [esp], eax                   |
| 0040175C call adder                   | 004010A0 call adder                       |
| 00401761 add esp, 8                   |                                           |
| 00401764 push eax                     | 004010A5 mov [esp+4], eax                 |
| 00401765 push offset TheFunctionRet   | 004010A9 mov [esp], offset TheFunctionRet |
| 0040176A call ds:printf               | 004010B0 call printf                      |
'-----------------------------------------------------------------------------------'
```

## Switch Statements

#### Analyzing switch Statements
- ```switch``` statements are used to make a decision based on a character or integer.
- They are compiled in two common ways
  - Using the 'if' style.
  - Using jump tables.

#### Three-Option Switch Statement

```
switch(i) {
  case 1:
    printf("i = %d", i+1);
    break;

  case 2:
    printf("i = %d", i+2);
    break;

  case 3:
    printf("i = %d", i+3);
    break;

  default:
    break;
}
```

#### Three-Option Switch Statement Disassembly

```
00401013    cmp [ebp+var_8], 1 -----+--> case 1: JMP to loc_401027
00401017    jz short loc_401027 ----'
00401019    cmp [ebp+var_8], 2 -----+--> case 2: JMP to loc_40103D
0040101D    jz short loc_40103D ----'  
0040101F    cmp [ebp+var_8], 3 --------> case 3: JMP to loc_401053
00401023    jz short loc_401053 ----'  
00401025    jmp short loc_401067 ------> default: JMP to loc_401067
00401027  loc_401027: -----------------,
00401027    mov ecx, [ebp+var_4]       |
0040102A    add ecx, 1                 |
0040102D    push ecx                   |
0040102E    push offset unk_40C000     |---- Handle case 1
00401033    call printf                |
00401038    add esp, 8                 |
0040103B    jmp short loc_401067 ------'
0040103D  loc_40103D: -----------------,
0040103D    mov edx, [ebp+var_4]       |
00401040    add edx, 2                 |
00401043    push edx                   |
00401044    push offset unk_40C004     |---- Handle case 2
00401049    call printf                |
0040104E    add esp, 8                 |
00401051    jmp short loc_401067 ------'
00401053  loc_401053: -----------------,                
00401053    mov eax, [ebp+var_4]       |
00401056    add eax, 3                 |
00401059    push eax                   |
0040105A    push offset unk_40C008     |---- Handle case 3
0040105F    call printf                |
00401064    add esp, 8 ----------------'
```


#### Four-Option Switch Statement

```
switch(i) {
  case 1:
    printf("i = %d", i+1);
    break;

  case 2:
    printf("i = %d", i+2);
    break;

  case 3:
    printf("i = %d", i+3);
    break;

  case 4:
    printf("i = %d", i+4);
    break;

  default:
    break;
}
```

#### Four-Option Switch Statement Disassembly

```
00401016    sub ecx, 1 ---------------------> Subtract one from ecx (range must be from 0 to 3)
00401019    mov [ebp+var_8], ecx -----------> Move ecx into i
0040101C    cmp [ebp+var_8], 3 -------------> Compare i with the number 3
00401020    ja short loc_401082 ------------> If unsigned i is greater than 3. jump to loc_401082
00401022    mov edx, [ebp+var_8] -----------> Move i to edx
00401025    jmp ds:off_401088[edx*4] -------> Jump to the entry in the jump table at off_401088
0040102C  loc_40102C: -------------------,
              .                          |
              .                          |--> Handle case 1
              .                          |
00401040    jmp short loc_401082 --------'
00401042  loc_401042: -------------------,
              .                          |
              .                          |--> Handle case 2
              .                          |
00401056    jmp short loc_401082 --------'
00401058  loc_401058: -------------------,
              .                          |
              .                          |--> Handle case 3
              .                          |
0040106C    jmp short loc_401082 --------'
0040106E  loc_40106E: -------------------,
              .                          |--> Handle case 4
              .                          |
              . -------------------------'
00401082  loc_401082: -------------------,
00401082    xor eax, eax                 |
00401084    mov esp, ebp                 |--> Code after the switch statement.....
00401086    pop ebp                      |
00401087    retn                         |
00401087    _main endp ------------------'
00401088  off_401088   dd offset loc_40102C ---,
0040108C               dd offset loc_401042    |--- Jump table for case blocks.
00401090               dd offset loc_401058    |
00401094               dd offset loc_40106E ---'
```

## Arrays

#### Disassembling Arrays
- Arrays are used by programmers to define an ordered set of similar data items.
- Malware can use an array of pointers to strings that contain hostnames used as options for connections.

#### Sample 'Array' Program

```
int b[5] = {123, 87, 487, 7, 978};
void main() {
  int i;
  int a[5];
  for(i = 0; i<5; i++) {
    a[i] = i;
    b[i] = i;
  }
}
```

#### Sample 'Array' Program Disassembly

```
00401006        mov [ebp+var_18], 0 -----------> Move 0 into var_18(i)
0040100D        jmp short loc_401018 ----------> Jump to loc_00401018
0040100F    loc_40100F:
0040100F        mov eax, [ebp+var_18] ---------> Move var_18(i) into EAX
00401012        add eax, 1 --------------------> Increment EAX
00401015        mov [ebp+var_18], eax ---------> Move EAX back into var_18(i)
00401018        loc_401018:
00401018        cmp [ebp+var_18], 5 -----------> Compare var_18(i) to 5
0040101C        jge short loc_401037 ----------> Exit the loop if var_18(i) is greater or equal to 5
0040101E        mov ecx, [ebp+var_18] ---------> Move var_18(i) into ECX
00401021        mov edx, [ebp+var_18] ---------> Move var_18(i) into EDX
00401024        mov [ebp+ecx*4+var_14], edx ---> var_14 is the location of the local array. Store EDX in it.
00401028        mov eax, [ebp+var_18] ---------> Move var_18(i) into EAX
0040102B        mov ecx, [ebp+var_18] ---------> Move var_18(i) into ECX
0040102E        mov dword_40A000[ecx*4], eax --> dword_40A000 is the location of the global array. Store EAX in it.
00401035        jmp short loc_40100F ----------> Jump back to loc_40100F for the loop.
```

## Structs

#### Identifying Structs
- Structures (or structs, for short) are similar to arrays, but they comprise elements of different types.
- Structures are commonly used by malware authors to group information.
- Structures (like arrays) are accessed with a base address used as a starting pointer.
- It is difficult to determine whether nearby data are part of the same struct or they just happen to be next to each other.
- Depending on the context, your ability to identify structs can have a significant impact on your ability to analyze malware.

#### Sample 'Struct' Program

```
struct my_structure {
  int x[5];
  char y;
  double z;
};

struct my_structure *gms;
void test(struct my_structure *q) {
  int i;
  q->y = 'a';
  q->z = 15.6;
  for(i = 0; i<5; i++){
    q->x[i] = i;
  }
}

void main() {
  gms = (struct my_structure *) malloc(
  sizeof(struct my_structure));
  test(gms);
}
```

#### Sample 'struct' Program 'main' function Disassembly

```
00401050     push ebp ------------------> Bookkeeping: Save the original base pointer
00401051     mov ebp, esp --------------> Bookkeeping: Move esp into ebp
00401053     push 20h ------------------> Push the size of the struct onto the stack as the function parameters.
00401055     call malloc ---------------> Call malloc()
0040105A     add esp, 4 ----------------> Cleanup the stack 
0040105D     mov dword_40EA30, eax -----> eax contians the address of allocated memory. Move eax into gms
00401062     mov eax, dword_40EA30 -----> Move gms into eax (unneeded)
00401067     push eax ------------------> Push eax on the stack as a parameter.
00401068     call sub_401000 -----------> Call test()
0040106D     add esp, 4 ----------------> Bookkeeping: Cleanup the stack 
00401070     xor eax, eax --------------> zero out eax
00401072     pop ebp -------------------> Bookkeeping: Restore the original base pointer
00401073     retn ----------------------> Return to the calling method.
```

#### Sample 'struct' Program 'test' function Disassembly

```
00401000     push ebp -----------------------> Bookkeeping: Save the original base pointer
00401001     mov ebp, esp -------------------> Bookkeeping: Move esp into ebp
00401003     push ecx -----------------------> ???????
00401004     mov eax,[ebp+arg_0] ------------> Move arg_0(q) into eax
00401007     mov byte ptr [eax+14h], 61h ----> Move 'a' into [eax+14h](q->y)
0040100B     mov ecx, [ebp+arg_0] -----------> Move arg0(q) into ecx
0040100E     fld ds:dbl_40B120 --------------> Load dbl_40B120(15.6) onto the floating point stack
00401014     fstp qword ptr [ecx+18h] -------> Store the value on top of the floating point stack into [ecx+18h](q->z)
00401017     mov [ebp+var_4], 0 -------------> Move 0 into var_4(i)
0040101E     jmp short loc_401029 -----------> Jump to loc_401029 unconditionally
00401020   loc_401020:
00401020     mov edx,[ebp+var_4] ------------> Move var_4(i) into edx.
00401023     add edx, 1 ---------------------> Increment edx
00401026     mov [ebp+var_4], edx -----------> Move edx into var_4(i)
00401029   loc_401029:
00401029     cmp [ebp+var_4], 5 -------------> Compare var_4(i) to 5
0040102D     jge short loc_40103D -----------> If 5 is greater than or equal to var_4(i), jump to loc_40103D
0040102F     mov eax,[ebp+var_4] ------------> Move var_4(i) into eax
00401032     mov ecx,[ebp+arg_0] ------------> Move arg_0(gms) into ecx
00401035     mov edx,[ebp+var_4] ------------> Move var_4(i) into edx
00401038     mov [ecx+eax*4],edx ------------> Move edx into [ecx+eax*4](q->x[i])
0040103B     jmp short loc_401020 -----------> Jump to loc_401020 unconditionally
0040103D   loc_40103D:
0040103D     mov esp, ebp -------------------> Bookkeeping: Restore esp from ebp.
0040103F     pop ebp ------------------------> Bookkeeping: Restore the original base pointer
00401040     retn ---------------------------> Return to the calling method.
```

## Linked Lists

#### Analyzing Linked List Traversal
- A linked list is a data structure that consists of a sequence of data records.
- Each record includes a field that contains a reference (link) to the next record in the sequence.
- The linked items can differ from the order the data items are stored in memory or on disk.
- Linked lists allow the insertion and removal of nodes at any point in the list.



#### Sample 'Linked List Traversal' Program

```
struct node {
  int x;
  struct node * next;
};

typedef struct node pnode;

void main() {
  pnode * curr, * head;
  int i;
  head = NULL;
  for(i=1;i<=10;i++) {
    curr = (pnode *)malloc(sizeof(pnode));
    curr->x = i;
    curr->next = head;
    head = curr;
  }

  curr = head;
  while(curr) {
    printf("%d\n", curr->x);
    curr = curr->next ;
  }
}
```

#### Sample 'Linked List Traversal' Program Disassembly

```
0040106A     mov [ebp+var_8], 0 -------------------------------> Move 0 into var_8(head)
00401071     mov [ebp+var_C], 1 -------------------------------> Move 1 into var_C(i)
00401078   loc_401078:
00401078     cmp [ebp+var_C], 0Ah -----------------------------> Compare var_C(i) to 10
0040107C     jg short loc_4010AB ------------------------------> If var_C(i) is greater 10, jump to loc_4010AB
0040107E     mov [esp+18h+var_18], 8 --------------------------> Move 8 into [esp+18h+var_18] as the function argument.
00401085     call malloc --------------------------------------> Call malloc
0040108A     mov [ebp+var_4], eax -----------------------------> Move eax into var_4(curr). This is the address of allocated memory from alloc.
0040108D     mov edx, [ebp+var_4] -----------------------------> Move var_4(curr) into edx
00401090     mov eax, [ebp+var_C] -----------------------------> Move var_C(i) into eax
00401093     mov [edx], eax -----------------------------------> Move eax into [edx](curr->x)
00401095     mov edx, [ebp+var_4] -----------------------------> Move var_4(curr) into edx
00401098     mov eax, [ebp+var_8] -----------------------------> Move var_8(head) into eax 
0040109B     mov [edx+4], eax ---------------------------------> Move eax(head) into [edx+4](curr->next)
0040109E     mov eax, [ebp+var_4] -----------------------------> Move var_4(curr) into eax
004010A1     mov [ebp+var_8], eax -----------------------------> Move eax(curr) into var_8(head)
004010A4     lea eax, [ebp+var_C] -----------------------------> Load the address of var_C(i) into eax
004010A7     inc dword ptr [eax] ------------------------------> Increment eax(i)
004010A9     jmp short loc_401078 -----------------------------> Jump to loc_401078, continuing the loop.
004010AB   loc_4010AB:
004010AB     mov eax, [ebp+var_8] -----------------------------> Move var_8(head) into eax
004010AE     mov [ebp+var_4], eax -----------------------------> Move eax(head) into var_4(curr)
004010B1   loc_4010B1:
004010B1     cmp [ebp+var_4], 0 -------------------------------> Compare var_4(curr) to 0
004010B5     jz short locret_4010D7 ---------------------------> If var_4(curr) is zero, jump to locret_4010D7
004010B7     mov eax, [ebp+var_4] -----------------------------> Move [var_4](curr) into eax
004010BA     mov eax, [eax] -----------------------------------> Move [eax] into eax
004010BC     mov [esp+18h+var_14], eax ------------------------> Move eax into [esp+18h+var_14] as a function argument.
004010C0     mov [esp+18h+var_18], offset aD ; "%d\n" ---------> Move offset aD into [esp+18h+var_18] as a function argument.
004010C7     call printf --------------------------------------> Call printf
004010CC     mov eax, [ebp+var_4] -----------------------------> Move [var_4](curr) into eax
004010CF     mov eax, [eax+4] ---------------------------------> Move [eax+4](curr->next) into eax
004010D2     mov [ebp+var_4], eax -----------------------------> Move eax(curr->next) into [var_4](curr)
004010D5     jmp short loc_4010B1 -----------------------------> Jump to loc_4010B1, continuing the loop.
```
