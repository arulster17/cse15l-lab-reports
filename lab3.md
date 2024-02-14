# LAB REPORT 3

## PART 1
I chose the bug in the ```reverseInPlace(int[] arr)``` method in ```ArrayExamples.java```

**Failure-Inducing Input**
```
@Test
public void testReverseInPlaceFail() {
  int[] input1 = {1, 2, 3};
  ArrayExamples.reverseInPlace(input1);
  assertArrayEquals(new int[]{3, 2, 1}, input1);
}
```

**Non-Failure-Inducing Input**
```
@Test 
public void testReverseInPlacePass() {
  int[] input1 = {1, 2, 1};
  ArrayExamples.reverseInPlace(input1);
  assertArrayEquals(new int[]{1, 2, 1}, input1);
}
```

**Symptom**
![Symptom](/lab3symptoms.png)

**Bug**

*Before*
```
static void reverseInPlace(int[] arr) {
  for(int i = 0; i < arr.length; i += 1) {
  arr[i] = arr[arr.length - i - 1];
  }
}
```
*After*
```
static void reverseInPlace(int[] arr) {
  for(int i = 0; i < arr.length/2; i += 1) {
    int temp = arr[i];
    arr[i] = arr[arr.length - i - 1];
    arr[arr.length - i - 1] = temp;
  }
}
```

**Why the Fix Works**

The original code tries to loop through the whole array and replace each element ```arr[i]``` with the element at the opposite index, ```arr[arr.length - i - 1]```. However, when we reach the second half of the array, the first half of the array has already been overwritten, and the data previously there is lost. We fix this by simply iterating through the first half of the array and using a temporary variable to switch data between entries.

## PART 2

I chose the ```grep``` command. We will examine the following 4 command-line options: ```-c, -l, -r, --context```.

# ```-c``` flag

*Example 1*
```
main:docsearch$ grep -c "adenoviral" technical/biomed/ar104.txt
7
```

*Example 2*
```
main:docsearch$ grep -c "Coyne" technical/plos/journal.pbio.0030062.txt
22
```

The ```-c``` flag makes the command print the number of lines containing the pattern instead of the lines themselves. This flag is very useful for finding the number of instances of something, such as the number of patients with a certain infection in a hospital record or the number of football games with a final score of ```20-13``` in a database.

# ```-l``` flag

*Example 1*
```
main:docsearch$ grep -l "Darwin" technical/*/*.txt
technical/biomed/1471-2105-3-2.txt
technical/plos/journal.pbio.0020046.txt
technical/plos/journal.pbio.0020071.txt
technical/plos/journal.pbio.0020302.txt
technical/plos/journal.pbio.0020311.txt
technical/plos/journal.pbio.0020346.txt
technical/plos/journal.pbio.0020347.txt
technical/plos/journal.pbio.0020439.txt

```

*Example 2*
```
main:docsearch$ grep -l "Coyne" technical/plos/*.txt                   
technical/plos/journal.pbio.0020420.txt
technical/plos/journal.pbio.0030062.txt
```

The ```-l``` flag makes the command print the files that contain the pattern out of the given files. This flag is very useful for finding all files with specific patterns in a directory, such as finding which logs in a logbook contain ```"Error"```. Since it gives you a list of files that contain the pattern, the flag also enables further operations on those files. This flag often benefits from the use of the ```-r``` flag, which we discuss next.

# ```-r``` flag

*Example 1*
```
main:docsearch$ grep -rl "Darwin" technical/       
technical//plos/journal.pbio.0020347.txt
technical//plos/journal.pbio.0020346.txt
technical//plos/journal.pbio.0020046.txt
technical//plos/journal.pbio.0020302.txt
technical//plos/journal.pbio.0020311.txt
technical//plos/journal.pbio.0020071.txt
technical//plos/journal.pbio.0020439.txt
technical//biomed/1471-2105-3-2.txt
```

*Example 2*
```
main:docsearch$ grep -r "grape" technical
technical/plos/journal.pbio.0020224.txt:        Dactylosphera vitifoliae devastated European grapewine varieties
technical/plos/journal.pbio.0020214.txt:        2004). The grapevine distributes stories of “bad words” that should be avoided when
technical/biomed/1471-2229-3-3.txt:        grapevine and tomato [ 34 ] . The locus PM50 contains only
technical/biomed/1472-6750-2-2.txt:        Biological control by F2/5 is grape-specific, as F2/5 is
technical/biomed/1472-6750-2-2.txt:        not effective on non-grapevine host plants such as 
technical/biomed/1472-6750-2-2.txt:        grape would be beneficial for disease control in field
technical/911report/chapter-12.txt:                about the size of a grapefruit or an orange, together with commercially available
```

The ```-r``` flag makes the command recursively read and search for the pattern in all files. This flag is very useful for finding all instances of a specific pattern in a directory, and it essentially extends the power of ```grep``` to search entire directories. In my opinion, this is the most useful ```grep``` flag.

# ```--context``` flag

*Example 1*
```
main:docsearch$ grep --context "grapewine" technical/plos/journal.pbio.0020224.txt
        attributes of the rootstock with those of the donor plant shoot, or scion. Grafting
        essentially saved European wine making: when the insect 
        Dactylosphera vitifoliae devastated European grapewine varieties
        over the course of the late 1800s and early 1900s, the varieties were saved by grafting
        them onto resistant rootstocks from the New World. Since then, these rootstocks have been
```

*Example 2*
```
main:docsearch$ grep --context=1 "pineapple" technical/biomed/1472-6882-1-10.txt
          scorpion stings in dogs makes use of steroids,
          antibiotics and the ananase enzyme (from the pineapple 
          Ananas comosus ) and needs to take
```

The ```--context[=num]``` flag prints the ```num``` lines before and after the line with the match (```num``` has a default value of 2). This flag is extremely useful for peeking into matches in large files, such as looking at contextual chat messages near a flagged message in a log. While this may not be as useful in scripting as ```-r``` or ```-l```, it is very convenient for users to investigate more into the pattern matches.

