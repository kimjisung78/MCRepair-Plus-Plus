# Math 63
* <h4>Bug type: Type 2 (T1B / T1F, T2F)</h4>
* <h4>The number of chunks: 1 chunk (1 used chunk / 1 fixed chunk)</h4>
* <h4>The number of locations: 5 locations (1 used location / 1, 3, 4, 5 fixed locations)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/main/java/org/apache/commons/math/util/MathUtils.java: 416-418
    public static boolean equals(double x, double y) {
-       return (Double.isNaN(x) && Double.isNaN(y)) || x == y;
+       return equals(x, y, 1);
    }
```
<br>

## 2. Used chunks and locations - T1B
* The number of used chunks: 1 chunk
* The number of used locations: 1 location
```java
src/main/java/org/apache/commons/math/util/MathUtils.java: 417
return (Double.isNaN(x) && Double.isNaN(y)) || x == y;
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 23
    * T1F (17): 609, 610, 613, 614, 615, 625, 637, 645, 646, 692, 699, 701, 709, 712, 721, 730, 772
    * T2F (6): 708, 728, 746, 747, 778, 779
<br><br>

## 4. Examples of correct patches
### 4.1. 692nd patch - T1F
#### I. Fixed Result
```java
src/main/java/org/apache/commons/math/util/MathUtils.java: 121
-   return (Double.isNaN(x) && Double.isNaN(y)) || x == y;
+   return x == y || x == y;
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/main/java/org/apache/commons/math/util/MathUtils.java: 121
return x == y || x == y;
```

#### III. Explanation 
The result of a floating-point comparison, as determined by the specification of the IEEE 754 standard, is:
Floating-point equality testing is performed in accordance with the rules of the IEEE 754 standard:
* If either operand is NaN, then the result of == is false but the result of != is true. Indeed, the test x!=x is true if and only if the value of x is NaN. The methods Float.isNaN and Double.isNaN may also be used to test whether a value is NaN.
* Positive zero and negative zero are considered equal. For example, -0.0==0.0 is true.
* Otherwise, two distinct floating-point values are considered unequal by the equality operators. In particular, there is one value representing positive infinity and one value representing negative infinity; each compares equal only to itself, and each compares unequal to all other values.
```java
Float.NEGATIVE_INFINITY == Float.NEGATIVE_INFINITY // true
Double.NEGATIVE_INFINITY == Double.NEGATIVE_INFINITY // true
Float.POSITIVE_INFINITY == Float.POSITIVE_INFINITY // true
Double.NEGATIVE_INFINITY == Double.NEGATIVE_INFINITY // true
-0.0==0.0 // true
Float.NaN == Float.NaN // false
Double.NaN == Double.NaN // false
```
Hence, ```testArrayEquals``` testcase of the bug is as follows:
```java
public void testArrayEquals() {
    assertFalse(MathUtils.equals(new double[] { 1d }, null));
    assertFalse(MathUtils.equals(null, new double[] { 1d }));
    assertTrue(MathUtils.equals((double[]) null, (double[]) null));

    assertFalse(MathUtils.equals(new double[] { 1d }, new double[0]));
    assertTrue(MathUtils.equals(new double[] { 1d }, new double[] { 1d }));
    assertTrue(MathUtils.equals(
        new double[] { Double.POSITIVE_INFINITY, Double.NEGATIVE_INFINITY, 1d, 0d }, 
        new double[] { Double.POSITIVE_INFINITY, Double.NEGATIVE_INFINITY, 1d, 0d }
    ));
    assertFalse(MathUtils.equals(new double[] { Double.NaN }, new double[] { Double.NaN }));
    assertFalse(MathUtils.equals(new double[] { Double.POSITIVE_INFINITY }, new double[] { Double.NEGATIVE_INFINITY }));
    assertFalse(MathUtils.equals(new double[] { 1d }, new double[] { FastMath.nextAfter(FastMath.nextAfter(1d, 2d), 2d) }));
}
```
Because ```==``` operator provides mathematical comparisons, its source code returns false for ```NaN == NaN``` and true for ```-0.0 == 0.0```. Therefore, to fix the bug, ```==``` operator should be used except for ```NaN``` comparisons.
<br>

### 4.2. 728th patch - T2F
#### I. Fixed Result
```java
src/main/java/org/apache/commons/math/util/MathUtils.java: 121
-   return (Double.isNaN(x) && Double.isNaN(y)) || x == y;
+   if (x == y)
+       return false || x == y;
+   return false; 
```  

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 3 locations
```java
src/main/java/org/apache/commons/math/util/MathUtils.java: 121
if (x == y)
    return false || x == y;
return false;
```

#### III. Explanation 
Its reason is the same as the reason in the 692nd patch.
<br>

### 4.3. 746th patch - T2F
#### I. Fixed Result
```java
src/main/java/org/apache/commons/math/util/MathUtils.java: 121
-   return (Double.isNaN(x) && Double.isNaN(y)) || x == y;
+   if (x == y) {
+       return true; 
+   }
+   return false; 
```  

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 4 locations
```java
src/main/java/org/apache/commons/math/util/MathUtils.java: 121
if (x == y) {
    return true;
}
return false;
```

#### III. Explanation 
Its reason is the same as the reason in the 692nd patch.
<br>

### 4.4. 747th patch - T2F
#### I. Fixed Result
```java
src/main/java/org/apache/commons/math/util/MathUtils.java: 121
-   return (Double.isNaN(x) && Double.isNaN(y)) || x == y;
+   if (x == y) {
+       return true; 
+   } else { 
+       return false; 
+   }
```  

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 5 locations
```java
src/main/java/org/apache/commons/math/util/MathUtils.java: 121
if (x == y) {
    return true;
} else { 
    return false;
}
```

#### III. Explanation 
Its reason is the same as the reason in the 692nd patch.
<br><br>