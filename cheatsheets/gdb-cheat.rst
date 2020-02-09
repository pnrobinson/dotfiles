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
next line with the ``n`` command (next line, ,including function calls) or ``s`` (next step). ::
  
  (gdb) run
  (gdb) print x
  (gdb) set x 42
  
Interesting commands
~~~~~~~~~~~~~~~~~~~~


1. ``(gdb) set args arglist``           specify arglist for next run
2. ``(gdb) set args``                   specify empty arglist for next run
3. ``(gdb) show args``                  display current args
4. ``(gdb) b file:lineno``              set break point in file at line n, e.g. ``b main.c:14``
5. ``(gdb) delete 2``                   delete breakpoint 2 (use ``info b`` to see the breakpoint numbers)
  



Installing gdb on Mac
~~~~~~~~~~~~~~~~~~~~~

This is a bit tricky. We first install gdb using homebrew. ::

  brew install gdb
  
We then need to code-sign the GDB executable, so it will be allowed to control other processes, as necessary for a debugger.
Open the Keychain Access application (can be found in Applications/Utilities directory). Select Certificate AssistantCreate a Certificate in the application menu (Keychain Access).

1. name the certificate ``gdbcert``
2. set Identity Type to ``Self Signed Root``, change Certificate Type to ``Code Signing``, check the ``Let me override defaults`` checkbox and continue
3. On the next page, leave Security Number to be 1, and set Validity Period to a large number of days, e.g. 3650 (ten years)
4. Continue through the next six screens without changing anything until we get to ``Specify a Location For The Certificate``.
5. For the property, Keychain, choose ``System``from the drop-down list and click ``Create``.
6. Now go back to the main window, choose the System keychain in the sidebar on the left, and select the newly created certificate from the list. Open the context menu and select Get Info. Chose ``Always trust``

 In order to make the certificate immediately available for signing, we need to restart the Taskgate access-control service.
 
 1. Open the Activity Monitor (found in Applications/Utilities)
 2. Open it and filter the list of processes by typing ``taskgated`` in the search field in the toolbar.  There will be one process. Stop it. Wait for it to restart or reboot if necessary
 3. Finally, open a terminal window and enter the following command. ::
 
    codesign -s gdbcert /usr/local/bin/gdb
