# Lab Report 3 - Bugs and Commands 
## Part 1 - Bugs
**The Bug:**
```
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
```

**Failure Inducing Input**
```
  @Test
  public void testReversed1() {
    int[] input1 = {1, 2, 3};
    assertArrayEquals(new int[]{3, 2, 1}, ArrayExamples.reversed(input1));
  }
```

**Input That Doesn't Induce Failure**
```
  @Test
  public void testReversed() {
    int[] input1 = {0, 0};
    assertArrayEquals(new int[]{0, 0}, ArrayExamples.reversed(input1));
  }
```

**The Symptom**
![image one](144853.png)

**The Fix**
Before
```
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
```
After
```
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      newArray[i] = arr[arr.length - i - 1];
    }
    return newArray;
  }
```

**Explanation**
The fix addresses the issue as prior to its implementation the original array, `arr`, was being updated instead of the new array that is supposed to be returned to the user, `newArray`. When this code was run prior to being fixed it returned an array of 0s since the values of `newArray` were never updated.

## Part 2 - Researching Commands

