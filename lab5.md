# LAB REPORT 5

***EdStem Conversation***

Student: Hi. After running my grader on a certain student repository and trying to grade another repository afterwards, I get the following issue:
![img](/lab5symptom.png)
It looks like my grade.sh file is completely gone. I think that at some point during the execution my grade.sh file is removed.

TA: You seem to have identified the symptom correctly. Is there something in your grade.sh file that messes with the file itself? If not, can you investigate the student submission and see if they have something to do with it?

Student: Ah, I found this in the student submission. It seems they just use java processes to run console commands and deleted my grade.sh file.
# insert issue image here

Student: I fixed the issue by using Java's SecurityManager feature. 

Here is the original file structure:
```
grader-review-arulster17
  |-> TestListExamples.java
  |-> grade.sh
  |-> lib
```

Here is the new file structure: 
```
grader-review-arulster17
  |-> TestListExamples.java
  |-> grade.sh
  |-> lib
```

Here is the original ```TestExamplesList.java```:
# insert image

Here is the new ```TestExamplesList.java```:
# insert image

Here is the original ```grade.sh```:

Here is the new ```grade.sh```:

Here are the contents of the new file ```mysecurity.policy```:


// created mysecurity.policy file
// added before clause to TestListExamples.java that started the java security manager
// added cp mysecurity.policy to grade.sh
