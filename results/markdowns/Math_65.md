# Math 65
* <h4>Bug type: Type 1 (T1B / T1F)</h4>
* <h4>The number of chunks: 1 chunk (1 used chunk / 1 fixed chunk)</h4>
* <h4>The number of locations: 1 location (1 used location / 1 fixed location)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/main/java/org/apache/commons/math/optimization/general/AbstractLeastSquaresOptimizer.java: 239-246
    public double getRMS() {
-       double criterion = 0;
-       for (int i = 0; i < rows; ++i) {
-           final double residual = residuals[i];
-           criterion += residual * residual * residualsWeights[i];
-       }
-       return Math.sqrt(criterion / rows);
+       return Math.sqrt(getChiSquare() / rows);
    }
```

```java
src/main/java/org/apache/commons/math/optimization/general/AbstractLeastSquaresOptimizer.java: 254-261
    public double getChiSquare() {
        double chiSquare = 0;
        for (int i = 0; i < rows; ++i) {
            final double residual = residuals[i];
-           chiSquare += residual * residual / residualsWeights[i];
+           chiSquare += residual * residual * residualsWeights[i];
        }
        return chiSquare;
    }
``` 
<br>

## 2. Used chunks and locations - T1B
* The number of used chunks: 1 chunk
* The number of used locations: 1 location
```java
src/main/java/org/apache/commons/math/optimization/general/AbstractLeastSquaresOptimizer.java: 258
chiSquare += residual * residual / residualsWeights[i];
```
* Locations 240-245 are overlapped according to ["Is the Ground Truth Really Accurate? Dataset Purification for Automated Program Repair"](https://ieeexplore.ieee.org/document/9426017) research paper.
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 1
    * T1F (5): 11
<br><br>

## 4. Examples of correct patches
### 4.1. 11st patch - T1F
#### I. Fixed Result
```java
src/main/java/org/apache/commons/math/optimization/general/AbstractLeastSquaresOptimizer.java: 258
-   chiSquare += residual * residual / residualsWeights[i];
+   chiSquare += residual * residual * residualsWeights[i];
```  

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/main/java/org/apache/commons/math/optimization/general/AbstractLeastSquaresOptimizer.java: 258
chiSquare += residual * residual * residualsWeights[i];
``` 
<br><br>