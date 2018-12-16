look at these interestng things

https://stackoverflow.com/questions/9031783/hide-all-warnings-in-ipython

https://github.com/JuliaIO/Suppressor.jl

```bash
#!/bin/bash
```

/#!/srv/julia

/srv/julia

/#!/usr/bin/julia

Step 36/46 : RUN julia -e 'if (VERSION > v"0.7-") using Pkg; else Pkg.init(); end; Pkg.add("IJulia"); using IJulia;' && mv ${HOME}/.local/share/jupyter/kernels/julia-${JULIA_VERSION%[.-]*}  ${NB_PYTHON_PREFIX}/share/jupyter/kernels/julia-${JULIA_VERSION%[.-]*}


# Unix Boolean Operators ( &&, -a, ||, -o )
  Rule of thumb: Use -a and -o inside square brackets, && and || outside.

  It's important to understand the difference between shell syntax and the syntax of the [ command.

  && and || are shell operators. They are used to combine the results of two commands. Because they are shell syntax, they have special syntactical significance and cannot be used as arguments to commands.
  [ is not special syntax. It's actually a command with the name [, also known as test. Since [ is just a regular command, it uses -a and -o for its and and or operators. It can't use && and || because those are shell syntax that commands don't get to see.
  But wait! Bash has a fancier test syntax in the form of [[ ]]. If you use double square brackets, you get access to things like regexes and wildcards. You can also use shell operators like &&, ||, <, and > freely inside the brackets because, unlike [, the double bracketed form is special shell syntax. Bash parses [[ itself so you can write things like [[ $foo == 5 && $bar == 6 ]].


# bash exit Status
A shell convention is that a successful executable should exit with the value 0. Anything else can be interpreted as a failure of some sort, on part of bash or the executable you that just ran. See also $PIPESTATUS and the EXIT STATUS section of the bash man page:

# sos
https://github.com/vatlab/SoS/issues/1077
> SoS is very easy to install, involving only two commands
>
>pip install sos sos-notebook
>python -m sos_notebook.install
>It is however quite troublesome to install kernels for Python, R, Julia etc, so it can be troublesome to set up sos on Binder if we are to include several kernels.
