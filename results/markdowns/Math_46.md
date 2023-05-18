# Math 46
* <h4>Bug type: Type 3 (T3B / T3F)</h4>
* <h4>The number of chunks: 2 chunks (2 used chunks / 2 fixed chunks)</h4>
* <h4>The number of locations: 2 locations (2 used locations / 2 fixed locations)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/main/java/org/apache/commons/math/complex/Complex.java: 258-261
    if (divisor.isZero) {
        // return isZero ? NaN : INF; // See MATH-657
-       return isZero ? NaN : INF;
+       return NaN;
    }
```

```java
src/main/java/org/apache/commons/math/complex/Complex.java: 295-298
    if (divisor == 0d) {
        // return isZero ? NaN : INF; // See MATH-657
-       return isZero ? NaN : INF;
+       return NaN;
    }
```                  
<br>

## 2. Used chunks and locations - T3B
* The number of used chunks: 2 chunks
* The number of used locations: 2 locations
```java
src/main/java/org/apache/commons/math/complex/Complex.java: 260
return isZero ? NaN : INF;
```

```java
src/main/java/org/apache/commons/math/complex/Complex.java: 297
return isZero ? NaN : INF;
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 1
    * T3F (1): 17,941
<br><br>

## 4. Examples of correct patches
### 4.1. 17,941st patch - T3F
#### I. Fixed Result
```java
src/main/java/org/apache/commons/math/complex/Complex.java: 260
-   return isZero ? NaN : INF;
+   return isZero ? NaN : NaN;
```

```java
src/main/java/org/apache/commons/math/complex/Complex.java: 297
-   return isZero ? NaN : INF;
+   return true ? NaN : INF;
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 2 chunks
* The number of fixed locations: 2 locations
```java
src/main/java/org/apache/commons/math/complex/Complex.java: 260
return isZero ? NaN : NaN;
```

```java
src/main/java/org/apache/commons/math/complex/Complex.java: 297
return true ? NaN : INF;
```
<br><br>