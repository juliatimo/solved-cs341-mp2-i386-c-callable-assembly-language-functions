Download Link: https://assignmentchef.com/product/solved-cs341-mp2-i386-c-callable-assembly-language-functions
<br>
The purpose of this assignment is to gain some familiarity with writing C callable functions that use assembly language. Copy all files from /courses/cs341/f20/cheungr/mp2/ to your mp2 subdirectory of cs341.Use the provided makefile for all builds except where instructed otherwise. As in mp1, use the new environment to build all your executables and use VMs to run and debug your code.

<ol>

 <li><strong><u>DESCRIPTION:</u></strong></li>

</ol>

<strong><u>Part 1: Program to count the occurrence of a user entered character in a string</u> </strong>




<ol>

 <li>Write a C callable assembler function that counts the number of characters in a string. The function should work for any string and character. The address of the string and character to be counted are passed as arguments according to the C function prototype:</li>

</ol>

int count (char *string, char c);




Since there are arguments, your assembly function should use a stack frame. It should return the count to the calling C program in %eax. Use 32-bit quantities for all data. Even though chars have only 8 bits, they are stored in memory (and on the stack) as 32 bits in “little endian” format. If the 32-bit value is moved from memory to a register, the char value is available in the 8 least significant bits of the register.

You are given a C calling program(countc.c) in mp2/part1/ that calls count to count the number of a user-entered character in a user-entered string and prints the result. The C code “driver” is in countc.c. Put your assembly code in count.s. Then build it using the provided makefile by invoking “make A=count”.

Capture a run of your program in the script file mp2_part1_typescript. The file will be captured in the vserver VM and later transferred to your CS341 homework directory for grading. Please provide the script showing a run with a breakpoint set using either Tutor or remote gdb where the count is incremented, showing the count (in a register) each time the breakpoint is hit, just before the increment is made. In the script, show how you determined where to set the breakpoint, i.e., how you determined where the increment instruction is located in memory.

<strong><u>Part 2: Program to print binary characters</u> </strong>




<ol start="2">

 <li>You are given a C calling program (printbinc.c) in mp2/part2+3/. Call your file printbin.s. The C caller for this program provides a char to the assembly function printbin. It asks the user for a hex number between 0 and 0xff, converts the input from an ASCII string to a char value, passes it to printbin as an argument, and displays the returned string which should be the ASCII characters for the binary value, e.g. for entry of the hex value 0x3d, you will get the printout:</li>

</ol>

“The binary format for character = is 0011 1101” You can see the function prototype for the printbin function in the calling C code.




The function printbin should be C callable using a stack frame and call an assembly language subprogram “donibble” that is not required to be C callable. Avoiding the use of stack frames is one way assembly code can be more efficient than C compiler generated code. The function printbin needs to declare space in the .data section for storage of a string to be returned and return the address of that location in the %eax. While processing the bits of the input argument, keep a pointer to the string in an available register. printbin and donibble can store an ascii character 0x20, 0x30, or 0x31 in the string indirectly via that register and then increment the pointer in that register until the entire return string has been filled in.




The donibble function handles one half of the char value producing the four ASCII character (0/1) for the bits in one hex digit. Printbin should call donibble twice once with each nibble to be processed in half of an available register, e.g. the %al. Donibble should scan the 4 bits of the register and move an appropriate ascii code into the string for each bit. Printbin adds the space between the two nibbles.




In file mp2_part2_typescript, show a run of printbin on the tutor VM to display 0xab, and then a run with a breakpoint set at the helper function, to prove that it is called exactly twice. You can use Tutor or remote gdb here as you wish.




<strong><u>Part 3:  Program to copy n characters of a string</u> </strong>




<ol start="3">

 <li>Write a C-callable assembler version of the library strncpy function called mystrncpy (to avoid conflicts with the library version) that copies the contents of one string to a user provided array and returns a pointer to the provided array. The function prototype is:</li>

</ol>




char *mystrncpy(char *s, char *ct,  int n);




Write your code in a source file named strncpy.s. The provided C driver (strncpyc.c) in mp2/part2+3/ takes user entered input for the source string and checks both the pointer returned and the effect of the copy. Choose test cases that exercise different possibilities in the logic of your code, e.g. a null string. What would happen if you choose a string longer than the destination array in the C driver?




In file mp2_part3_typescript, show a run of strncpy on the tutor VM to display the source string copied and the pointer returned.