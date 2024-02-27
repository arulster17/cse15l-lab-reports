# LAB REPORT 4

***Step 4: Log into ieng6***

![img](/labreport4img4.png)

Keys Pressed: ```<up> <enter>```

The ```ssh armathur@ieng6.ucsd.edu``` command was 1 up in my history, so I used the up arrow to access it. This command lets me SSH into the ieng6 remote server.

***Step 5: Clone your fork of the repository from your Github account***

![img](/labreport4img5.png)

Keys Pressed: ```<Cmd + V> <enter>```

I had the command ```git clone git@github.com:arulster17/lab7.git``` copied on my clipboard, so I used my computer's paste function to input it into the command line. This command clones the code from the GitHub repository and adds the code to my file system.

***Step 6: Run the tests, demonstrating that they fail***

![img](/labreport4img6.png)

Keys Pressed: ```cd <space> l <tab> <enter>```, ```bash t <tab> <enter>```

When ```cd l``` is typed into the command line, pressing ```<tab>``` will make the command autocomplete to ```cd lab7/```, as ```lab7``` is the only thing that starts with ```l``` in the working directory, Similarly, upon typing ```bash t```, pressing ```<tab>``` will make the command autocomplete to ```bash test.sh```, as ```test.sh``` is the only thing that starts with ```t``` in the working directory. The ```cd lab7/``` command moves the working directory into the cloned folder to continue work. The ```bash test.sh``` command runs the testing script.

***Step 7: Edit the code file to fix the failing test***

![img](/labreport4img7a.png)

![img](/labreport4img7b.png)

Keys Pressed: ```vim L <tab> . <tab> <enter>```, ```43 <enter> e r 2 :wq <enter>```

When ```vim L``` is typed into the command line, pressing ```<tab>``` fills the command to ```vim ListExamples```, as the two matching text files in the directory are ```ListExamples.java``` and ``` ListExamplesTests.java```. Typing ```.``` and pressing ```<tab>``` again makes the command ```vim ListExamples.java```. Now that we are in vim and are at the head of the file, we can type ```43 <enter>``` to jump to the front of line 44 (1 + 43). Pressing ```e``` takes us to the end of the first word, which is ```index1```. Since we want to change the ```index1``` to ```index2```, we can type ```r``` to enter replace mode and type ```2```. To save our work, we can now type ```:wq <enter>```. This set of commands opens the file in the vim editor, jumps to the word to be changed, makes the necessary change, and saves the corrected file.

***Step 8: Run the tests, demonstrating that they now succeed***

![img](/labreport4img8.png)

Keys Pressed: ```<up> <up> <enter>```

Since we ran the test script just before we used vim, we know the testing command is 2 up in our history. We can access it by pressing up 2 times and hitting enter. This command runs the testing script again, which now shows that all tests pass.

***Step 9: Commit and push the resulting change to your Github account***

![img](/labreport4img9.png)

Keys Pressed: ```git commit -am . <enter>```, ```git push <enter>```

The ```-a``` flag for git commit essentially tells git to stage all modified files for commit (in this case ```ListExamples.java```). We also add the ```-m``` flag and give ```.``` as the commit message. We can then push the code to the repository and we are done.
