# ENV
This file contains the information of packages for setting up an OCAML environment

## opam
opam is a source-based package manager for OCaml. It supports multiple simultaneous compiler installations, flexible package constraints, and a Git-friendly development workflow. Managing your OCaml installation can be as simple as:

```bash
opam list -a         # List the available packages
opam install lwt     # Install LWT
opam update          # Update the package list
...
opam upgrade         # Upgrade the installed packages to their latest version
```

### first install failed
```bash
Checking for available remotes: rsync and local, git, mercurial.
  - you won't be able to use darcs repositories unless you install the darcs
    command on your system.

[ERROR] Missing dependencies -- the following commands are required for opam to
        operate:
  - bwrap: Sandboxing tool bwrap was not found. You should install
    'bubblewrap'. See
    http://opam.ocaml.org/doc/2.0/FAQ.html#Why-opam-asks-me-to-install-bwrap.
```

### build bubblewrap-0.3.3 failed

```bash
checking whether gcc accepts -g... (cached) yes
checking for gcc option to accept ISO C89... (cached) none needed
checking whether gcc understands -c and -o together... (cached) yes
checking sys/capability.h usability... no
checking sys/capability.h presence... no
checking for sys/capability.h... no
configure: error: *** POSIX caps headers not found
```

found this at https://github.com/projectatomic/bubblewrap/releases

>On Debian or Ubuntu, something like the following should work:

>$ sudo apt-get install libcap-dev

#### succeed
```txt
    bubblewrap 0.3.3
    ===================

    man pages (xsltproc):                         no
    SELinux:                                      no
    setuid mode on make install:                  none
    require default userns:                       no
    mysteriously satisfying to pop:               yes
```

make && make install

### set up the opam
selected y
```txt
In normal operation, opam only alters files within ~/.opam.

  However, to best integrate with your system, some environment variables
  should be set. If you allow it to, this initialisation step will update
  your bash configuration by adding the following line to ~/.bash_profile:

    test -r /home/yangcy/.opam/opam-init/init.sh && . /home/yangcy/.opam/opam-init/init.sh > /dev/null 2> /dev/null || true

  Otherwise, every time you want to access your opam installation, you will
  need to run:

    eval $(opam env)

  You can always re-run this setup with 'opam init' later.
```
**run eval $(opam env) to update the shell environment**

**NEEDED EVERY TIME FOR A NEW TERMINAL**


## utop
utop is an improved toplevel (i.e., Read-Eval-Print Loop) for OCaml. It can run in a terminal or in Emacs. It supports line editing, history, real-time and context sensitive completion, colors, and more.

https://github.com/ocaml-community/utop


# edit and compile
To compile an OCaml program named my_prog.ml to a native executable, use ocamlbuild my_prog.native:

```bash
$ mkdir my_project
$ cd my_project
$ echo 'let () = print_endline "Hello, World!"' > my_prog.ml
$ ocamlbuild my_prog.native
Finished, 4 targets (0 cached) in 00:00:00.
$ ./my_prog.native
Hello, World!
```

