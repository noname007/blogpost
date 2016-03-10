- View C++ as a federation of language
- Prefer consts ,enums , and inlines to #defines
	- prefer the compiler to the preprocessor
	- in-class initialization is allowed only for integeral types and only for constan
	-  enum hacking
- Use const whenever possible
	
	```
	char greeting[] = "Hello";
	char *p = greeting; //non-const pointer , non-const data
	const char *p = greeting; //non - const pointer ,const data 
	char * const p = greeting; //const pointer, non-const data
	const char* const p =greeting; // const data,const pointer
	
	// if the word const appears  to the left of the asterisk ,what's pointed to is constant;if the word const appears to the right of the asterisk ,the pointer itself is constant; if const appears on both sides, both are constant
	```
	
- Make sure that  objectas are initalized before they're used 
	- sometimes the initialization list must be used, even for built-in types . For example ,data members that are const or references must be initialized.
	- to avoid using objects before they're initialized, you need to do only three things .First ,manualy initialize non-member objects of build-in types.Second ,use member initialization lists to initialize all parts of an object.Finally , design around the initialization order uncertainty that afflicts non-local static objects defined in separate translation units.
- Know what functions C++ silently writes and calls


