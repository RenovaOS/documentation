GovOS Programming Guidelines
============================
GovOS follows a strict programming style to keep the code consistent and readable.

Indentation and Spacing
-----------------------
Indents should be three spaces, no tab characters.  In Makefiles, tabs are acceptable.  
There should always be a space after a comma, and before and after operators.

```C
int main(int argc, char ** argv) {
   printf("Hello, world!\n");
   return 0;
}
```

In a switch-case, the case statements must be indented.

```C
switch (i) {
   case 1:
      printf("i == 1\n");
      break;
   default:
      printf("i != 1\n");
      break;
}
```

C Preprocessor statements must not be indented.

```C
#ifndef _HELLOWORLD_H
#define _HELLOWORLD_H
   void helloWorld();
#ifdef ADVHELLOWORLD
   void advHelloWorld();
#endif //ADVHELLOWORLD
#endif //_HELLOWORLD_H
```

There must be (only) one blank line between the three main sections of a function and between
functions.  These three sections are the variable declarations, the code block, and the single
`return` statement.
Additional blank lines can be added for readability, but only one at a time.

```C
int foo(int i) {
   int j = i / 2;

   for(j = 0; j < 1; ++j) {
      printf("THIS IS FOO\n");
   }

   return j;
}

int bar() {
   printf("This is a much better function than foo.\n");
}
```

Braces
------
Braces should start on the same line as the previous statement in the so-called "Egyptian" style.

```C
int main(int argc, char ** argv) {
   if (argc == 1) {
      printf("These are not the arguments you're looking for.\n");
   }
   else {
      printf("These ARE the arguments you're looking for!\n");(
   }

   return 0;
}
```

Line Length
-----------
100 characters per line, max.  If you go over, goto "Goto Statements".

Loops
-----
All counter variables must be declared before the loop.

```C
void foo() {
   int j;

   for(j = 0; j < 1; ++j) {
      printf("THIS IS FOO\n");
   }
}
```

Captialisation
--------------
Function names should be camel-cased.  Variable names should be underscored.  
Preprocessor defines should be in all caps and underscored, while directives
should be lowercase.

```C
void fooBar();

int score_counter;

#define VERSION "1.0"
```

Conditionals
------------
If statements should be on their own line, with a space between the if and the condition.  The
condition should be flush with the parentheses. For an else if statement, the else and the else
should be on the same line, one line after the closing brace of the previous if statement.
This is also the case with all keywords.

```C
if (condition) {
   dontDoStuff();
}
else if (condition2) {
   doStuff();
}
```

Data Structures
---------------
Structs should be names with an _s and be typedef'd to their name, but with an _t.  When instantiating 
a struct, the variables should be explicitly initialized.

```C
typedef struct node_s {
   node_s* next;
   int data;
} node_t;
```

Comments
--------
Code should be self-documenting.  Excessive comments should not replace good variable naming.
There should be a comment block before every function describing the purpose, use, and 
possible side effects of the function (especially if any memory is allocated in the function).

At the beginning of every file, the purpose of the file should be present.  Each time you edit
a file, you should ensure that your name is in this comment block, as well as the date in 
international format (for example, 12 Apr 2013).  

Inline comments should go on the line before what they comment and should be indented to 
the same column.

Define Guards
-------------
All header files must use define guards to prevent double inclusion.  The naming convention of 
the define is `_NAMEOFFILE_H`.

Goto Statements
---------------
![If you are still unsure, this means no goto's.](http://imgs.xkcd.com/comics/goto.png "If you are still unsure, this means no goto's.")
