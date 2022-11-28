# Lab Report 5
## `grade.sh`
```
# Create your grading script here
# set -e

rm -rf student-submission           # Clears previous submission
git clone $1 student-submission     # Clones new submission to local

# Sample Submissions
# https://github.com/ucsd-cse15l-f22/list-methods-lab3
# https://github.com/ucsd-cse15l-f22/list-methods-corrected     ... fixed
# https://github.com/ucsd-cse15l-f22/list-methods-compile-error ... syntax error
# https://github.com/ucsd-cse15l-f22/list-methods-signature     ... wrong order for filter
# https://github.com/ucsd-cse15l-f22/list-methods-filename      ... wrong filename
# https://github.com/ucsd-cse15l-f22/list-methods-nested        ... nested directory
# https://github.com/ucsd-cse15l-f22/list-examples-subtle       ... subtle mistakes

echo "Grading Repo: $1 ..."
echo '----------------------------------------------------------'
SCORE=0;
JPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar'
# javac -cp $JUPATH TestListExamples.java
if [[ -e student-submission/ListExamples.java ]]; then
    echo '[+1 point] Submitted with correct file name and path!!'
    SCORE=$(( SCORE + 1 ))
    cp student-submission/ListExamples.java .
    echo > CompileErrors.log # Clears log from previous if it exists
    echo > TestErrors.log    # Clears log from previous if it exists
    javac -cp $JPATH ListExamples.java TestListExamples.java 2> CompileErrors.log
    if [[ $? -eq 0 ]]; then
        SCORE=$(( SCORE + 1 ))
        echo '[+1 point] File compiled with success!!'
        java -cp $JPATH org.junit.runner.JUnitCore TestListExamples 1> TestErrors.log
        if grep -q 'testFilter' TestErrors.log; then
            echo '[+0 point] Filter - Test failed.. check TestErrors.log for details'
        else
            SCORE=$(( SCORE + 1 ))
            echo '[+1 point] Filter - Regular case success!!'
        fi
        if grep -q 'testMergeReg' TestErrors.log; then
            echo '[+0 point] Merge - Regular case failed.. check TestErrors.log for details'
        else
            SCORE=$(( SCORE + 1 ))
            echo '[+1 point] Merge - Regular case success!!'
        fi
        if grep -q testMergeDupe TestErrors.log; then
            echo '[+0 point] Merge - Duplicate case failed.. check TestErrors.log for details'
        else
            SCORE=$(( SCORE + 1 ))
            echo '[+1 point] Merge -  Duplicate case success!!'
        fi
    else
        echo '[+0 point] Compile errors found. Check CompileErors.log'
    fi
else
    echo '[+0 point] File not found, expected path is: student-submission/ListExamples.java'
fi
echo '----------------------------------------------------------'
echo "Total score is ${SCORE}/5 points"

rm -f ListExamples.java   # Removes copied java file
```

## Repos Tested by Autograder
### Compile Error
![](./compile.png)
---
**Syntax error on script halts further testing.**

### Filter Error
![](./filter.png)
---
**Code appends to front instead of back, resulting a different list**

### Merge Error
![](./merge.png)
---
**Duplicate cases aren't considered for the implementation**

## Trace for `list-methods-compile-error`

`rm -rf student-submission`
> stdout: none <br> stderr: none <br> return: zero

`git clone $1 student-submission`
> stdout: none <br> stderr: none <br> return: zero

`echo "Grading Repo: $1 ..."`
> stdout: Grading Repo: https://github.com/ucsd-cse15l-f22/list-methods-compile-error ... <br> stderr: none <br> return: zero

`echo '----------------------------------------------------------'`
> stdout: ---------------------------------------------------------- <br> stderr: none <br> return: zero

`if [[ -e student-submission/ListExamples.java ]]; then`
> **True**, because correct file name copied from list-methods-compile-error/ListExamples.java <br> stdout: none <br> stderr: none <br> return: zero

`echo [+1 point] Submitted with correct file name and path!!`
> stdout: [+1 point] Submitted with correct file name and path!! <br> stderr: none <br> return: zero

`cp student-submission/ListExamples.java .`
> stdout: none <br> stderr: none <br> return: zero

`echo > CompileErrors.log`
> stdout: none <br> stderr: none <br> return: zero

`echo > TestErrors.log`
> stdout: none <br> stderr: none <br> return: zero
    
`javac -cp $JPATH ListExamples.java TestListExamples.java`
> stdout: none <br> stderr: <br> ListExamples.java:15: error: ';' expected <br>         result.add(0, s)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ^ <br> 1 error <br> return: 1

`if [[ $? -eq 0 ]]; then`
> **False**, because correct file name copied from list-methods-compile-error/ListExamples.java <br> stdout: none <br> stderr: none <br> return: zero

```
echo '[+1 point] File compiled with success!!'
java -cp $JPATH org.junit.runner.JUnitCore TestListExamples 1> TestErrors.log
        if grep -q 'testFilter' TestErrors.log; then
            echo '[+0 point] Filter - Test failed.. check TestErrors.log for details'
        else
            SCORE=$(( SCORE + 1 ))
            echo '[+1 point] Filter - Regular case success!!'
        fi
        if grep -q 'testMergeReg' TestErrors.log; then
            echo '[+0 point] Merge - Regular case failed.. check TestErrors.log for details'
        else
            SCORE=$(( SCORE + 1 ))
            echo '[+1 point] Merge - Regular case success!!'
        fi
        if grep -q testMergeDupe TestErrors.log; then
            echo '[+0 point] Merge - Duplicate case failed.. check TestErrors.log for details'
        else
            SCORE=$(( SCORE + 1 ))
            echo '[+1 point] Merge -  Duplicate case success!!'
        fi
```
> This block doesn't run at all due to false condition
    else
        echo '[+0 point] Compile errors found. Check CompileErors.log'
    fi
else
    echo '[+0 point] File not found, expected path is: student-submission/ListExamples.java'
fi
echo '----------------------------------------------------------'
echo "Total score is ${SCORE}/5 points"

rm -f ListExamples.java   # Removes copied java file


> It took `2:06` minutes with VScode locally and SCPing, and `1:05` minutes with VIM on remote.

* Which of these two styles would you prefer using if you had to work on a program that you were running remotely, and why?
  >Even if the program were to run remotely, I would still prefer VScode because it allows me more functionality and I am more accustomed to it.
For minor edits, however, I'd rather prefer vim.

* What about the project or task might factor into your decision one way or another? <br> (If nothing would affect your decision, say so and why!)
  >If the project involves lots of coding and planning, I would rather port the files locally and work on my own system. However, if the project involves few lines of codes or edits, I would rather have VIM open and work directly from there.
