Project 1: Socket Basics

The goal of this project is to explore communicating with a socket by building a client application that connects to a socket server. It uses Python's native socket module (import socket) and native json module (import json). The socket server contains a wordle server that IDs a connection and assigns it a 5 letter word. When the client sends the server a word guess, the server responds with which letters are green, uellow, or red. This client application communicates with the socket server, sending guesses until it guesses the correct word.

The high-level approach to guessing the correct word was a general method of elimination. It takes a file of eligible words as a list, and filters down the list each time it receives a new reply and set of marks. It only accesses the latest mark, as any older marks are irrelevant due to their corresponding words having been eliminated.

The logic for elimination is as so:
The program links each letter in the guess with its corresponding mark and tracks their index in the word.
For green [2] letters, any word without the green letter in the same index is filtered out.
For yellow [1] letters, any word without the yellow letter is filtered out. Any words with the yellow letter in the same index are also filtered out.
For red [0] letters, any word with the red letter is filtered out.

Some extra logic had to be attached to account for the weird way in which the server assigned marks for duplicate letters (like 'apple'). A guess with 'p' in index 2 and another 'p' in index 0 would be given a [2] and a [0] for p. The contradiction would filter out every possible word, so green was set to take precedence. This was very hard to discern at first.

Some helper functions were tested by giving them a controlled set of variables, but most of the testing was done by scattering print statements all over the place and running the program repeatedly. A better method is needed.
