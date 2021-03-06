Tautology checker
=================

[![Build Status](https://travis-ci.org/snim2/tautology-checker.png?branch=master)](https://travis-ci.org/snim2/tautology-checker)

This is a simple tautology checker, written in Java, as a teaching
tool.

It uses an operator-precendence parser to parse a file containing a
proposition and print out a trace which contains the syntax tree of
the original proposition, its negative normal form, conjunctive normal
form and whether or not the proposition is a tautology.

The language parse by the checker is the following:

    Prop ::= FF
           | TT
           | NOT Prop
           | Prop AND Prop
           | Prop OR Prop
           | Prop => Prop
           | Prop AND Prop
           | ( Prop )

To build the package run Maven:

    $ mvn compile

To run the unit tests use Maven again:

    $ mvn test

There are a number of examples in the `src/test/resources` directory and a
shell script `check.sh` which takes a file name and calls the checker.

For example:

    $ ./check.sh src/test/resources/peirces_law.prop 

Produces the following output:

    A Tautology Checker for Propositional Calculus
    ------------------------------------------------
    
    Input file: tests/peirces_law.prop
    ----------
    ((P => Q)=>P)=>P
    
    
    
    Abstract syntax tree:
    --------------------
    ((P => Q) => P) => P
    
    RESULT OF formula.removeImplications():
    --------------------------------------
    (!(!(!P \/ Q) \/ P) \/ P)
    
    RESULT OF formula.toNnf():
    -------------------------
    (((!P \/ Q) /\ !P) \/ P)
    
    RESULT OF formula.nnfToCnf():
    ----------------------------
    (((!P \/ Q) \/ P) /\ (!P \/ P))
    
    RESULT OF formula.simplifyCnf():
    -------------------------------
    TRUE
    
    Your formula is a tautology.
    
    $ 


-- Sarah Mount 2010.