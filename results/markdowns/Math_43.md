# Math 43
* <h4>Bug type: Type 3 (T3B / T3F)</h4>
* <h4>The number of chunks: 3 chunks (3 used chunks / 3 fixed chunks)</h4>
* <h4>The number of locations: 3 locations (3 used locations / 3 fixed locations)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/main/java/org/apache/commons/math/stat/descriptive/SummaryStatistics.java: 158-166
-   if (!(meanImpl instanceof Mean)) {
+   if (meanImpl != mean) {
        meanImpl.increment(value);
    }
-   if (!(varianceImpl instanceof Variance)) {
+   if (varianceImpl != variance) {
        varianceImpl.increment(value);
    }
-   if (!(geoMeanImpl instanceof GeometricMean)) {
+   if (geoMeanImpl != geoMean) {
        geoMeanImpl.increment(value);
    }
```
<br>

## 2. Used chunks and locations - T1B
* The number of used chunks: 3 chunks
* The number of used locations: 3 locations
```java
src/main/java/org/apache/commons/math/stat/descriptive/SummaryStatistics.java: 158
if (!(meanImpl instanceof Mean)) {
```

```java
src/main/java/org/apache/commons/math/stat/descriptive/SummaryStatistics.java: 161
if (!(varianceImpl instanceof Variance)) {
```

```java
src/main/java/org/apache/commons/math/stat/descriptive/SummaryStatistics.java: 164
if (!(geoMeanImpl instanceof GeometricMean)) {
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 1
    * T3F (1): 414
<br><br>

## 4. Examples of correct patches
### 4.1. 414th patch - T3F
#### I. Fixed Result
```java
src/main/java/org/apache/commons/math/stat/descriptive/SummaryStatistics.java: 158-166
-   if (!(meanImpl instanceof Mean)) {
+   if (meanImpl != mean) {
        meanImpl.increment(value);
    }
-   if (!(varianceImpl instanceof Variance)) {
+   if (varianceImpl != variance) {
        varianceImpl.increment(value);
    }
-   if (!(geoMeanImpl instanceof GeometricMean)) {
+   if (geoMeanImpl != geoMean) {
        geoMeanImpl.increment(value);
    }
```

#### II. Fixed chunks and locations 
* The number of fixed chunks: 3 chunks
* The number of fixed locations: 3 locations
```java
src/main/java/org/apache/commons/math/stat/descriptive/SummaryStatistics.java: 158
if (meanImpl != mean) {
```

```java
src/main/java/org/apache/commons/math/stat/descriptive/SummaryStatistics.java: 161
if (varianceImpl != variance) {
```

```java
src/main/java/org/apache/commons/math/stat/descriptive/SummaryStatistics.java: 164
if (geoMeanImpl != geoMean) {
```
<br><br>