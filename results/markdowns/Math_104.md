# Math 104
* <h4>Bug type: Type 1 (T1B / T1F)</h4>
* <h4>The number of chunks: 1 chunk (1 used chunk / 1 fixed chunk)</h4>
* <h4>The number of locations: 1 location (1 used location / 1 fixed location)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/java/org/apache/commons/math/special/Gamma.java: 37
-   private static final double DEFAULT_EPSILON = 10e-9;
+   private static final double DEFAULT_EPSILON = 10e-15;
```
<br>

## 2. Used chunks and locations - T1B
* The number of used chunks: 1 chunk
* The number of used locations: 1 location
```java
src/java/org/apache/commons/math/special/Gamma.java: 37
private static final double DEFAULT_EPSILON = 10e-9;
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 39
    * T1F (39): 17, 46, 122, 192, 215, 226, 240, 250, 273, 275, 276, 286, 287, 305, 323, 333, 346, 368, 374, 385, 412, 421, 460, 514, 515, 524, 536, 548, 558, 565, 583, 591, 604, 612, 624, 625, 650, 659, 660
<br><br>

## 4. Examples of correct patches
### 4.1. 515th patch - T1F
#### I. Fixed Result
```java
src/java/org/apache/commons/math/special/Gamma.java: 37
-   private static final double DEFAULT_EPSILON = 10e-9;
+   private static final double DEFAULT_EPSILON = 10e-15;
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/java/org/apache/commons/math/special/Gamma.java: 37
private static final double DEFAULT_EPSILON = 10e-15;
```  
<br>

### 4.2. 583rd patch - T1F
#### I. Fixed Result
```java
src/java/org/apache/commons/math/special/Gamma.java: 37
-   private static final double DEFAULT_EPSILON = 10e-9;
+   private static final double DEFAULT_EPSILON = 10e-14;
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/java/org/apache/commons/math/special/Gamma.java: 37
private static final double DEFAULT_EPSILON = 10e-14;
```

#### III. Explanation
To fix the bug, ```DEFAULT_EPSILON``` field is greater than ```10e-9```.
<br><br>