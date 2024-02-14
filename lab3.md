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

**-c**

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

The ```-c``` flag makes the command print the number of lines containing the pattern instead of the lines themselves. This flag is very useful for finding the number of instances of something, such as the number of patients with a certain infection in a hospital record or the number of football games with a final score of 20-13 in a database.

**-l**

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

The ```-l``` flag makes the command print the files that contain the pattern out of the given files. This flag is very useful for finding specific patterns in entire directories, such as finding which files in a hospital's directory contain a certain patient's data. Since it gives you a list of files that contain the pattern, the flag also enables further operations on those files (aka find the file with the most words out of files containing "Hello").
