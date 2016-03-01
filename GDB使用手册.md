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