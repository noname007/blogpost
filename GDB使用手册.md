The following commands help you find out which language is the working language, and also what language source files were written in.

show language
Display the current working language. This is the language you can use with commands such as print to build and compute expressions that may involve variables in your program. 
info frame
Display the source language for this frame. This language becomes the working language if you use an identifier from this frame. See Information about a Frame, to identify the other information listed here. 
info source
Display the source language of this source file. See Examining the Symbol Table, to identify the other information listed here.
In unusual circumstances, you may have source files with extensions not in the standard list. You can then set the extension associated with a language explicitly:

set extension-language ext language
Tell gdb that source files with extension ext are to be assumed as written in the source language language. 
info extensions
List all the filename extensions and the associated languages.



	* b main - Puts a breakpoint at the beginning of the program
	* b - Puts a breakpoint at the current line
	* b N - Puts a breakpoint at line N
	* b +N - Puts a breakpoint N lines down from the current line
	* b fn - Puts a breakpoint at the beginning of function "fn"
	* d N - Deletes breakpoint number N
	* info break - list breakpoints
	* r - Runs the program until a breakpoint or error
	* c - Continues running the program until the next breakpoint or error
	* f - Runs until the current function is finished
	* s - Runs the next line of the program
	* s N - Runs the next N lines of the program
	* n - Like s, but it does not step into functions
	* u N - Runs until you get N lines in front of the current line
	* p var - Prints the current value of the variable "var"
	* bt - Prints a stack trace
	* u - Goes up a level in the stack
	* d - Goes down a level in the stack
	* q - Quits gdb

