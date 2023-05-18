# Math 32
* <h4>Bug type: Type 1 (T1B / T1F)</h4>
* <h4>The number of chunks: 1 chunk (1 used chunk / 1 fixed chunk)</h4>
* <h4>The number of locations: 1 location (1 used location / 1 fixed location)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/main/java/org/apache/commons/math3/geometry/euclidean/twod/PolygonsSet.java: 135-136
    final BSPTree<Euclidean2D> tree = getTree(false);
-   if ((Boolean) tree.getAttribute()) {
+   if (tree.getCut() == null && (Boolean) tree.getAttribute()) {
```
<br>

## 2. Used chunks and locations - T1B
* The number of used chunks: 1 chunk
* The number of used locations: 1 location
```java
src/main/java/org/apache/commons/math3/geometry/euclidean/twod/PolygonsSet.java: 136
if ((Boolean) tree.getAttribute()) {
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 2
    * T1F (2): 336, 467
<br><br>

## 4. Examples of correct patches
### 4.1. 336th patch - T1F
#### I. Fixed Result
```java
src/main/java/org/apache/commons/math3/geometry/euclidean/twod/PolygonsSet.java: 136
-   if ((Boolean) tree.getAttribute()) {
+   if (tree.getAttribute() instanceof Boolean) {
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/main/java/org/apache/commons/math3/geometry/euclidean/twod/PolygonsSet.java: 136
if (tree.getAttribute() instanceof Boolean) {
```

#### III. Explanation
To fix the bug, its source code must be changed that it checks that ```tree.getAttribute()``` can convert to ```Boolean``` class.
<br>

### 4.2. 467th patch - T1F
#### I. Fixed Result
```java
src/main/java/org/apache/commons/math3/geometry/euclidean/twod/PolygonsSet.java: 136
-   if ((Boolean) tree.getAttribute()) {
+   if (tree != null && tree.getAttribute() instanceof Boolean) {
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/main/java/org/apache/commons/math3/geometry/euclidean/twod/PolygonsSet.java: 136
if (tree != null && tree.getAttribute() instanceof Boolean) {
```

#### III. Explanation
Its reason is the same as the reason in the 336th patch.
<br><br>