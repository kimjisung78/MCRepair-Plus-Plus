# Math 62
* <h4>Bug type: Type 3 (T3B / T2F, T3F)</h4>
* <h4>The number of chunks: 2 chunks (2 used chunks / 1, 2 fixed chunks)</h4>
* <h4>The number of locations: 4 locations (4 used locations / 3, 4 fixed locations)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/main/java/org/apache/commons/math/optimization/univariate/MultiStartUnivariateRealOptimizer.java: 146
-   return optimize(f, goal, min, max, 0);
+   return optimize(f, goal, min, max, min + 0.5 * (max - min));
```

```java
src/main/java/org/apache/commons/math/optimization/univariate/MultiStartUnivariateRealOptimizer.java: 160-162
-   final double bound1 = (i == 0) ? min : min + generator.nextDouble() * (max - min);
-   final double bound2 = (i == 0) ? max : min + generator.nextDouble() * (max - min);
+   final double s = (i == 0) ? startValue : min + generator.nextDouble() * (max - min);
-   optima[i] = optimizer.optimize(f, goal, FastMath.min(bound1, bound2), FastMath.max(bound1, bound2));
+   optima[i] = optimizer.optimize(f, goal, min, max, s);
```
<br>

## 2. Used chunks and locations - T3B
* The number of used chunks: 2 chunks
* The number of used locations: 4 locations
```java
src/main/java/org/apache/commons/math/optimization/univariate/MultiStartUnivariateRealOptimizer.java: 146
return optimize(f, goal, min, max, 0);
```

```java
src/main/java/org/apache/commons/math/optimization/univariate/MultiStartUnivariateRealOptimizer.java: 160-162
final double bound1 = (i == 0) ? min : min + generator.nextDouble() * (max - min);
final double bound2 = (i == 0) ? max : min + generator.nextDouble() * (max - min);
optima[i] = optimizer.optimize(f, goal, FastMath.min(bound1, bound2), FastMath.max(bound1, bound2));
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 2
    * T2F (1): 10,761
    * T3F (1): 5,103
<br><br>

## 4. Examples of correct patches
### 4.1. 5,103rd patch - T3F
#### I. Fixed Result
```java
src/main/java/org/apache/commons/math/optimization/univariate/MultiStartUnivariateRealOptimizer.java: 146
-   return optimize(f, goal, min, max, 0);
+   return optimize(f, goal, min, max, 0L);
```

```java
src/main/java/org/apache/commons/math/optimization/univariate/MultiStartUnivariateRealOptimizer.java: 160-162
-   final double bound1 = (i == 0) ? min : min + generator.nextDouble() * (max - min);
-   final double bound2 = (i == 0) ? max : min + generator.nextDouble() * (max - min);
-   optima[i] = optimizer.optimize(f, goal, FastMath.min(bound1, bound2), FastMath.max(bound1, bound2));
+   optima[i] = optimizer.optimize(f, goal, FastMath.min(min, max), FastMath.max(min + generator.nextDouble(), max));
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 2 chunks
* The number of fixed locations: 4 locations
```java
src/main/java/org/apache/commons/math/optimization/univariate/MultiStartUnivariateRealOptimizer.java: 146
return optimize(f, goal, min, max, 0L);
```

```java
src/main/java/org/apache/commons/math/optimization/univariate/MultiStartUnivariateRealOptimizer.java: 160-162
optima[i] = optimizer.optimize(f, goal, FastMath.min(min, max), FastMath.max(min + generator.nextDouble(), max));
```

### III. Explanation
To fix the bug, its source code must be changed that it increases its small boundaries. The patch increased its small boundaries and then did not exceed the boundaries.
<br>

### 4.2. 10,761st patch - T2F
#### I. Fixed Result
```java
src/main/java/org/apache/commons/math/optimization/univariate/MultiStartUnivariateRealOptimizer.java: 160-162
-   final double bound1 = (i == 0) ? min : min + generator.nextDouble() * (max - min);
-   final double bound2 = (i == 0) ? max : min + generator.nextDouble() * (max - min);
-   optima[i] = optimizer.optimize(f, goal, FastMath.min(bound1, bound2), FastMath.max(bound1, bound2));
+   optima[i] = optimizer.optimize(f, goal, FastMath.min(min, max), FastMath.max(min + generator.nextDouble(), max));
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/main/java/org/apache/commons/math/optimization/univariate/MultiStartUnivariateRealOptimizer.java: 160-162
optima[i] = optimizer.optimize(f, goal, FastMath.min(min, max), FastMath.max(min + generator.nextDouble(), max));
```

### III. Explanation
Its reason is the same as the reason in the 5,103rd patch.
<br><br>