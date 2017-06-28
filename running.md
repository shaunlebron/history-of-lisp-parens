# Running

Running old Lisp editors to learn their behavior by experience.

## Interlisp Teletype

A working Interlisp command-line emulator can be found at:<br>
https://github.com/blakemcbride/LISPF4

The repo includes binaries for windows, mac, and linux.  Building is also painless.

__Run Interlisp command prompt on Mac__:

```
brew install rlwrap         # lets us use arrow keys in the Interlisp prompt

cd Mac
rlwrap ./lispf4 BASIC.IMG
```

__Run the editor for an arbitrary expression__:

```
_(EDITS '(A B (C D) E F G))    

*PP
(A B
   (C D)
   E F G)

*(BO 3)
*PP
(A B C D E F G)
```

__Exiting__:

- `OK` exits the editor
- `(EXIT)` exits the Interlisp emulator

## Interlisp DEdit?

Unfortunately, I do not know how to run DEdit, since the only publicly available
Interlisp-D environment runs only SEdit, which replaced DEdit:

> The list structure editor, DEdit, is not part of the Lisp environment. It is
> now a Lisp Library Module.<br>
> —[Medley Release Notes] chapter 16


## Interlisp SEDit

Running an emulated SEdit is trickier than the teletype editor since it requires
the Interlisp-D graphical environment.

Xerox has published a free Interlisp-D environment (for research and education),
[described here][LFG]. It is bundled with programs for allowing linguists to
create "Lexical Functional Grammars", but we are using it only to discover the
behavior of Interlisp's SEdit.

The last binaries were built in 2003, so we must run it in a supported OS from
that time. We can do this by running Debian 3.1 + X11 inside VirtualBox.

You can build it yourself with [these instructions], or use our prepackaged
image below.

__Run the VM:__

1. Download our [prepackaged debian image]
1. Open VirtualBox
1. Create a new VirtualBox VM (Linux 2.4, 32 bit)
1. Point it to an existing disk (the vdi file from step 1)
1. In Settings, ensure pointing device is a PS/2 Mouse
1. In Settings, ensure that the disc is mounted as an IDE device
1. Start

__Once inside Debian, run Interlisp:__

1. Login as `root`/`toor`
1. Hold click on Debian's desktop (and keep holding)
1. Hover on Debian's right menu icon
1. Hover on XShells's right menu icon
1. Release click on XTerm

```
cd lfg
./ldex lfg.sysout
```

__Once inside InterLisp, run SEdit:__

1. Close the open windows by holding right-click on each window head > close
1. Hold right-click on Interlisp's desktop > EXEC
1. Type `(ED 'FOO)` > click "Functions" > click "Defun"
1. You are now in an SEdit window.

## Nokolisp

1. Download [noko.exe] and place it in some empty directory (e.g. `~/nokolisp` used below)
1. Open [DOSBox].

```
Z:\>mount c: ~/nokolisp

Z:\>c:

C:\>noko
```

You can display and edit the packaged `fib` function to try it out:

```
0> fib

1> (edit fib)
```

[Medley Release Notes]:http://bitsavers.trailing-edge.com/pdf/xerox/interlisp-d/198809_Medley_1.0/400006_Lisp_Release_Notes_Medley_Release_1.0_Sep88.pdf
[these instructions]:https://gist.github.com/grav/7fe0f054f5ad04da2bb0eef2414a663b
[LFG]:http://www2.parc.com/isl/groups/nltt/medley/
[prepackaged debian image]:https://github.com/shaunlebron/history-of-lisp-editing/releases/download/0.0/Debian.3.1r0a.x86.netinstall.vdi.zip
[noko.exe]:http://timonoko.github.io/noko.exe
[DOSBox]:https://www.dosbox.com/
