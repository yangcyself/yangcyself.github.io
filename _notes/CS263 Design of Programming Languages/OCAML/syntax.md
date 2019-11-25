
# use
Use ;; to indicate that you've finished entering each statement
### comments
use `(*` and `*)`

## functions
### def functios
I have seen many methods of defining functions
- func x -> x+1
- let f x = x+1
- let f = function
1 -> "one"
### calling function
```OCaml
repeated "hello" 3  (* this is OCaml code *)
```
repeated ("hello", 3) is correct but it forms hello and 3 into a tuple

```OCaml
repeated (prompt_string "Name please: ") 3
```
Note here is not comma in this bracket because this is a function call

"bracket around the whole function call — don't put brackets around the arguments to a function call". 


OCaml is a strongly statically typed language (in other words, there's nothing dynamic going on between int, float and string, as in Perl).
OCaml uses type inference to work out the types, so you don't have to. If you use the OCaml interactive toplevel as above, then OCaml will tell you its inferred type for your function.
OCaml doesn't do any implicit casting. If you want a float, you have to write 2.0 because 2 is an integer. OCaml does no automatic conversion between int, float, string or any other type.
As a side-effect of type inference in OCaml, functions (including operators) can't have overloaded definitions. OCaml defines + as the integer addition function. To add floats, use +. (note the trailing period). Similarly, use -., *., /. for other float operations.
OCaml doesn't have a return keyword — the last expression in a function becomes the result of the function automatically.

### types
OCaml type  Range

int         31-bit signed int (roughly +/- 1 billion) on 32-bit
            processors, or 63-bit signed int on 64-bit processors
float       IEEE double-precision floating point, equivalent to C's double
bool        A boolean, written either true or false
char        An 8-bit character
string      A string
unit        Written as ()

### recursive functions
Unlike in C-derived languages, a function isn't recursive unless you explicitly say so by using let rec instead of just let. Here's an example of a recursive function:

The only difference between let and let rec is in the scoping of the function name.

### bindings 
```OCaml
let positive_sum a b = 
    let a = max a 0
    and b = max b 0 in
    a + b;;
```

我觉得let and in 是程序的语法， 函数最后只有一个表达式作为返回值，前面的都是let in



## variables
### Let binding
Let bindings are just short hand expressions(but not the same with Macro in C), 把可以复用的中间结果let的话是可以加速的

#### Local variables
```ocaml
let f a b =
    let x = a +. b in
    x +. x ** 2.;;
``` 
#### global variables

define variables at above

### references: the real variables
**generate a new reference:**

```ocaml
ref 0;; (*0 is the initial value*)
let my_ref = ref 0;;
```
**assign**

`my_ref := 10`

get the content out

`!my_ref`

## about Modules
a lot of libraries are located in `/usr/lib/ocaml/`

OCaml always capitalizes the first letter of the file name to get the module name. This can be very confusing until you know about it!

### two methods to use symbols defined in a module
`open Graphics;;`

in this way, the later use will not need to indicate the Graphics (like include in C)

or add `Graphics.` before every ...

or renaming the module

```ocaml
module Gr = Graphics;;

Gr.open_graph " 640x480";;
Gr.fill_circle 320 240 240;;
read_line ();;
```



## doing optional and named arguments to functions
`?foo` and `~foo`

`foo#bar` is a method invocation 


## Mutually recursive functions
can be write in this way
```ocaml
let rec even n =
    match n with
    | 0 -> true
    | x -> odd (x-1)
  and odd n =
    match n with
    | 0 -> false
    | x -> even (x-1);;
```

note that the `rec` is only needed in the head of the whole clause