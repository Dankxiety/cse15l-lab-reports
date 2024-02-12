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
<br />
2. `grep -c`
  - Example 1: `grep -c "heart" biomed/*.txt`
    ```
    $ grep -c "heart" biomed/*.txt
    biomed/1468-6708-3-1.txt:1
    biomed/1468-6708-3-10.txt:3
    biomed/1468-6708-3-3.txt:3
    biomed/1468-6708-3-4.txt:1
    biomed/1468-6708-3-7.txt:14
    biomed/1471-2091-2-10.txt:0
    biomed/1471-2091-2-11.txt:0
    biomed/1471-2091-2-12.txt:0
    biomed/1471-2091-2-13.txt:0
    biomed/1471-2091-2-16.txt:1
    ... many more ...
    ```
    This prints the number of lines in which the string "heart" appears in every file in `biomed`. This could be useful for "ranking" files based on how much information they contain relating to the heart.
  - Example 2: `grep -c "human" plos/*.txt`
    ```
    $ grep -c "human" plos/*.txt
    plos/journal.pbio.0020001.txt:0
    plos/journal.pbio.0020010.txt:0
    plos/journal.pbio.0020012.txt:14
    plos/journal.pbio.0020013.txt:0
    plos/journal.pbio.0020019.txt:0
    plos/journal.pbio.0020028.txt:3
    plos/journal.pbio.0020035.txt:1
    plos/journal.pbio.0020040.txt:2
    plos/journal.pbio.0020042.txt:1
    plos/journal.pbio.0020043.txt:4
    plos/journal.pbio.0020046.txt:0
    ... many more ...
    ```
    This prints the number of lines in which the string "human" appears in every file in `plos`. This could be useful for "ranking" which files based on how much information they contain relevant to humans.
<br />
3. `grep -l`
  - Example 1: `grep -l "leaf" biomed/*.txt`
    ```
    $ grep -l "leaf" biomed/*.txt
    biomed/1471-2164-4-26.txt
    biomed/1471-2180-3-5.txt
    biomed/1471-2229-1-3.txt
    biomed/1471-2229-2-8.txt
    biomed/1471-2229-2-9.txt
    biomed/1472-6785-1-3.txt
    biomed/1472-6785-2-7.txt
    biomed/1472-6882-1-10.txt
    biomed/1472-6882-1-7.txt
    biomed/gb-2001-2-11-research0045.txt
    biomed/gb-2002-3-9-research0045.txt
    biomed/gb-2002-3-9-research0049.txt
    biomed/gb-2003-4-1-r5.txt
    biomed/gb-2003-4-3-r20.txt
    ```
    This prints the path of every file which contains the string "leaf" in `biomed`. This is useful for finding all the files that may contain information about leaves.
  - Example 2: `grep -l "Canada" government/*/*.txt`
    ```
    $ grep -l "Canada" government/*/*.txt
    government/About_LSC/ONTARIO_LEGAL_AID_SERIES.txt
    government/About_LSC/Progress_report.txt
    government/About_LSC/Strategic_report.txt
    government/Env_Prot_Agen/atx1-6.txt
    government/Env_Prot_Agen/ctf1-6.txt
    government/Env_Prot_Agen/ctm4-10.txt
    government/Env_Prot_Agen/multi102902.txt
    government/Env_Prot_Agen/ro_clear_skies_book.txt
    government/Gen_Account_Office/ai00134.txt
    government/Gen_Account_Office/ai9868.txt
    government/Gen_Account_Office/d01376g.txt
    government/Gen_Account_Office/d01591sp.txt
    government/Gen_Account_Office/d0269g.txt
    government/Gen_Account_Office/gg96118.txt
    government/Gen_Account_Office/May1998_ai98068.txt
    government/Gen_Account_Office/Oct15-2001_d0224.txt
    government/Gen_Account_Office/pe1019.txt
    government/Media/Assuring_Underprivileged.txt
    government/Media/Few_who_need.txt
    government/Post_Rate_Comm/Cohenetal_comparison.txt
    government/Post_Rate_Comm/Cohenetal_Cost_Function.txt
    government/Post_Rate_Comm/Mitchell_RMVancouver.txt
    government/Post_Rate_Comm/Redacted_Study.txt
    ```
    This prints the path of every file which contains the string "Canada" in `government`. This is useful for finding all the files that mention Canada.
<br />
4. `grep -i`
  - Example 1: `grep -i "biology" plos/*.txt`
    ```
    $ grep -i "biology" plos/*.txt
    plos/journal.pbio.0020001.txt:        the area of ecology (including the fields of evolutionary biology, conservation biology,
    plos/journal.pbio.0020001.txt:        and global change biology) between 1990 and 2002 in both the two top general science
    plos/journal.pbio.0020012.txt:        properties and physiological developments. “We've had a separation of the biology of ageing
    plos/journal.pbio.0020028.txt:        biology in the last couple decades,” and since it was first recognized by Andrew Fire et
    plos/journal.pbio.0020028.txt:        Biology at City of Hope Hospital in Duarte, California, who has worked on RNA-based
    plos/journal.pbio.0020035.txt:        PloS Biology , is that the PKSs for these compounds consist of two
    plos/journal.pbio.0020040.txt:        PLoS Biology , Trotman et al. (2003) used mouse models to describe how
    plos/journal.pbio.0020042.txt:        into microarray analysis, proteomic initiatives, and even systems biology, it seems an
    plos/journal.pbio.0020042.txt:        of its biology.
    ... many more ...
    ```
    This prints every line containing "biology" in `plos` without case sensitivity. This is useful for making sure that all mentions of biology are included in the search, including instances where it may be at the beginning of a sentence or part of a proper noun.
  - Example 2: `grep -i "president" government/*/*.txt`
    ```
    $ grep -i "president" government/*/*.txt
    government/About_LSC/Comments_on_semiannual.txt:President of the United States with the advice and consent of the
    government/About_LSC/Comments_on_semiannual.txt:Senate. The Board appoints LSC's President, who serves as the
    government/About_LSC/commission_report.txt:John McKay, President Danilo A. Cardona, A cting V ice President
    government/About_LSC/commission_report.txt:Fortuno, V ice President for Legal A ffairs, General Counsel and
    government/About_LSC/commission_report.txt:Corporate Secretary James J. Hogan, V ice President for A
    government/About_LSC/commission_report.txt:dministration Mauricio Vivero, V ice President for Governmental
    government/About_LSC/commission_report.txt:to the President John Kennedy, Director of A dministration and
    government/About_LSC/commission_report.txt:are appointed by the President of the United States with the advice
    government/About_LSC/commission_report.txt:of the demand for service. See id. The President of the North
    government/About_LSC/commission_report.txt:Gilbert Casellas is currently the President and Chief Operating
    government/About_LSC/commission_report.txt:civilian, and reserve attorneys. In 1994, President Clinton
    government/About_LSC/commission_report.txt:has served as President of the Hispanic National Bar Association,
    ... many more ...
    ```
    This prints every line containing "president" in `government` without case sensitivity. Again, this is useful for including all mentions of presidency, including those which are capitalised for any reason.
<br />
<br />
I found the documentation for all of these command-line options by using the command `man grep`.
