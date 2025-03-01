Download link :https://programming.engineering/product/cs-445-ssignment-5-huffman-compression-implementation-solution/

# CS-445-ssignment-5-Huffman-Compression-Implementation-Solution
CS 445 ssignment 5 Huffman Compression Implementation Solution
Purpose and Goal: We have discussed binary trees (BTs) and you will utilize them in a rough implementation of a famous compression algorithm: Huffman Compression. In this program you will utilize a pre-made Huffman compression tree to compress and decompress selected text strings.

DETAILS


Huffman Compression is a very useful compression algorithm that is utilized in several commonly used compression schemes. The details of Huffman compression, its viability and how the Huffman tree is initially created are not necessary for this project but may be of interest to you. If you would like more information on the details of Huffman Compression, see: http://en.wikipedia.org/wiki/Huffman_coding

In this assignment, you must do the following:

Task 1) Read in a representation of a Huffman tree from a text file and generate a Huffman tree of binary nodes. See more details below about the format of the file and requirements for the tree.

Task 2) Use the tree generated in Task 1) above to create a Huffman encoding table. See more details below about the format of the encoding table.

Task 3) Initiate an interactive session with the user that will continue until the user elects to quit. Each iteration has the following options:

Encode a word. In this case, show the user the set of valid characters and prompt the user to enter a word in normal text. Your program should output the equivalent Huffman codes as strings of 0’s and 1’s, with the code for each character being shown on a separate line. If the input String cannot be encoded properly, indicate this to the user. See example output in the files specified below.

Decode a Huffman code. In this case, show the user the Huffman encoding table and prompt the user to enter a Huffman string of 0s and 1s on a single line. There should be no

Assignment adapted from Dr. John Ramirez’s CS 445 class.


spaces in the line. Your program should output the equivalent text string on a single line. If the Huffman code cannot be decoded properly, indicate this to the user. See example output in the files specified below.

c. Quit the program

Note that for a real Huffman code, the encoded output would be binary bits. Since we are instead using

strings of 0’s and 1’s, we are not actually compressing anything (rather we are making the data

bigger). However, we can still see how the process works and see what the binary bits WOULD be if we

completed the implementation.

This program has a lot to it, so you definitely want to start early. However, none of the tasks is

in itself extremely difficult. Proceed step by step carefully and you should be able to complete it. To give you an idea of how the finished product would look, you can find some test runs. See the attached files a5out1.txt and a5out2.txt.

TASK 1. READING THE TREE

Representing the Tree. The Huffman tree must be stored as a dynamic tree of BinaryNodes. Use BinaryNode<Character> for your node type so that you can store character values within your nodes. You may use the BinaryNode class as provided by the author (see the attached code), or you may modify it as necessary to make your implementation simpler. Either way, be sure to include all files that you use for this assignment, whether you have written them or the textbook author has written them.

Creating a Huffman tree from scratch is a non-trivial process. However, reading a representation of a Huffman tree from a file can be done in a fairly simple way utilizing recursion. The input file will consist of a number of lines of text. Each line will be one of two possibilities:

The single letter “I”. This indicates that the node is an Interior node in the Huffman tree. For simplicity, in this case we will consider the root to also be an interior node. Due to the nature of Huffman trees, all interior nodes will have two children.

The single letter “L” followed by a single space, followed by a single letter. This indicates a Leaf node in the Huffman tree. The second letter on each line can be any upper-case letter, ‘A’ through ‘Z’, but each letter in the alphabet can appear in at most one line. These second letters represent the characters that can be encoded by the Huffman tree. For simplicity, assume that any subset of the alphabet in the file will always be a contiguous sequence starting at ‘A’. For example, if the file contains only 5 letters, the leaf nodes will be ‘A’, ‘B’, ‘C’, ‘D’ and ‘E’. However, they do not have to appear in the file in any particular order.

Your algorithm can read the tree in the following way:

Start with an empty binary tree

Recursively build the tree as follows:

Read the next line from the file


This is actually fairly simple to do with an inorder traversal and a StringBuilder. As mentioned above, we will assign the bit ‘0’ to the left child of a node and the bit ‘1’ to the right child of a node. As we recursively traverse the tree, we add the correct bit to our StringBuilder with each recursive call, and we remove the bit when we backtrack. Upon reaching a leaf node, the current StringBuilder should contain the Huffman encoding string for that letter. We then store that value in an array of Strings. To make indexing easier, we will map the letter ‘A’ to location 0 and successive letters to the following locations. Given the example tree above, the resulting encoding table will be:

Index

Letter

Huffman Code

0

A

0

1

B

111

2

C

110

3

D

100

4

E

1010

5

F

1011

TASK 3. ENCODING AND DECODING A TEXT STRING:

Encoding. Once you have the encoding table built, encoding a string is a simple process. Simply iterate through the characters of the string. For each character, look up the Huffman code in the encoding table and append the results of all of the lookups together. To make it easier to grade, separate the codes of different letters with line feeds. For example, given the text string “BAD”, your program would append “111”, “0” and “100” to yield “111\n0\n100\n”.

Decoding. Decoding a Huffman string works in the following way:

– Start at the root of the Huffman tree and at the first bit (character) in the Huffman string

– If the current bit is a ‘0’, go left in the tree

– If the current bit is a ‘1’, go right in the tree

– When a leaf in the tree is reached, append the corresponding character to the output and return to the root

– Continue until all of the bits have been consumed

For example, given the Huffman code string:

1110100

The process would be:

Go right, go right, go right – append ‘B’ and return to root

Go left – append ‘A’ and return to root

Go right, go left, go left – append ‘D’ and return to root

No more bits remain so the decoding is over – return “BAD”

SUBMISSION REQUIREMENTS


Be sure to submit Assig5.java and ALL files necessary to compile and run your program, as well as your completed Assignment Information Sheet. This includes all source files (both yours and the textbook author’s) as well as all test data files and any other files that you may have used. Your files should be submitted to GradeScope.

The idea from your submission is that the autograder and your TA can compile and run your program WITHOUT ANY additional files OR PROCESSING. This means compilation and execution on the command line using the javac and java commands. Test your programs from the command line before submitting

– especially if you use an IDE such as NetBeans or Eclipse to develop your project.

As you did in previous assignments, be sure to document your code adequately, especially in segments where the logic is not obvious.

Extra CREDIT


As a challenging extra credit option, add code to generate the initial Huffman tree by processing a text file and creating the tree based on the relative frequencies of the characters in the file. Once the tree has been generated, save it in the format described above so that it can be read in again later if necessary. This is a lot of work so don’t attempt it unless you have already completed the required elements of the assignment. You may need to consult various sources to see how the Huffman tree is initially generated.

RUBRICS


Please check the grading rubric on CourseWeb.
