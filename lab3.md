# Lab Report 2 - 8 Feb 2024
## Part 1 - Bugs
- Failure-inducing input:
```
@Test 
public void testReverseInPlace() {
  int[] input1 = {5, 9, 10, 2, 6};
  ArrayExamples.reverseInPlace(input1);
  assertArrayEquals(new int[]{6, 2, 10, 9, 5}, input1);
}
```
- Non-failure-inducing input:
```
@Test 
public void testReverseInPlace2() {
  int[] input1 = { 3 };
  ArrayExamples.reverseInPlace(input1);
  assertArrayEquals(new int[]{ 3 }, input1);
}
```
- Symptom:
```
JUnit version 4.13.2
..E
Time: 0.016
There was 1 failure:
1) testReverseInPlace(ArrayTests)
arrays first differed at element [3]; expected:<9> but was:<2>
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:78)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:28)
        at org.junit.Assert.internalArrayEquals(Assert.java:534)
        at org.junit.Assert.assertArrayEquals(Assert.java:418)
        at org.junit.Assert.assertArrayEquals(Assert.java:429)
        at ArrayTests.testReverseInPlace(ArrayTests.java:9)
        ... 32 trimmed
Caused by: java.lang.AssertionError: expected:<9> but was:<2>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at org.junit.internal.ExactComparisonCriteria.assertElementsEqual(ExactComparisonCriteria.java:8)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:76)
        ... 38 more
‎ 
FAILURES!!!
Tests run: 2,  Failures: 1
```
- Bug:
  <br />
  Before:
  ```
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
  ```
  After:
  ```
  static void reverseInPlace(int[] arr) {
    int[] newArr = new int[arr.length];
‎ 
    for(int i = 0; i < arr.length; i += 1) {
      newArr[i] = arr[arr.length - i - 1];
    }
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArr[i];
    }
  }
  ```
The previous code used a for loop to directly alter the array, replacing elements starting from the front with the corresponding elements starting from the end. However, because the array's new elements were pulled directly from the array itself, the latter half of the array would pull from the elements that had already been replaced; i.e. the second half of the array woud simply mirror the first. The new code fixes the issue by creating a temporary new array, copying the elements from the old array in reverse order, and then copying the elements from the new array into the old array.
```
<br />
## Part 2 - Researching Commands (grep)
1. `grep -n`
  - Example 1: `grep -n "biomedical" biomed/*.txt`
    ```
    $ grep -n "biomedical" biomed/*.txt
    biomed/1471-2105-3-16.txt:16:        The availability of biomedical literature in electronic
    biomed/1471-2105-3-17.txt:526:        study aimed at enabling the biomedical community to cope
    biomed/1471-2164-3-7.txt:8:        of biomedical research. These include, but are by no means
    biomed/1472-6807-1-1.txt:17:        types of ligands could therefore have important biomedical
    biomed/1472-6882-1-12.txt:472:        biomedical framework. While the SR method has been used in
    biomed/1472-6882-3-3.txt:22:        biomedical literature [ 3 ] . With the recent development
    biomed/1472-6882-3-3.txt:49:        Other biomedical databases that include CAM literature,
    biomed/1472-6920-2-3.txt:214:        international journals [ 5 ] . For biomedical disciplines
    biomed/1472-6947-3-5.txt:49:        another level of biomedical data integration in which array
    biomed/1472-6947-3-8.txt:56:          Creators of biomedical databases use terminologies to
    biomed/1472-6947-3-8.txt:624:        biomedical data sets. Public comment is welcomed.
    biomed/1475-9276-1-3.txt:143:        33 34 ] . This model has been widely applied in biomedical
    biomed/1477-7827-1-54.txt:695:        study increases the biomedical significance of findings
    biomed/gb-2001-2-4-research0012.txt:532:        to biomedical education, investigation and industry. For
    biomed/gb-2003-4-4-r28.txt:493:        biomedical research community. GoMiner is flexible both
    biomed/gb-2003-4-7-r46.txt:75:        gene annotations or concepts from the biomedical
    ```
    This prints every instance of the string "biomedical" in the `biomed` folder, along with the line numbers of every such instance. This is useful for locating the exact lines where a given string appears.
  - Example 2: `grep -n "marital" government/*/*.txt`
    ```
    $ grep -n "marital" government/*/*.txt
    government/Alcohol_Problems/Session3-PDF.txt:1546:change, and marital or employment status. He thought natural
    government/Gen_Account_Office/d03273g.txt:1030:marital status).
    government/Media/Firm_to_the_Poor_Needs_Help.txt:33:unemployment, marital problems and deeper poverty."
    government/Media/Legal_Aid_in_Clay_County.txt:58:victims need to legally sever their marital relationship with their
    government/Media/Retirement_Has_Its_Appeal.txt:88:month to keep the group's members up to date on marital law and
    government/Post_Rate_Comm/WolakSpeech_usps.txt:85:head and spouse, age and race of head and spouse, marital status,
    ```
    This prints every instance of the string "marital" in the `government` folder, along with the line numbers of every such instance. Again, this is useful for locating exactly where certain information pertaining to marriage appears.
2. 
