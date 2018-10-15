---
title: "Introducing the Shell"
teaching: 5
exercises: 0
questions:
- "What is a command shell and why would I use one?"
objectives:
- "Explain how the shell relates to the keyboard, the screen, the operating system, and users' programs."
- "Explain when and why command-line interfaces should be used instead of graphical interfaces."
keypoints:
- "Explain the steps in the shell's read-run-print cycle."
- "Most commands take flags (options) which begin with a `-`."
- "Identify the actual command, flags, and filenames in a command-line call."
- "Explain the steps in the shell's read-run-print cycle."
- "Demonstrate the use of tab completion and explain its advantages."
keypoints:
- "A shell is a program whose primary purpose is to read commands and run other programs."
- "The shell's main advantages are its high action-to-keystroke ratio, its support for automating repetitive tasks, and its capacity to access networked machines."
- "The shell's main disadvantages are its primarily textual nature and how cryptic its commands and operation can be."
---
### Background
At a high level, computers do four things:

-   run programs
-   store data
-   communicate with each other, and
-   interact with us

They can do the last of these in many different ways,
including through a keyboard and mouse, or touch screen interfaces, or using speech recognition systems.
While touch and voice interfaces are becoming more commonplace, most interaction is still
done using traditional screens, mice, touchpads and keyboards.

We are all familiar with **graphical user interfaces** (GUI): windows, icons and pointers.
They are easy to learn and fantastic for simple tasks where a vocabulary consisting of
"click" translates easily into "do the thing I want". But this magic relies on 
wanting a simple set of things, and having programs that can do exactly those things.

If you wish to do complex, purpose-specific things it helps to have a richer means
of expressing your instructions to the computer. It doesn't need to be complicated or
difficult, just a vocabulary of commands and a simple grammar for using them.

This is what the shell provides - a simple language and a **command-line interface** 
to use it through. 

The heart of a command-line interface is a **read-evaluate-print loop** (REPL). It is called
so because when you type a command and press <kbd>Return</kbd> the shell
reads your command,
evaluates (or "executes") it,
prints the output of your command,
loops back and waits for you to enter another command.
 
### The Shell

A shell is a program like any other.
What's special about it is that its job is to run other programs
rather than to do calculations itself.
The most popular Unix shell is Bash,
the Bourne Again SHell
(so-called because it's derived from a shell written by Stephen Bourne).
Bash is the default shell on most modern implementations of Unix
and in most packages that provide Unix-like tools for Windows.

### What does it look like?

A typical shell window looks something like:

~~~
bash-3.2$ 
bash-3.2$ ls -F / 
Applications/         System/
Library/              Users/
Network/              Volumes/
bash-3.2$ 
~~~

The first line shows only a **prompt**,
indicating that the shell is waiting for input.
Your shell may use different text for the prompt. Most importantly: 
when typing commands, either from these lessons or from other sources,
*do not type the prompt*, only the commands that follow it.

The part that you type,
`ls -F /` in the second line of the example,
typically has the following structure: a **command**,
some **flags** (also called **options** or **switches**) and an **argument**.
Flags start with a single dash (`-`) or two dashes (`--`), and change the behaviour of a command.
Arguments tell the command what to operate on (e.g. files and directories).
Sometimes flags and arguments are referred to as parameters.
A command can be called with more than one flag and more than one argument: but a
command doesn't always require an argument or a flag.

In the second line of the example above, our **command** is `ls`, with a **flag** `-F` and an
**argument** `/`. Each part is separated by spaces: if you omit the space 
between `ls` and `-F` the shell will look for a command called `ls-F`, which 
doesn't exist. Also, capitalization matters: `LS` is different to `ls`. 

Next we see the output that our command produced. In this case it is a listing 
of files and folders in a location called `/` - we'll cover what all these mean 
later today. Those using a macOS might recognize the output in this example.

Finally, the shell again prints the prompt and waits for you to type the next 
command.

In the examples for this lesson, we'll show the prompt as `$ `. You can make your 
prompt look the same by entering the command `PS1='$ '`. But you can also leave 
your prompt as it is - often the prompt includes useful information about who and where 
you are.

Open a shell window and try entering `ls -F /` for yourself (don't forget that spaces
and capitalization are important!). You can change the prompt too, if you like.

### How does the shell know what `ls` and its flags mean?

Every command is a program stored somewhere on the computer, and the shell keeps a
list of places to search for commands (the list is in a **variable** called `PATH`, 
but those are concepts we'll meet later and are not too important at the moment). Recall
that commands, flags and arguments are separated by spaces.

So let's look at the REPL (read-evaluate-print loop) in more detail. Notice that the
"evaluate" step is made of two parts:

1. Read what was typed (`ls -F /` in our example)  
    The shell uses the spaces to split the line into the command, flags, and arguments
2. Evaluate:  
    a. Find a program called `ls`  
    b. Execute it, passing it the flags and arguments (`-F` and `/`) to 
       interpret as the program sees fit 
3. Print the output produced by the program

and then print the prompt and wait for you to enter another command.

> ## Command not found 
> If the shell can't find a program whose name is the command you typed, it 
> will print an erorr message like:
> 
> ~~~
> $ ls-F
> ~~~
> {: .language-bash}
> ~~~
> -bash: ls-F: command not found
> ~~~
> {: .output}
> 
> Usually this means that you have mis-typed the command - in this case we omitted
> the space between `ls` and `-F`. 
{: .callout}

### Is it difficult?

It is a different model of interacting than a GUI, and that 
will take some effort - and some time - to learn. A GUI 
presents you with choices and you select one. With a **command line interface** (CLI) the choices are combinations 
of commands and parameters, more like words in a language than buttons on a screen. They
are not presented to you so
you must learn a few, like learning some vocabulary in a new language. But a small 
number of commands gets you a long way, and we'll cover those essential few today.

### Flexibility and automation 

The grammar of a shell allows you to combine existing tools into powerful
pipelines and handle large volumes of data automatically. Sequences of
commands can be written into a *script*, improving the reproducibility of 
workflows and allowing you to repeat them easily.

In addition, the command line is often the easiest way to interact with remote machines and supercomputers.
Familiarity with the shell is near essential to run a variety of specialized tools and resources
including high-performance computing systems.
As clusters and cloud computing systems become more popular for scientific data crunching,
being able to interact with the shell is becoming a necessary skill.
We can build on the command-line skills covered here
to tackle a wide range of scientific questions and computational challenges.

## A Disasterous Downloads Directory: Starting Point

Nelle Nemo, a typical computer user,
has a `Downloads` directory that is full of all kinds of files that are disorganized.
Her goal is to create a script that she can periodically run that will automatically
clean up the directory according to some rules that she devises.
Her sample directory is what you have downloaded and extracted as `data-shell` on your Desktop.
