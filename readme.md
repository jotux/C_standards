### C language syntax and language use standards

### 1 Naming

#### 1.1 Files

File names are to be all lowercase and use underscores (_). Names shall be descriptive and specific.

>Example 1.1a - Acceptable file names for code and header files

    wireless_comm.c
    hardware_config.h
    printer.c

#### 1.2 Functions

Regular Function names are mixed-case with no underscores. Functions that get or set specific variables (accessors or mutators) are lowercase with underscores and have names that include the variable(s) they access.

>Example 1.2a - Acceptable regular function names

    MyUsefulFunction()
    ParseData()

>Example 1.2b - Acceptable accessor/mutator function names

    set_error_count()
    get_error_count()

#### 1.3 Variables

Variables shall be all lowercase with underscores to separate words. Names should be related to their function, clear, and as long as is needed to express their function. Do not use abbreviations unless they are universally understood.

>Example 1.3a - Acceptable variable names

    baseline_average
    local_interrupt_count

>Example 1.3b - Unacceptable variable names

    bline_av
    int_cnt

#### 1.4 Types

Type names are mixed-case with no underscores.

>Example 1.4a - Acceptable type names

    class MyUsefulClass { …
    struct MyStruct { …
    typedef … SpecialType;    
    enum MyErrors { …

#### 1.5 Defines and Macros

Defines and macros are to be all uppercase with underscores separating words.

>Example 1.5a - Acceptable define names

    #define MAX_ALLOWED_ERRORS 3
    #define DEFAULT_TIMEOUT_SECONDS 10

>Example 1.5b - Acceptable macro names

    #define OPEN_PORT() {code…}
    #define GREEN_LED_OFF() {code…}

### 2 Formatting

#### 2.1 Spaces instead of tabs

Spaces shall be used at all times instead of tabs. Tabs should be replaced with FOUR(4) spaces. Most editors have an option to convert tabs to spaces. Using spaces instead of tabs ensures that code will look consistent from one computer to the next and print properly.

#### 2.2 One statement per line

Only one statement is allowed per line. This makes variables and code easier to find and document.

>Example 2.2a - unacceptable declaration of multiple variables on one line

    unsigned char a, b, c, d;

>Example 2.2b - acceptable declaration of multiple variables

    unsigned char a = 0;    
    unsigned char b = 0;    
    unsigned char c = 0;    
    unsigned char d = 0;

#### 2.3 Parenthesis, Argument, and Operator spacing

Spaces shall appear on both sides of parenthesis (except at the end of a line). Operators shall have a space on either side of them. Operators shall not have a space between themselves and the argument they operate on.

>Example 2.3a - Assignment with multiple operators, arguments, and parenthesis.

    foo = ((bar1 | bar2) & bar3) / bar4;

>Example 2.3b - Operator spacing

    foo = bar1 + ~bar2 - (bar3 * bar4);

#### 2.4 while, do while, and for loops

All code statements within loops shall be encompassed by brackets even if they are single statements. Comments should be added to closing braces of loops to document where the closing brace originates.

>Example 2.4a - while loop formatting

    while ((a < b) || (b < c))   // comment
    {
       code…
    }    // end while

>Example 2.4b - do while loop formatting

    do
    {
       code…
    }while ((a < b) && (b < c));    // comment

>Example 2.4c - for loop formatting

    for (a = 0;a < MAX_LOOP_CNT;a += LOOP_INC)    // comment
    {
       code…
    }    //end for loop

>Example 2.4d - A while loop with a single line of associated code

    while (a < b)    // comment
    {
       a++;
    }    // end while

Empty loops shall not be terminated with a single semicolon. Use brackets with associated comments explaining why the loop has no functioning code or use continue.

>Example 2.4e - while loops with no body

    while (condition)
    {
        // wait for this condition to return false
    }

    while (condition) continue;    // comment

#### 2.5 if, else if, and else statements

All code statements within if statements shall be encompassed by brackets even if they are single statements. Comments should be added to closing braces of if statements to document where the closing brace originates.

>Example 2.5a - if, if-else, and else statement formatting

    if (a == b)         // comment
    {
       code…
    }
    else if (a < b)     // comment
    {
       code…
    }
    else                // comment
    {  
       code…
    }    // end a==b if

>Example 2.5b - An if statement with a single line of associated code

    if (a < b)    // comment
    {
       a++;
    }

#### 2.6 switch statements

Switch statements are to have the case statements indented one level out from the switch. Fall-throughs must be clearly documented. A default case is recommended but not required.

>Example 2.6a - A switch statement with multiple cases including a fall-through

    Switch (foo)
    {
       case bar1:    // comment  
           code…  
           break;  
       case bar2:    // OMG FALL THROUGH  
           code…  
       case bar3:    // comment  
           code…  
           break;  
       case default:  
           break;
    }    // end switch foo

#### 2.7 Ternary operator

Ternary operators are sometimes useful in making code concise and readable. If possible, try to restrict ternary operations to single lines.

>Example 2.7a - acceptable ternary usage

    foo = (bar > 10) ? 0 : 1;

#### 2.8 Commenting

Use either // or /* */, as long as you are consistent. // is much more common for C commenting.

### 3 Documentation

#### 3.1 Files

The first line of every file shall indicate the start of the file; the last line should indicate the end.

Generally .h files will have a general overview of the code and how to use it. A .c file will contain more information specifically describing how the code operates or specific algorithms and how they were implemented. When making changes to code, document the change in your source code repository softwareor in a .txt file accompanying your source code, do not document the changes in .h or .c files.

#### 3.3 TODO

Use TODO comments to document code that is in-progress, temporary, working but should be improved, or good enough but not perfect. TODOs should include the string TODO in all caps, followed by the name of the programmer who made the comment. TODO comments provide an easy and searchable way to document code you'd like to improve at a later time.

>Example 3.3a - correct TODO comment usage

    // TODO(Joe): remove equation here and use lookup table instead
    // TODO(Bob): add exception handling to this loop

### 4 Language Use

#### 4.1 Macros

Macros shall always be encompassed by brackets. Many problems that arise from using macros are associated with not using brackets to encompass them. Macro use should be avoided whenever possible. If you need a macro-like functionality use inline functions instead.

>Example 4.1a - A correctly formatted macro to return the maximum of two values

    #define MAX(a,b) {(a > b) ? a : b;}

>Example 4.1b - The same functionality implemented as an inline function

    inline int max(int a, int b)
    {
        return a > b ? a : b;
    }

#### 4.2 Magic numbers

Magic numbers are arbitrary numbers in C files that are meaningless to anyone reading the code that isn't the original author. Magic numbers are forbidden. The only numbers allowed in C files are 0 or 1. In most cases 0 and 1 should be further defined as FALSE and TRUE to ensure code clarity. There can be exceptions to this rule, such as code specific to a piece of hardware, but generally all numbers should be defined in the header file associated with a specific C file.

>Example 4.2a - Correct use of definition instead of a Magic number

    if (var <= MINIMUM_SPECIFIC_THRESHOLD)

#### 4.3 Hardware-specific code

All hardware specific definitions are to be in header files. Hardware specific code is strictly forbidden in .C files. Ideally you should have a single file defining all hardware interaction, though sometimes you will use imported libraries with their own associated hardware configuration. The only exception to this rule is for functions that initialize hardware.

>Example 4.3a - Correctly defining hardware

    #define RED_LED_PORT     P1OUT
    #define RED_LED_PIN      BIT0

#### 4.4 Header files

All C files should have an associated header file. The only exception would be special source files that contain your main function. Header files contain function prototypes, defines, macros, and the associated documentation on how to use the functions in the associated C file. Remember, documentation within header files explains how to use the functions and documentation in the C files explains how the code works. All header files will have #define guards to prevent multiple inclusions. The format of the symbol name should beFILENAME_H.

>Example 4.4a - #define guard for hardware_init.h

    #ifndef HARDWARE_INIT_H    
    #define HARDWARE_INIT_H
    …
    #endif //HARDWARE_INIT_H

#### 4.5 Initialize all variables

All variables must be initialized, always.

#### 4.6 Boolean Conditionals

All boolean conditionals shall be encompassed by parenthesis to prevent operator-ordering errors.

#### 4.7 Consistency

When working on code that follows a different style maintain the coding style of the code you are working on.

