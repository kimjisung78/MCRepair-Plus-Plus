# Math 77
* <h4>Bug type: Type 3 (T3B / T3F)</h4>
* <h4>The number of chunks: 2 chunks (2 used chunks / 2 fixed chunks)</h4>
* <h4>The number of locations: 10 locations (10 used locations / 2 fixed locations)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/main/java/org/apache/commons/math/linear/ArrayRealVector.java: 721
-   max += Math.max(max, Math.abs(a));
+   max = Math.max(max, Math.abs(a));
```

```java
src/main/java/org/apache/commons/math/linear/OpenMapRealVector.java: 498-506
-   public double getLInfNorm() {
-       double max = 0;
-       Iterator iter = entries.iterator();
-       while (iter.hasNext()) {
-           iter.advance();
-           max += iter.value();
-       }
-       return max;
-   }
```
<br>

## 2. Used chunks and locations - T3B
* The number of used chunks: 2 chunks
* The number of used locations: 10 locations
```java
src/main/java/org/apache/commons/math/linear/ArrayRealVector.java: 721
max += Math.max(max, Math.abs(a));
```

```java
src/main/java/org/apache/commons/math/linear/OpenMapRealVector.java: 498-506
public double getLInfNorm() {
    double max = 0;
    Iterator iter = entries.iterator();
    while (iter.hasNext()) {
        iter.advance();
        max += iter.value();
    }
    return max;
}
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 7
    * T3F (7): 263, 2,129, 3,106, 4,486, 5,602, 9,852, 10,258
<br><br>

## 4. Examples of correct patches
### 4.1. 263rd patch - T3F
#### I. Fixed Result
```java
src/main/java/org/apache/commons/math/linear/ArrayRealVector.java: 721
-   max += Math.max(max, Math.abs(a));
+   max = Math.max(max, Math.abs(a));
```

```java
src/main/java/org/apache/commons/math/linear/OpenMapRealVector.java: 498
-   public double getLInfNorm() {
+   public double getLConfNorm() {
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 2 chunks
* The number of fixed locations: 2 locations
```java
src/main/java/org/apache/commons/math/linear/ArrayRealVector.java: 721
max = Math.max(max, Math.abs(a));
```

```java
src/main/java/org/apache/commons/math/linear/OpenMapRealVector.java: 498
public double getLConfNorm() {
```

### III. Explanation
Because ```getLInfNorm``` method is not called in ```ArrayRealVector.java```, the method is equivalent to its deletion.
<br><br>