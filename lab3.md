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
