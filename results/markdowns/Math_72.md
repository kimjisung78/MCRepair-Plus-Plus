# Math 72
* <h4>Bug type: Type 3 (T3B / T3F)</h4>
* <h4>The number of chunks: 2 chunks (2 used chunks / 2 fixed chunks)</h4>
* <h4>The number of locations: 2 locations (2 used locations / 2 fixed locations)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/main/java/org/apache/commons/math/analysis/solvers/BrentSolver.java: 115
-   setResult(yMin, 0);
+   setResult(min, 0);
```

```java
src/main/java/org/apache/commons/math/analysis/solvers/BrentSolver.java: 127
-   setResult(yMax, 0);
+   setResult(max, 0);
```
<br>

## 2. Used chunks and locations - T3B
* The number of used chunks: 2 chunks
* The number of used locations: 2 locations
```java
src/main/java/org/apache/commons/math/analysis/solvers/BrentSolver.java: 115
setResult(min, 0);
```

```java
src/main/java/org/apache/commons/math/analysis/solvers/BrentSolver.java: 127
setResult(max, 0);
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 1
    * T3F (1): 18
<br><br>

## 4. Examples of correct patches
### 4.1. 18th patch - T3F
#### I. Fixed Result
```java
src/main/java/org/apache/commons/math/analysis/solvers/BrentSolver.java: 115
-   setResult(yMin, 0);
+   setResult(min, 0);
```

```java
src/main/java/org/apache/commons/math/analysis/solvers/BrentSolver.java: 127
-   setResult(yMax, 0);
+   setResult(max, 0);
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 2 chunks
* The number of fixed locations: 2 locations
```java
src/main/java/org/apache/commons/math/analysis/solvers/BrentSolver.java: 115
setResult(min, 0);
```

```java
src/main/java/org/apache/commons/math/analysis/solvers/BrentSolver.java: 127
setResult(max, 0);
```
<br><br>