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
	
	```



