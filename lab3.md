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
