
Programming and Problem Solving
CSIS 2610 Project 2 – Bar Code Decoding
Goal
Develop and implement an algorithm that decodes a bar code using three different encoding schemes.
Details Bar codes have been in use for several decades and exist in many different forms, ranging from
the earliest use in identifying railroad cars to their current ubiquitous forms today. In this project, we
will look at three linear (one-dimensional) codes.
Simple binary
The simplest bar code simply alternates between white and black stripes, where each stripe is either
wide or narrow. The difference in color provides the boundary between bars and the width provides
each bar's value, with a wide bar being interpreted as 1 and a narrow bar as 0. The bars are then
grouped together, with the group being interpreted as a binary number.
Code 39
One of the big issues with a simple binary encoding is that it is sensitive to how fast a code is scanned.
Bar width is usually determined by how long it takes the scanner to traverse the bar. If the scan is too
fast or too slow, it will misinterpret the bar, usually leading to a maximum possible value (if too slow) or
zero (if too fast) for the bar code.
Code 39 is a “self-clocking code,” which means that the scan speed does not matter, although for this
version the scan speed must be constant. The “39” in the name comes from “three of nine;” nine bars
(five black alternating with four white) are grouped together and in each group of nine, exactly three are
wide. Each group is separated by a narrow white bar.
Decoding a code 39 bar code is interesting, as it involves some basic combinatorics. In a code 39 bar
code, the bars are numbered 8 to 0, from left to right. Suppose the three wide bars are numbered w1 ,w2
,w3 with w1>w2>w3 . Then, the encoded number is:
n!
w1
w2
w3
n
,
if n ≥ k
e = ( ) + ( ) + ( ) where ( ) = { k! (n − k)!
4
3
2
k
0,
otherwise
Side note: You have most likely seen code 39 before, as it is a common encoding scheme. YSU's parking
passes use it, as does Sam's Club.
Code 48
Code 48 is an interesting code, as there are only narrow bars. A code 48 bar code has eight bars, four of
which are black (and four are white.) What makes the code more interesting is that the colors do not
alternate, so multiple white bars and multiple black bars can be adjacent. This does not pose a problem,
however, as a code 48 reader looks at all eight bars simultaneously, so there is no issue with scan speed
or bar width.
Decoding is similar to the process used in code 39; the bars are numbered 7 to 0, and the positions of
the four black bars are used. If those positions are b1 ,b2 ,b3 ,b4 with b1>b2>b3>b4 then the encoded
position is
b1
b2
b3
b4
e = ( )+ ( )+ ( )+ ( )
4
3
2
1
You should write a function int choose(int n, int k) that computes ( n ) and another function int
k
factorial(int n) that computes n!. The values involved here will not cause overflow issues (any factorial
larger than 12! won't fit into an int) and will always be integers.
Your program will begin by reading an integer. A 1 indicates the bar code that follows is a binary bar
code, a 2 indicates a code 39 bar code, a 3 indicates a code 48 bar code and a 0 is used to quit the
program.
For a binary bar code, your program must do the following:
• Read a number b indicating the number of bars in the code (an odd integer 1 ≤ b ≤ 21 )
• Read b characters, one at a time
◦ Each character will be either w for wide or n for narrow
◦ Wide bars are a 1, narrow bars are a 0
• Convert the bar code into its equivalent number and display the number
For a code 39 bar code, your program must do the following:
• Read in nine characters, one at a time
◦ Each character will be w or n
• Decode the bars using the formula described above
• Output the decoded number, or an error message if there were too many or too few wide bars
For a code 48 bar code, your program must do the following:
• Read in eight characters, one at a time
◦ Each character will be b or w
• Decode the bars using the formula described above
• Output the decoded number, or an error message if there were too many or too few black or white
bars
After decoding, the program should repeat the process until a bar code of type 0 is entered.
Suggestion: You'll probably want to write three functions, one for each type of bar code.
What to turn in
Turn in a copy of your source code.
