# pdbpp
A fork of [PDB++](https://bitbucket.org/antocuni/pdb/src) with the following objectives:

1. Turn on 'sticky mode' by default.
2. Add code to help store breakpoints in a file, and have those breakpoints move forward in the code to the next valid line if the code changes.

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

## License
This code is adapted from:
1. The Python code base (from pdb.py), license [here](https://www.python.org/download/releases/3.4.0/license/). 
2. The PDB++ project (license shown as BSD [here](https://pypi.python.org/pypi/pdbpp/). 

Any code I've written/modified I release under the MIT and/or BSD license.
