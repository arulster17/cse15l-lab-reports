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

