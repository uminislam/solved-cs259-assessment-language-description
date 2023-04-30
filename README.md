Download Link: https://assignmentchef.com/product/solved-cs259-assessment-language-description
<br>



PLM (Programming Language of the Moment) is a language that allows users to write code that computes non-negative integers. A PLM program consists of several lines of code, each of which defines a single function. For instance the function that returns its argument incremented by 4 can be defined using the following syntax.

DEF ADDFOUR x { x+4 } ;

ADDFOUR will be called the <em>function name</em>, x will be called the <em>parameter name </em>and x+4 is the <em>function body</em>.

A <em>function definition </em>must contain the seven elements specified below. They must occur in a single line, exactly in the order listed below, and must be separated from each other by exactly one space character.

<ul>

 <li>keyword DEF</li>

 <li>function name</li>

 <li>parameter name</li>

 <li>left brace</li>

 <li>function body</li>

 <li>right brace</li>

 <li>semicolon</li>

</ul>

Additionally, PLM code must satisfy all conditions described below.

<ol>

 <li>The character D from DEF must be the first character on each line with a function definition.</li>

 <li>The semicolon in the last function definition must be followed immediately by the end-ofline character and then the end-of-file character.</li>

 <li>Function names are non-empty strings of upper-case letters with one exception. The word DEF is a keyword <em>and </em>a reserved word in the language. Consequently, DEF cannot be used as the name of a function.</li>

 <li>Parameter names are non-empty strings of lower-case letters.</li>

 <li>The only exception to the rules is the function name MAIN. No parameter name is allowed after MAIN, i.e. MAIN must be followed by one space and then the left brace.</li>

 <li>There can be no whitespace inside the function body, but remember that the body must be separated from the enclosing braces by one space on each side.</li>

 <li>The function body is an arithmetic expression built from non-negative integers, the associated parameter name as well as function calls. The only arithmetic operations allowed are addition and multiplication. Parentheses are not allowed, except in function calls (see next point). The function body must be non-empty.</li>

 <li>Function calls have to refer to functions that have been defined as part of the same program. Function definitions are listed in no particular order. It is possible for a function body to make calls to functions defined later in the program. Functions can also call themselves.</li>

 <li>Any function different from MAIN can be called. Function calls are made by mentioning the relevant function name along with an argument enclosed in a pair of parentheses, e.g. ADDFOUR(3+5*6). No Whitespace can occur between the parentheses. The argument must satisfy the same constraints as function bodies. That is, it must be a non-empty arithmetic expression built from addition, multiplication, non-negative integers, the parameter name of the function that is making the call, as well as calls to other functions.</li>

 <li>Every program must define the MAIN</li>

 <li>No function can be defined twice.</li>

 <li>No characters other than the specific ASCII characters referenced so far, are allowed.</li>

</ol>

Here are some examples of PLM programs.

<ol>

 <li><strong>Example 1</strong></li>

</ol>

DEF MAIN { 1+ADDFOUR(2+ADDFOUR(3)) } ; DEF ADDFOUR x { x+4 } ;

<ol start="2">

 <li><strong>Example 2</strong></li>

</ol>

DEF ABCD xyz { BCD(xyz) } ;

DEF BCD xy { 2*CD(xy) } ;

DEF CD x { D(x)+EF(x) } ;

DEF D x { 10 } ;

DEF EF x { 10*x } ;

DEF MAIN { ABCD(1) } ;

<ol start="3">

 <li><strong>Example 3</strong></li>

</ol>

DEF QQ yy { 2*PP(yy)+3*QQ(yy) } ;

DEF PP xx { QQ(xx)+3 } ; DEF MAIN { PP(0)+3 } ;

Here are some examples of pieces of code that <em>do not </em>constitute a legitimate PLM program.

<ol>

 <li><strong>Non-example 1</strong></li>

</ol>

DIF MAIN { 1+ADDFOUR(2+ADDFOUR(3)) } ;

This is not a PLM program because DIF is used instead of DEF.

<ol start="2">

 <li><strong>Non-example 2</strong></li>

</ol>

DEF P2P xXx { 3*Q()+R(6,Q(5)) };

This is not a PLM program due to any one of the following reasons.

<ul>

 <li>The function name P2P contains a number but function names are only allowed to contain upper-case letters.</li>

 <li>The parameter name xXx contains an upper-case letter, which is not allowed.</li>

 <li>The function body contains calls to undefined functions Q and R. Also there are two spaces before }.</li>

 <li>The MAIN function is missing.</li>

 <li>There is no space between } and ;.</li>

 <li>The argument in the call to Q is empty.</li>

 <li>The argument in the call to R contains a ‘,’ which is not allowed.</li>

</ul>

<h1>2     Tasks</h1>

PLM programs can be executed by running the function body of MAIN. This may result in calls to other functions, which may in turn call further functions and so on. When a function call is made, we assume that the argument is always evaluated first and the value is then substituted for all occurrences of the corresponding parameter in the function body. Sometimes this will produce a result: the first two examples of PLM programs we saw earlier return 14 and 40 respectively. In cases when there are circular dependencies between functions (eg. Example 3), the program will not terminate. For the purposes of evaluation, we assume that multiplication takes precedence over addition.

<strong>2.1      Task one</strong>

Implement a parser (along with a lexer) that recognizes PLM programs.

<h2>2.2       Task Two</h2>

Extend the parser to an evaluator so that it can determine whether the input program returns a result or not. If the former is the case, the result (a non-negative integer) should be printed out.

<h1>3       I/O Specifications</h1>

Your parser should read the input from System.in. System.out should be used for output. Parsing errors should be reported on System.err. You must provide exactly one error message which gives exactly one reason (out of possibly many reasons) why the input is not a PLM program. More details follow.

<ul>

 <li>If the input is a valid PLM program, two lines must printed out to out: the first line only contains the word PASS and the second line must contain information about the results, as explained in the next sentence. If the program evaluates to a number, then the number should be printed out on the second line. Otherwise, the line should read DIVERGENCE.</li>

 <li>If the input is <em>not </em>a PLM program, only a single line with FAIL should be printed out to the standard output stream. Two lines must printed out to err: the first line only contains the line number in the input where a violation has been identified and the second line gives an error message describing this violation. When the violation described is a missing MAIN function, then the line number of the violation should be 0. <strong>You are not allowed to simply use default </strong>javacc <strong>messages regarding uncaught exceptions as a reason for the input not being a PLM program. </strong>Consequently, you are expected to decode the javacc exceptions to provide your own error message.</li>

</ul>

Here is the expected output for the examples given earlier.

<strong>Example 1</strong>

PASS

14

<strong>Example 2</strong>

PASS

40

<strong>Example 3</strong>

PASS

DIVERGENCE

<strong>Nonexample 1</strong>

FAIL

<strong>Nonexample 2</strong>

FAIL

Here is a sample of acceptable outputs to the error stream.

<strong>Nonexample 1</strong>

1

Missing keyword DEF

<strong>Nonexample 2</strong>

0

Missing MAIN function