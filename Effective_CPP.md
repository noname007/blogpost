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
	- compiles refuse  generate  change reference with different value and const variable
- Explicitly disallow the use of compiler-generated functions you do not want
	- declarae not define   && the easier way private inherit 
- Declare destructors virtual in polymorphic base classes
	- If a class does not contain virtual functions, that often indicates it is not meant to be used as a base class. When a class is not intended to be a base class, making the destructor virtual is usually a bad idea.
	- Polymorphic base classes should declare virtual destructors. If a class has any virtual functions, it should have a virtual destructor.
	- Classes not designed to be base classes or not designed to be used polymorphically should not declare virtual destructors.
- Prevent Exceptions from leaving destructors
- Never call virtual functions during construction or destruction 


