# Math 86
* <h4>Bug type: Type 3 (T3B / T3F)</h4>
* <h4>The number of chunks: 2 chunks (2 used chunks / 2 fixed chunks)</h4>
* <h4>The number of locations: 6 locations (4 used locations / 5, 6 fixed locations)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/java/org/apache/commons/math/linear/CholeskyDecompositionImpl.java: 112-116
    final double[] lI = lTData[i];

-   if (lTData[i][i] < absolutePositivityThreshold) {
-       throw new NotPositiveDefiniteMatrixException();
-   }
```
* Location 113 is not a blank location related to "FAULT_OF_OMISSION."

```java
src/java/org/apache/commons/math/linear/CholeskyDecompositionImpl.java: 134-138
    final double[] ltI = lTData[i];

    // check diagonal element
+   if (ltI[i] < absolutePositivityThreshold) {
+       throw new NotPositiveDefiniteMatrixException();
+   }

    tI[i] = Math.sqrt(ltI[i]);
```
* Location 135, 136 and 137 are not blank or comment locations related to "FAULT_OF_OMISSION."
<br>

## 2. Used chunks and locations - T3B
* The number of used chunks: 2 chunks
* The number of used locations: 4 locations
```java
src/java/org/apache/commons/math/linear/CholeskyDecompositionImpl.java: 114-116
if (lTData[i][i] < absolutePositivityThreshold) {
    throw new NotPositiveDefiniteMatrixException();
}
```

```java
src/java/org/apache/commons/math/linear/CholeskyDecompositionImpl.java: 138
FAULT_OF_OMISSION
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 2
    * T3F (2): 1, 2
<br><br>

## 4. Examples of correct patches
### 4.1. 1st patch - T3F
#### I. Fixed Result
```java
src/java/org/apache/commons/math/linear/CholeskyDecompositionImpl.java: 114-116
-   if (lTData[i][i] < absolutePositivityThreshold) {
-       throw new NotPositiveDefiniteMatrixException();
-   }
```

```java
src/java/org/apache/commons/math/linear/CholeskyDecompositionImpl.java: 138
+   if (lTData[i][i] < absolutePositivityThreshold) {
+       throw new NotPositiveDefiniteMatrixException();
+   }
    tI[i] = Math.sqrt(ltI[i]);
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 2 chunks
* The number of fixed locations: 6 locations
```java
src/java/org/apache/commons/math/linear/CholeskyDecompositionImpl.java: 114-116
Location 114 was deleted.
Location 115 was deleted.
Location 116 was deleted.
```

```java
src/java/org/apache/commons/math/linear/CholeskyDecompositionImpl.java: 138
Three locations was inserted in front of Location 138.
```

#### III. Explanation
```lTData[i][i]``` is a diagonal element, too.
<br>

### 4.2. 2nd patch - T3F
#### I. Fixed Result
```java
src/java/org/apache/commons/math/linear/CholeskyDecompositionImpl.java: 114-116
-   if (lTData[i][i] < absolutePositivityThreshold) {
-       throw new NotPositiveDefiniteMatrixException();
-   }
```

```java
src/java/org/apache/commons/math/linear/CholeskyDecompositionImpl.java: 138
+   if (lTData[i][i] < absolutePositivityThreshold)
+       throw new NotPositiveDefiniteMatrixException();
    tI[i] = Math.sqrt(ltI[i]);
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 2 chunks
* The number of fixed locations: 5 locations
```java
src/java/org/apache/commons/math/linear/CholeskyDecompositionImpl.java: 114-116
Location 114 was deleted.
Location 115 was deleted.
Location 116 was deleted.
```

```java
src/java/org/apache/commons/math/linear/CholeskyDecompositionImpl.java: 138
Two locations was inserted in front of Location 138.
```

#### III. Explanation
Its reason is the same as the reason in the 1st patch.
<br><br>