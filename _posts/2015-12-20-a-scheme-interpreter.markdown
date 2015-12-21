---
layout: post
title: "A Simple Scheme interpreter!"
date: 2015-12-18 20:30:00
---

This is a simple scheme interpreter for you to learn SICP, you can clone it from my [GitHub](https://github.com/rex-zhou/Schemescript) and open in your browser.

#What is a language interpreter?
A language interpreter has two parts:

- 1 Parsing:
The parsing component transform an input program from a sequence of character to an internal representation by some syntactic rules.
- 2 Execution:
The execution component will processing the internal representation to the real output by the semantic rules.

Here's the working progress of a interpreter:

program(string of file) -> parse -> AST(abstract syntax tree) -> eval -> output
