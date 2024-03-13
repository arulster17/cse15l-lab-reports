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
  |-> mysecurity.policy
```

Here is the original ```TestListExamples.java```:
```
import static org.junit.Assert.*;
import org.junit.*;
import java.util.Arrays;
import java.util.List;

class IsMoon implements StringChecker {
  public boolean checkString(String s) {
    return s.equalsIgnoreCase("moon");
  }
}

public class TestListExamples {
  @Test(timeout = 500)
  public void testMergeRightEnd() {
    List<String> left = Arrays.asList("a", "b", "c");
    List<String> right = Arrays.asList("a", "d");
    List<String> merged = ListExamples.merge(left, right);
    List<String> expected = Arrays.asList("a", "a", "b", "c", "d");
    assertEquals(expected, merged);
  }

  @Test(timeout = 500)
  public void testFilter() {
    List<String> left = Arrays.asList("a", "b", "c", "moOn");
    StringChecker sc = new IsMoon();
    List<String> moons = ListExamples.filter(left, sc);
    List<String> expected = Arrays.asList("moOn");
    assertEquals(expected, moons);
  }
}
```

Here is the new ```TestListExamples.java```:
```
import ... (other imports remain unchanged)
import org.junit.Before;

class IsMoon implements StringChecker {
  // unchanged
}

public class TestListExamples {
  @Before
  public void setup() {
    System.setProperty("java.security.policy", "mysecurity.policy");
    System.setSecurityManager(new SecurityManager());
  }

  // other tests remain unchanged
}
```

Here is the original ```grade.sh```:
```
CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar'

rm -rf student-submission
rm -rf grading-area


mkdir grading-area
git clone $1 student-submission &> /dev/null
echo 'Finished cloning.'

bab=$(find student-submission | grep "ListExamples.java" | head -n 1)

echo $bab

if [[ bab != "" ]]
then
	cp TestListExamples.java grading-area
	cp $bab grading-area
	cp -r lib grading-area
else
	echo 'Missing ListExamples.java, did you forget the file or misname it?'
	exit 1
fi

# Draw a picture/take notes on the directory structure that's set up after
# getting to this point

# Then, add here code to compile and run, and do any post-processing of the
# tests

cd grading-area
javac -cp $CPATH *.java

if [[ $? -ne 0 ]]
then
	echo "Compilation error, see error above."
	exit 1
else
	echo "Compilation successful."
fi

java -cp $CPATH org.junit.runner.JUnitCore TestListExamples > junitoutput.txt

cat junitoutput.txt | grep 'OK' > dave.txt

if [[ -s dave.txt ]]
then
	tests=$(cat dave.txt | grep -o '[0-9]\+')
	successes=$((tests))
else
	cat junitoutput.txt | tail -n 2 | head -n 1 > result.txt
	tests=$(cat result.txt | grep -o '[0-9]\+' | head -n 1)
	failures=$(cat result.txt | grep -o '[0-9]\+' | tail -n 1)
	successes=$((tests - failures))

fi
echo "Your score is $successes/$tests"
```

Here is the new ```grade.sh```:
```
// above unchanged

if [[ bab != "" ]]
then
	cp TestListExamples.java grading-area
	cp $bab grading-area
	cp -r lib grading-area
  cp mysecurity.policy grading-area # <--- added this line

else
	echo 'Missing ListExamples.java, did you forget the file or misname it?'
	exit 1
fi

// below unchanged
```

Here are the contents of the new file ```mysecurity.policy```:
```grant{};```

// created mysecurity.policy file
// added before clause to TestListExamples.java that started the java security manager
// added cp mysecurity.policy to grade.sh
