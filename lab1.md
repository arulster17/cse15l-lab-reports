# cd with no arguments
```
[user@sahara ~/lecture1]$ cd
[user@sahara ~]$

# Working Directory: /home/lecture1
# Why this output: When cd is executed with no arguments, it sets the working directory back to the home directory. In this case, it sets the working directory to /home
# Error: This is not an error.
```

# cd with a path to a directory as an argument
```
[user@sahara ~/lecture1]$ cd messages
[user@sahara ~/lecture1/messages]$ 

# Working Directory: /home/lecture1
# Why this output: When cd is executed with a path to the directory as an argument, it makes that directory the working directory of the terminal.
# Error: This is not an error.
```

# cd with a path to a file as an argument
```
[user@sahara ~/lecture1]$ cd README
bash: cd: README: Not a directory
[user@sahara ~/lecture1]$ 

# Working Directory: /home/lecture1
# Why this output: cd is not equipped to handle a file as an argument, so the shell sends us a message telling us our argument is not of the required type.
# Error: This is an error, which we can see as bash sends us a message saying that our argument is not a directory.
```

# ls with no arguments
```
[user@sahara ~/lecture1]$ ls
Hello.class  Hello.java  messages  README
[user@sahara ~/lecture1]$ 

# Working Directory: /home/lecture1
# Why this output: When ls is executed with no arguments, it prints out the contents of the current directory
# Error: This is not an error.
```

# ls with a path to a directory as an argument
```
[user@sahara ~/lecture1]$ ls messages
en-us.txt  es-mx.txt  it.txt  zh-cn.txt
[user@sahara ~/lecture1]$ 

# Working Directory: /home/lecture1
# Why this output: When ls is executed with a path to a directory as an argument, it prints out the content of the directory
# Error: This is not an error.
```

# ls with a path to a file as an argument
```
[user@sahara ~/lecture1]$ ls README 
README
[user@sahara ~/lecture1]$

# Working Directory: /home/lecture1
# Why this output: When ls is executed with a path to a file as an argument, it will repeat the name of the file back to you. 
# Error: This is not an error.
```

# cd with no arguments
```
[user@sahara ~/lecture1]$ cat
test1
test1
test2
test2

# Working Directory: /home/lecture1
# Why this output: When cat is executed with no arguments, it waits for input and prints what it receives back to stdout.
# Error: This is not an error.
```

# cat with a path to a directory as an argument
```
[user@sahara ~/lecture1]$ cat messages
cat: messages: Is a directory
[user@sahara ~/lecture1]$ 

# Working Directory: /home/lecture1
# Why this output: cat is not equipped to handle directories as input, so it tells the caller that the input is a directory.
# Error: This is an error, which we can see as cat responded and threw the "messages: Is a directory" error and did nothing else.
```

# cat with a path to a file as an argument
```
[user@sahara ~/lecture1]$ cat messages/en-us.txt 
Hello World!
[user@sahara ~/lecture1]$ 

# Working Directory: /home/lecture1
# Why this output: When cat is executed with a path to a file as an argument, it will print out the contents of the file.
# Error: This is not an error.
```
