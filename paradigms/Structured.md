# Structured Programming Paradigm
Structured programming is a paradigm that aims to make programs easier to comprehend from a reader's point of view. It does this by linearising the flow of control through a program. In structured programming, execution follows the writing order of the code.

Structured programming caught favor with programming languages for its iconic opposition to the keyword goto, aiming to reduce the prevalence of spaghetti code. Some other controversial features that most languages have not adopted are avoiding early exit and opposition to exceptions for control flow.

## What are the elementary structures of structured programs?
* Block: It is a command or a set of commands that the program executes linearly. The sequence has a single point of entry (first line) and exit (last line).
* Selection: It is the branching of the flow of control based on the outcome of a condition. Two sequences are specified: the 'if' block when the condition is true and the 'else' block when it is false. The 'else' block is optional and can be a no-op.
* Iteration: It is the repetition of a block as long as it meets a specific condition. The evaluation of the condition happens at the start or the end of the block. When the condition results in false, the loop terminates and moves on to the next block.
* Nesting: The above building blocks can be nested because conditions and iterations, when encapsulated, have singular entry-exit points and behave just like any other block.
* Subroutines: Since entire programs now have singular entry-exit points, encapsulating them into subroutines allows us to invoke blocks by one identifier.
