## Motivation
A good way to learn more about programming languages is by understanding how they work. The best way to understand something is to have made it in the first place. Today we set out to build a simple JSON parser using the specs on [json.org](json.org). JSON is a fairly straightforward and well documented spec so it is a good target for learning how to write a parser.

## Process of parsing
JSON gets parsed into a data structure, so we don't have to worry about anything but the translation of a JSON string to the data structure. The first step in the process of translating the JSON file into a more abstract JSON object is called tokenization, lexical analysis or lexing. These terms are often used interchangeably. Lexing and lexical analysis are more often used in natural language processing and have their roots in linguistics. The process is as follows:

1. the tokenizer gets called with a string lets say: `{ "key": "value"}`

2. The string gets broken down in units of meaning (e.g. keywords, separators, operators). The way we do this is by simply scanning over every single character and changing our mode of operation to accommodate (see an opening curly brace? we are dealing with a JSON object, opening square bracket? an array). These units of meaning are called tokens or lexemes. We can see that our string starts with an `{` indicating its a JSON object, moving on to the next relevant token we see a `"key"`, `:`, `"value"`, and finally the end of the JSON object `}`. 

3. The tokens get put in the resulting data structure as we identify them. In our case our string becomes a root JSON object in our abstract representation of the JSON. `(JSON object)` We create the JSON object as soon as we identify it. If we encounter any malformed token along the way we will panic and the parser will quit, so its save to make assumptions like that the object will be a complete JSON object. Once we see the key we append it in our structure `(JSON object (key))` and once we see the value we append it to the key `(JSON object (key value))`. 

You might wonder why we would still need the closing brace, or why we don't just represent it without these symbols if they don't contribute up until this point. Our tokenizer works like a state machine, it switches modes depending on the input it gets called with. The `}` means, exit parsing JSON object, where a `,` would indicate there to be more key value pairs to follow. 

Once we have the entire string turned to a data structure we are done, because JSON is much simpler than a programming language we do not have to go over the resulting data structure to run any instructions. The program can decide how it will use your resulting JSON data structure. 

## Implementing the tokenizer
the easiest way is to loop trough every character and switch modes depending on the character fed into the parser. You can do this using a switch statement that calls into a the right function for parsing a token. For a string you would see that it starts with `"` so any character that is not `"` will need to be stored, the latter token indicating that the string has ended and that you should exit the function and return the string to be embedded in the data structure you are creating.

## understanding how to read the relevant documents for implementing a JSON parser

This excerpt from "how javascript works" is linked on json.org and explains the "McKeeman form", its good to read this trough and use this as a guide when implementing the different modes of the parser as you can see which types include what more clearly than on a syntax diagram:
https://www.crockford.com/mckeeman.html



If you have any suggestions or sources that should be linked you can [fork this article](https://github.com/kaliumxyz/posts/blob/master/JSON.md).
