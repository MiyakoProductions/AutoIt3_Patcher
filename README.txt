███████╗ ██████╗██╗  ██╗██████╗ ██╗     ██████╗ ███████╗
██╔════╝██╔════╝██║  ██║██╔══██╗██║     ╚════██╗╚════██║
███████╗██║     ███████║██████╔╝██║      █████╔╝    ██╔╝
╚════██║██║     ╚════██║██╔══██╗██║      ╚═══██╗   ██╔╝ 
███████║╚██████╗     ██║██║  ██║███████╗██████╔╝   ██║  
╚══════╝ ╚═════╝     ╚═╝╚═╝  ╚═╝╚══════╝╚═════╝    ╚═╝  
                                                        
    ██████╗ ██████╗ ██╗   ██╗ ██╗██╗     ███████╗       
    ██╔══██╗╚════██╗██║   ██║███║██║     ██╔════╝       
    ██║  ██║ █████╔╝██║   ██║╚██║██║     ███████╗       
    ██║  ██║ ╚═══██╗╚██╗ ██╔╝ ██║██║     ╚════██║       
    ██████╔╝██████╔╝ ╚████╔╝  ██║███████╗███████║       
    ╚═════╝ ╚═════╝   ╚═══╝   ╚═╝╚══════╝╚══════╝
	
█████████████████████████████████████████████████████████

This is a simple release for educational purposes.
The project is designed to replicate an old skool patcher
for cracking software.

Included:
+ CRKME1.exe - Crack Me #1 by Phrozen Crew
+ Full source for the patcher in AutoIt3
+ Patcher.exe - Compiled executable

= Finding the address of the target program to patch =
I wanted to briefly cover how the address in memory that
cracked the program is found.

To begin, we will be using OlyDbg for this example.
Other debuggers and disassemblers such as IDA Pro
however work just as well.

1. Open OlyDbg and create the process for CRKME1.exe
2. Run all threads.
3. In the assembly window, search for the binary string
   "Not Registered"
4. Above our string, we should see a couple jumps.
   Specifically we are looking for a JE (Jump if Equals)
   directly above our string.
5. Double click on the JE and reassemble it as JNE.
6. Test for success by typing anything into the input
   box.
7. Write down the address shown to the left of the
   assembly instruction.
8a. Open the instruction in the Hex View. Write down the
   offset of the byte. Then in a hex editor, go to the
   offset and change the 74 to a 75. Hit save and the
   file is permanently patched.
8b. Copy the memory address of the assembly instruction
   shown to the left of the instruction. Then in our
   patcher's source, apply the address inside of a
   WriteMemory() function.