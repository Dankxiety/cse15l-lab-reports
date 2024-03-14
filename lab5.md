# Lab Report 5 - 7 March 2024
## Part 1 - Debugging Scenario
1. Student: I'm getting errors on all my MyArrayList methods when I try to compile the file using my bash script (see attached screenshots). It seems like I have some sort of issue with overriding methods from the MyList interface, but I'm not sure what the exact problem is.
<br />
Errors (there are more, they don't all fit in the screenshot):
<br />

<br />
Testing script:
```
javac -cp ".;..\libs\junit-4.13.2.jar;..\libs\hamcrest-2.2.jar" MyArrayListHiddenTester.java
javac -cp ".;..\libs\junit-4.13.2.jar;..\libs\hamcrest-2.2.jar" MyArrayListPublicTester.java
javac MyArrayList.java

java -cp ".;..\libs\junit-4.13.2.jar;..\libs\hamcrest-2.2.jar" org.junit.runner.JUnitCore MyArrayListHiddenTester
java -cp ".;..\libs\junit-4.13.2.jar;..\libs\hamcrest-2.2.jar" org.junit.runner.JUnitCore MyArrayListPublicTester
```
