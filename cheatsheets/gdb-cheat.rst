##############
GDB cheatsheet
##############

Compilation
~~~~~~~~~~~
Compile with debugging symbols. For a simple example of a program with one source file called bla.c ::

  gcc -g3 bla.c -o bla
  
  
Then start gdb and enter the ``list`` command

  (gdb) list
  
to see an excerpt of the code.

Breakpoints
~~~~~~~~~~~

Add break points at a specific line with the ``b`` command. ::

  (gdb) b 10
  (gdb) b 42
  
To see all active breakpoints, use the ``info`` command. ::

  (gdb) info b
  
The breakpoints can be toggled with ``enable``/``disable`` b. ::

  (gdb) disable b
  (gdb) enable b
  
Stepping through the program
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To step through the program, set at least one break point. We run the program with the ``run`` command and can
inspect the value of a variable x with the ``print`` command. We can set x to a new value with the ``set`` command. We can go to the
next line with the ``n`` command. ::
  
  (gdb) run
  (gdb) print x
  (gdb) set x 42
  
Interesting command
~~~~~~~~~~~~~~~~~~~


1. ``(gdb) set args arglist``           specify arglist for next run
2. ``(gdb) set args``                   specify empty arglist for next run
3. ``(gdb) show args``                  display current args
4. ``(gdb) b file:lineno                set break point in file at line n, e.g. ``b main.c:14``
  
