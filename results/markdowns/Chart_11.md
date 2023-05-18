# Chart 11
* <h4>Bug type: Type 1 (T1B / T1F)</h4>
* <h4>The number of chunks: 1 chunk (1 used chunk / 1 fixed chunk)</h4>
* <h4>The number of locations: 1 location (1 used location / 1 fixed location)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
source/org/jfree/chart/util/ShapeUtilities.java: 274-277
    PathIterator iterator1 = p1.getPathIterator(null);
-   PathIterator iterator2 = p1.getPathIterator(null);
+   PathIterator iterator2 = p2.getPathIterator(null);
    double[] d1 = new double[6];
    double[] d2 = new double[6];
```
<br>

## 2. Used chunks and locations - T1B
* The number of used chunks: 1 chunk
* The number of used locations: 1 location
```java
source/org/jfree/chart/util/ShapeUtilities.java: 275
PathIterator iterator2 = p1.getPathIterator(null);
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 4
    * T1F (4): 342, 389, 693, 700
<br><br>

## 4. Examples of correct patches
### 4.1. 342nd patch - T1F
#### I. Fixed Result
```java
source/org/jfree/chart/util/ShapeUtilities.java: 275
-   PathIterator iterator2 = p1.getPathIterator(null);            
+   PathIterator iterator2 = p2.getPathIterator(null); 
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
source/org/jfree/chart/util/ShapeUtilities.java: 275
PathIterator iterator2 = p2.getPathIterator(null);
```
<br>

### 4.2. 389th patch - T1F
#### I. Evaluated Result
```java
source/org/jfree/chart/util/ShapeUtilities.java: 274
-   PathIterator iterator1 = p1.getPathIterator(null);            
+   PathIterator iterator1 = p2.getPathIterator(null); 
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
source/org/jfree/chart/util/ShapeUtilities.java: 274
PathIterator iterator1 = p2.getPathIterator(null);
```

#### III. Explanation
To fix the bug, its source code should be changed that it compares ```p1``` and ```p2``` iterators. 
<br><br>

### 4.3. 693rd patch - T1F 
#### I. Evaluated Result
```java
source/org/jfree/chart/util/ShapeUtilities.java: 274
-   PathIterator iterator1 = p1.getPathIterator(null);            
+   final PathIterator iterator1 = p2.getPathIterator(null); 
```

#### III. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
source/org/jfree/chart/util/ShapeUtilities.java: 274
final PathIterator iterator2 = p2.getPathIterator(null);
```
<br><br>


