# Math 82
* <h4>Bug type: Type 3 (T1B / T1F, T3F)</h4>
* <h4>The number of chunks: 2 chunks (1 used chunk / 1, 2 fixed chunks)</h4>
* <h4>The number of locations: 2 locations (1 used location / 1, 2 fixed locations)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/main/java/org/apache/commons/math/optimization/linear/SimplexSolver.java: 76-82
    private Integer getPivotRow(final int col, final SimplexTableau tableau) {
        double minRatio = Double.MAX_VALUE;
        Integer minRatioPos = null;
        for (int i = tableau.getNumObjectiveFunctions(); i < tableau.getHeight(); i++) {
            final double rhs = tableau.getEntry(i, tableau.getWidth() - 1);
            final double entry = tableau.getEntry(i, col);
-           if (MathUtils.compareTo(entry, 0, epsilon) >= 0) {
+           if (MathUtils.compareTo(entry, 0, epsilon) > 0) {
```
<br>

## 2. Used chunks and locations - T1B
* The number of used chunks: 1 chunk
* The number of used locations: 1 location
```java
src/main/java/org/apache/commons/math/optimization/linear/SimplexSolver.java: 82
if (MathUtils.compareTo(entry, 0, epsilon) >= 0) {
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 3
    * T1F (2): 211, 783
    * T3F (1): 797
<br><br>

## 4. Examples of correct patches
### 4.1. 783rd patch - T1F
#### I. Fixed Result
```java
src/main/java/org/apache/commons/math/optimization/linear/SimplexSolver.java: 82
-   if (MathUtils.compareTo(entry, 0, epsilon) >= 0) {
+   if (MathUtils.compareTo(entry, 0, epsilon) > 0) {
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/main/java/org/apache/commons/math/optimization/linear/SimplexSolver.java: 82
if (MathUtils.compareTo(entry, 0, epsilon) > 0) {
```  
<br>

### 4.2. 797th patch - T3F
#### I. Fixed Result
```java
src/main/java/org/apache/commons/math/optimization/linear/SimplexSolver.java: 76
-   private Integer getPivotRow(final int col, final SimplexTableau tableau) {
+   private Integer getPivotRow(int col, final SimplexTableau tableau) {
```

```java
src/main/java/org/apache/commons/math/optimization/linear/SimplexSolver.java: 82
-   if (MathUtils.compareTo(entry, 0, epsilon) >= 0) {
+   if (MathUtils.compareTo(entry, 0, epsilon) > 0) {
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 2 chunks
* The number of fixed locations: 2 locations
```java
src/main/java/org/apache/commons/math/optimization/linear/SimplexSolver.java: 76
private Integer getPivotRow(int col, final SimplexTableau tableau) {
```

```java
src/main/java/org/apache/commons/math/optimization/linear/SimplexSolver.java: 82
if (MathUtils.compareTo(entry, 0, epsilon) > 0) {
```  
<br><br>