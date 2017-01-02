## What is PDB++?
[PDB++](https://bitbucket.org/antocuni/pdb/src) is code that extends the Python debugger [PDB](https://docs.python.org/3/library/pdb.html). This is a project that extends PDB++.

## Why this? 
1. Turn on 'sticky mode' by default (repaint the code on the screen at each step).
2. Persist breakpoints to a file and load them when the first `pdb.set_trace()` is called. Also have the breakpoints auto-adjust to the next valid line if the code changes.

## How do I install this?
1. [Install pdb++](https://pypi.python.org/pypi/pdbpp/). (e.g. `pip install pdbpp`).
2. Copy the pdb.py file in this repository to your site-packages directory.

## How do I store breakpoints in a file?
Create a `.py-breakpoints` file in your home directory, and put the breakpoint text (what you would usually specify manually in a PDB debugging session) on separate lines.

Example `~/.py-breakpoints` file:
```
/home/jason/projects/st/run.py:15
```
## How do the breakpoints get initialized?
Add an `import pdb; pdb.set_trace()` to the top of the script you're running. Once the set_trace() is called, the breakpoints will be read from the file and initialized.

## Can I set a breakpoint from Emacs?
Yes. This function appends breakpoints (e.g. `/my/path/run.py:50`) to my `.py-breakpoints` file:
```
(defun breakpoint-append()
  (interactive)
  (setq lnum (format-mode-line "%l"))
  (setq bp (concat (buffer-file-name) ":" lnum "\n"))
  (write-region bp nil "~/.py-breakpoints" 'append)
  )
  ```
If you're on Windows, you'll probably need to indicate the full path above (e.g. `c:/Users/BobSmith/.py-breakpoints`).

## Does this work on Windows?
Yes, pdb++ and these modifications do work on Windows if you use a console that supports colors (I used [ConEmu](https://conemu.github.io/)).

## License
This code is adapted from:
  1. The Python code base (from pdb.py), license [here](https://www.python.org/download/releases/3.4.0/license/). 
  2. The PDB++ project (license shown as BSD [here](https://pypi.python.org/pypi/pdbpp/). 

Any modifications are released under the MIT and/or BSD licenses.
