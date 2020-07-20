# Buffer Overflow Attack with Example
A buffer is a temporary area for data storage. When more data (than was originally allocated to be stored) gets placed by a program or system process, the extra data overflows. It causes some of that data to leak out into other buffers, which can corrupt or overwrite whatever data they were holding.

In a buffer-overflow attack, the extra data sometimes holds specific instructions for actions intended by a hacker or malicious user; for example, the data could trigger a response that damages files, changes data or unveils private information.

Attacker would use a buffer-overflow exploit to take advantage of a program that is waiting on a user’s input. There are two types of buffer overflows: stack-based and heap-based. Heap-based, which are difficult to execute and the least common of the two, attack an application by flooding the memory space reserved for a program. Stack-based buffer overflows, which are more common among attackers, exploit applications and programs by using what is known as a stack: memory space used to store user input.

Let us study some real program examples that show the danger of such situations based on the C.
In the examples, we do not implement any malicious code injection but just to show that the buffer can be overflow. Modern compilers normally provide overflow checking option during the compile/link time but during the run time it is quite difficult to check this problem without any extra protection mechanism such as using exception handling.

{ // A C program to demonstrate buffer overflow 
#include <stdio.h> 
#include <string.h> 
#include <stdlib.h> 
  
int main(int argc, char *argv[]) 
{ 
  
       // Reserve 5 byte of buffer plus the terminating NULL. 
       // should allocate 8 bytes = 2 double words, 
       // To overflow, need more than 8 bytes... 
       char buffer[5];  // If more than 8 characters input 
                        // by user, there will be access  
                        // violation, segmentation fault 
  
       // a prompt how to execute the program... 
       if (argc < 2) 
       { 
              printf("strcpy() NOT executed....\n"); 
              printf("Syntax: %s <characters>\n", argv[0]); 
              exit(0); 
       } 
  
       // copy the user input to mybuffer, without any 
       // bound checking a secure version is srtcpy_s() 
       strcpy(buffer, argv[1]); 
       printf("buffer content= %s\n", buffer); 
  
       // you may want to try strcpy_s() 
       printf("strcpy() executed...\n"); 
  
       return 0; 
}* 
