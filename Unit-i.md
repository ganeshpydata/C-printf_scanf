/* ============================================================
   c_basics_demo.c
   Demonstrates: Character set, C Tokens, Keywords & Identifiers,
   Constants, Variables, Data Types, Declaration of Variables,
   Storage Classes, Assigning Values, Symbolic Constants (#define),
   const Variables, and volatile Variables.
   ============================================================ */

#include <stdio.h>     /* Preprocessor directive -> a C Token */

/* ---- Symbolic Constant (defined using the preprocessor) ---- */
#define PI 3.14159      /* PI is a symbolic constant, not a variable */
#define MAX_STUDENTS 50

/* ---- Global variable with EXTERN storage class (file scope) ---- */
int totalCalls = 0;      /* visible to every function in this file */

/* Function prototype — demonstrates an Identifier (function name) */
void showStorageClasses(void);

int main(void)
{
    /* ---------------- KEYWORDS & IDENTIFIERS ----------------
       'int', 'float', 'char', 'const', 'volatile', 'return' are
       KEYWORDS (reserved words).
       'age', 'height', 'grade' etc. below are IDENTIFIERS
       (user-defined names). ---------------------------------- */

    /* ---------------- VARIABLES & DATA TYPES ----------------- */
    int    age      = 21;          /* integer data type        */
    float  height   = 5.9f;        /* floating-point data type */
    double weight   = 62.345;      /* double precision float   */
    char   grade    = 'A';         /* character data type      */
    unsigned int roll = 101u;      /* unsigned integer type    */

    /* ---------------- DECLARATION WITHOUT INITIALISATION ----- */
    int marks;                     /* declared, assigned below */

    /* ---------------- ASSIGNING VALUES TO VARIABLES ---------- */
    marks = 95;                    /* assignment statement     */

    /* ---------------- CONSTANTS (C TOKENS: literals) --------- */
    int   integerConstant   = 100;        /* integer constant   */
    float floatConstant     = 3.14f;      /* real/float constant*/
    char  charConstant      = 'Z';        /* character constant */
    char  stringConstant[]  = "Hello C";  /* string constant    */

    /* ---------------- DECLARING A VARIABLE AS CONSTANT -------- */
    const float GRAVITY = 9.8f;    /* value cannot change after this */
    /* GRAVITY = 10.0f;   <-- would cause a compile-time error */

    /* ---------------- DECLARING A VARIABLE AS VOLATILE -------- */
    volatile int sensorValue = 0;  /* tells compiler: this value may
                                       change unexpectedly (hardware,
                                       interrupt, another thread),
                                       so never cache it in a register */

    /* ---------------- USING A SYMBOLIC CONSTANT --------------- */
    float radius = 4.0f;
    float area   = PI * radius * radius;   /* PI expands to 3.14159 */

    /* ---------------- DISPLAYING EVERYTHING (printf token) ---- */
    printf("----- Variables and Data Types -----\n");
    printf("Age (int)        : %d\n", age);
    printf("Height (float)   : %.1f\n", height);
    printf("Weight (double)  : %.3lf\n", weight);
    printf("Grade (char)     : %c\n", grade);
    printf("Roll (unsigned)  : %u\n", roll);
    printf("Marks (assigned) : %d\n", marks);

    printf("\n----- Constants -----\n");
    printf("Integer constant : %d\n", integerConstant);
    printf("Float constant   : %.2f\n", floatConstant);
    printf("Char constant    : %c\n", charConstant);
    printf("String constant  : %s\n", stringConstant);

    printf("\n----- const and Symbolic Constant -----\n");
    printf("GRAVITY (const)  : %.1f\n", GRAVITY);
    printf("MAX_STUDENTS     : %d\n", MAX_STUDENTS);
    printf("Area using PI    : %.2f\n", area);

    printf("\n----- volatile demonstration -----\n");
    sensorValue = 25;               /* value can change anytime */
    printf("sensorValue      : %d\n", sensorValue);

    printf("\n----- Storage Classes -----\n");
    showStorageClasses();
    showStorageClasses();   /* called twice to show static behaviour */

    return 0;
}

/* ============================================================
   Demonstrates STORAGE CLASSES: auto, static, extern, register
   ============================================================ */
void showStorageClasses(void)
{
    auto  int localVar = 0;     /* 'auto' is default for locals,
                                    created fresh every call       */
    static int callCount = 0;   /* 'static' keeps its value
                                    between function calls          */
    register int fastCounter = 10; /* 'register' hints the compiler
                                       to keep this in a CPU register
                                       for faster access             */

    localVar++;
    callCount++;      /* retains previous value across calls */
    totalCalls++;     /* extern/global variable, shared across file */

    printf("Call #%d -> localVar(auto)=%d  "
           "callCount(static)=%d  "
           "fastCounter(register)=%d  "
           "totalCalls(extern/global)=%d\n",
           callCount, localVar, callCount, fastCounter, totalCalls);
}
