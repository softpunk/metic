# metic
metic is a new paragidm of shell. Many shells have one simple function: run programs. Shells like bash and zsh come with a few more features that make them preferable over these simpler shells, like control structures and functions. However, the usefulness of the shell has yet to reach its full potential.

# The Problem with Shells
Shells provide programming constructs, sure. But constructs are just half of programming. What about the type system? Well, from the shell's perspective, there are only two true types: text and integers.

Programs all return some integer to let the environment know how well it executed. They may also output data to stdout, which can be passed around in a script for manipulation or into other programs through pipes. This means that in order to use the data, you have to do the following things:

* Know the format of the data you will get
* Create a program to work specifically with that format
* Make a copy of the text

This is prone to bugs. Very prone. The chances that a program improperly parses the output of a program is high, leading to unnecessary bugs. Furthermore, the program which recieves the information has to know what to do with it. If shells were designed better, there would be a library of functions to handle common forms of data.

# The solution
The solution is metic. Metic will be a C#-based shell environment for working with programs. Programs are defined in C#, organized in modules that make sense for their function. Instead of "ls", you may have `Dir.List`. Instead of rm, `Dir.Remove("file")`. Everything will be organized. Everything will return meaningful values.

# Technical Overview
metic is in its planning stage. For right now, I forsee the system working like this:

The 'ground floor' of the program is a C# REPL. It uses an anonymous class to accept lines, compiling them on the fly. Each REPL acts as a sandbox, having unique variables to it.

Each REPL will inherit information from 'Global', a static class, and equivelant to .bashrc. This will be placed in the user's home directory, and contain things like aliases, global variables, and import functions for metic programs.

In order to make metic compatible with existing programs, there are two options which will likely both be implemented: TRlayer and native.

TRlayer is literally a translation layer for programs. It is C# code that will wrap binary files and provide "TRlayer" Objects. These contain instance variables used to parse native binaries. It will contain "lines", for programs that have to parse using lines. It will contain "words", for programs that parse by words, etc. It will also include options for manually manipulating STDIN, STDOUT, and STDERR

Native is a sandboxed shell running inside of metic. You can have as many Native threads running as you'd like. new Native("/bin/bash").exec("ls").arg("-a"), for instance, would run `ls -a` in a bash shell, managed by metic. The output is capture and returned in a TRlayer for use in other programs.

# Milestones
Here is a list of some of the things that need to be done:

* C# REPL works
* Global configuration file works
* Global configuration file supports aliases
* Importing C# programs works
* TRlayer works
* Native works

Some optional milestones I want to shoot for:

* Code completion by way of tab works
* Automatic Native calls get to the point where it can be used as a boot shell

# License
This program is licensed under the MIT license. See LICENSE for more information.
