# Math 56
* <h4>Bug type: Type 2 (T2B / T2F)</h4>
* <h4>The number of chunks: 1 chunk (1 used chunk / 1 fixed chunk)</h4>
* <h4>The number of locations: 7 locations (7 used locations / 6 fixed locations)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/main/java/org/apache/commons/math/util/MultidimensionalCounter.java: 237-243
-   int idx = 1;
-   while (count < index) {
-       count += idx;
-       ++idx;
-   }
-   --idx;
-   indices[last] = idx;
+   indices[last] = index - count;
```                  
<br>

## 2. Used chunks and locations - T3B
* The number of used chunks: 1 chunk
* The number of used locations: 7 locations
```java
src/main/java/org/apache/commons/math/util/MultidimensionalCounter.java: 237-243
int idx = 1;
while (count < index) {
    count += idx;
    ++idx;
}
--idx;
indices[last] = idx;
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 1
    * T2F (1): 508
<br><br>

## 4. Examples of correct patches
### 4.1. 508th patch - T2F
#### I. Fixed Result
```java
src/main/java/org/apache/commons/math/util/MultidimensionalCounter.java: 237-243
-   int idx = 1;
+   int idx = index - count;
-   while (count < index) {
-       count += idx;
-       ++idx;
-   }
-   --idx;
    indices[last] = idx;
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 6 locations
```java
src/main/java/org/apache/commons/math/util/MultidimensionalCounter.java: 237-242
int idx = index - count;
```
<br><br>