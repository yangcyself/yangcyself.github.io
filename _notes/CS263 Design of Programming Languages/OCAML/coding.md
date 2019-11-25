## guide line
**Basically, there are two guidelines in functional programming:**

- Procedures have no side effects, which means that no globals have been modified
- Functions have no destructive operations

It is a good idea to try and keep functional code separate from imperative code. Functions should be created for specific purposes and should not contain a myriad of imperative statements. **One common practice is to have some sort of an imperative main function in an Ocaml program which calls other functional procedures.**


## recursion
In functional programming, all looping is done through recursion. In writing recursive procedures, there are just two important steps:
- Start with the base cases
- Trust the recursion

### Recursive vs. Iterative Processes

Tail recursion is often more efficient because it runs in constant space. Whereas a recursive process adds to the stack on each call.

for example:
```ocaml
let rec factorial x = 
  if (0 > x) then (raise Exit) else
    let rec helper x so_far = 
      match x with
	  0 -> so_far
	| n -> (helper (n - 1) (so_far * n))
    in
      (helper x 1)
```
俺，必须需要一个helperfunction， 否则无法存储中间变量。所有的中间变量都要用参数的方式传递

## about ;;
The truth is that `;;` is mostly used in the toplevel and tutorials to mark the end of an OCaml phrase and send this phrase to the toplevel in order to evaluate it.

Outside of the toplevel, uses of `;;` are, at best, infrequent and are never required for well written code. Briefly, double semi-colon `;;` can used for three reasons:
- For compatibility with the toplevel;
- To split the code to ease debugging;
- To introduce a toplevel expression.



However, this use of ;; can (should) always be replaced by either
```ocaml
let () = expression ()
```
or
```ocaml
let _ = expression ()
```
Note that the first form is safer, since it requires that the type of the returned expression is unit; preventing us, for instance, from forgetting an argument in
```ocaml
let () =
  print_newline
  (* here, we forgot () and the compiler will complain. *)
```

Consequently, some style guidelines consider that ;; should never be used outside of the toplevel

## Higher order functions


# common Modules
## List
### list map
```ocaml
List.map (fun x -> x + 1) [1;2;3;4];;
- : int list = [2; 3; 4; 5]
```
### list filter
```ocaml
List.filter (fun x -> (x mod 2) = 0) [1;2;3;4;5];;
- : int list = [2; 4]
```

## basic operations
### build
`[]`
### add an item at head
`a::lst`