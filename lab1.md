# cd with no arguments
```
[user@sahara ~/lecture1]$ cd
[user@sahara ~]$

# Working Directory: /home/lecture1
# Why this output: When cd is executed with no arguments, it sets the working directory
#                  back to the home directory. In this case, it sets the working directory to /home
# Error: This is not an error, as this is the expected behavior of cd without args.

```

# cd with a path to a directory
```
[user@sahara ~/lecture1]$ cd messages
[user@sahara ~/lecture1/messages]$ 

# Working Directory: /home/lecture1
# Why this output: When cd is executed with a path to the directory, it makes
#                  that directory the working directory of the terminal.
# Error: This is not an error, as this is again the expected behavior of cd with a directory argument.

```

# cd with a path to a file
```
[user@sahara ~/lecture1]$ cd README
bash: cd: README: Not a directory
[user@sahara ~/lecture1]$ 

# Working Directory: /home/lecture1
# Why this output: cd is not equipped to handle a file as an argument, so the shell
#                  sends us a message telling us our argument is not of the required type.
# Error: This is an error, which we can see as bash sends us a message saying that our
#        argument is not a directory.

```
