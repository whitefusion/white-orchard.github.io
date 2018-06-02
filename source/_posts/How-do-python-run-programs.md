---
title: How do python run programs
date: 2018-06-02 12:16:04
tags:
    - core
    - language
    - python
    - note
---
> This is the reading note for "Chapter 2: how python run programs, Learning python 5th edition". <br>

### Brief
An interpreter is a kind of program that executes other programs. It is a layer of software logic between your code and computer hardware on your machine. <br>

Before running a program in python, the program will be first compiled to something called 'byte code' and then routed to something called a 'virtual machine'. <br>

### Bytecode compilation
Compilation is simply a translation step, and byte code is a lower-level, platform-indepedent representation of the source code. It translate the source code into a group of byte code instructions. This process speeds up the execution. <br>

If the Python process has write access on your machine, it will store the byte code of your programs in files that end with a '.pyc' extension. '.pyc' means compiled '.py' source. Prior to 3.2, your will see these files show up next to '.py' after execution. In 3.2 and later, Python instead saves its '.pyc' byte code files in a subdirectory named '\_\_pycache\_\_' located in the directory that your souce code reside, and in files whose names identify the Python version that created them. (e.g. script.cpython-33.pyc).<br>

It is a startup speed optimization. The next time you run your program, Python will load the '.pyc' files and skip the compilation step, as long as you haven't changed your source code since the byte code was last saved, and aren't running with a different Python than the one that created the byte code. Python will automatically check the last-modified timestamp to determine whether the source code was being edited. And it also check the version of Python it was compiled to.<br>

If Python cannot write the byte code files to your machine, you program still works - the byte code is generated in memory and simply discarded on program exit. <br>

Byte code files are also one way to ship Python programs- Python is happy to run a program if all it can find are '.pyc' files, even if the original '.py' files are absent. <br>

Byte code is saved in files only for files that are imported, not for the top-level files of a program that are only run as scripts. （I don't know what is this shit...）<br>

### The Python Virtual Machine (PVM)
Once a program has benn compiled to byte code, it is shipped off to something known as the Python Virtual Mahicne (PVM). The PVM is just a big codee loop that iterates through your byte code instructions, one by one, to carry out their operations. 

### Performance Implications
Compared to C and C++, for one thing, there is no build or 'make' step in Python. Python does not need to reanalyze and reparse each source statement's text repeatedly. For another, byte code instructions requires more work than CPU instructions (binary source code the C and C++ compiled to). <br>

The effect is that pure Python code run at speeds somewhere between those of a traditional compiled language and a traditional interpreted language. 

### Development Implications
All we have in Python is **runtime**, there is no initial compile-time phase at all, and everything happens as the program is running. 

### Cpython
The original, and standard implementation is usually called CPython. This name comes from the fact that it is coded in portable ANSI C language mode. 

### Frozen Binaries
Frozen binaries bundle together the byte code of your program files, along with the PVM and any Python support files your program needs, into a single package. It can be easily shipped to customers. <br>
We need generation tools like py2exe to produce it. 

