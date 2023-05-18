# Chart 24
* <h4>Bug type: Type 1 (T1B / T1F)</h4>
* <h4>The number of chunks: 1 chunk (1 used chunk / 1 fixed chunk)</h4>
* <h4>The number of locations: 1 location (1 used location / 1 fixed location)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
source/org/jfree/chart/renderer/GrayPaintScale.java: 126-127
-   int g = (int) ((value - this.lowerBound) / (this.upperBound
+   int g = (int) ((v - this.lowerBound) / (this.upperBound 
        - this.lowerBound) * 255.0);
```
<br>

## 2. Used chunks and locations - T1B
* The number of used chunks: 1 chunk
* The number of used locations: 1 location
```java
source/org/jfree/chart/renderer/GrayPaintScale.java: 126-127
(Locations 126-127 are divided.)
int g = (int) ((value - this.lowerBound) / (this.upperBound - this.lowerBound) * 255.0);
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 1
    * T1F (1): 97
<br><br>

## 4. Examples of correct patches
### 4.1. 97th patch - T1F
#### I. Fixed Result
```java
source/org/jfree/chart/renderer/GrayPaintScale.java: 126-127
(Locations 126-127 are divided.)
-   int g = (int) ((value - this.lowerBound) / (this.upperBound - this.lowerBound) * 255.0);
+   int g = (int) ((v - this.lowerBound) / (this.upperBound - this.lowerBound) * 255.0);
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
source/org/jfree/chart/renderer/GrayPaintScale.java: 126-127
(Locations 126-127 are divided.)
int g = (int) ((v - this.lowerBound) / (this.upperBound - this.lowerBound) * 255.0);
```
<br><br>


