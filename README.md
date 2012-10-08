# Ruby-Shells

These are very simple shells, normal and reverse I wrote in ruby to help in pen testing.  Simply you can use them to get a working shell on a box that won't be killed by AV, use it to kill AV then use it to upgrade to a meterperter session or whatever you like.  You can compile them to an executable file to run on systems with no ruby.

## revshell.rb
This is a classic reverse shell.  First change the IP and Port to what you want it to be.  Test it and if all is working setup your attacking box to accept the connections.  Then on a windows box with ruby and the ocra gem installed run this command:

ocra --verbose revshell.rb

Let it connect to your attacking box.  Then exit the conneciton which will finish the script and allowed it to be compiled.  Now you have a simple reverse shell .exe file that AV won't think twice about.

You can use the exploit/multi/handler with the generic/shell_reverse_tcp payload to let a ton of these connect back to you.


## shell.rb
This is a normal shell, it is a basic no-auth telnet server on the port you pick, kinda.  Once you connect to it to kill it on the server type IQuit!, otherwise it will stay open as long as you like.

Bug: The exist command works fine on everything other than Windows, I don't know why.  In Windows to kill it you have to kill the process or it will stay until reboot.

To compile it to a exe using ocra use the command:
 "ocra --verbose --no-dep-run --add-all-core shell.rb" 
 Since I didn't figure out a way to give it an exit command on Windows you have to use the -no-dep-run or the compile will hang forever.  The --add-all-core makes the file HUGE, which is no good.  I have not put the effort into figuring out what it really needs since I normally use the reverse shell, if someone else figures out a better way let me know.
 
### Limitations
The change directory command doesn't work.  So this: 
cd /etc
ls
doesn't work.  However, this:
ls /etc/
does. 
Also wildcards don't work.  So this:
ls /etc/*.conf
doesn't work.

Stay in the shell and don't try to go into another program.  If you vi a file say, it will run and show you the file, but you will never get out of vi and you lost your shell.