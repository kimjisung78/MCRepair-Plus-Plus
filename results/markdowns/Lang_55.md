# Lang 55
* <h4>Bug type: Type 3 (T2B / T3F)</h4>
* <h4>The number of chunks: 2 chunks (1 used chunk / 2 fixed chunks)</h4>
* <h4>The number of locations: 2 locations (2 used locations / 2 fixed locations)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/java/org/apache/commons/lang/time/StopWatch.java: 118-119
+   if(this.runningState == STATE_RUNNING) {
        stopTime = System.currentTimeMillis();
+   }
    this.runningState = STATE_STOPPED;
```
<br>

## 2. Used chunks and locations - T2B
* The number of used chunks: 2 chunks
* The number of used locations: 2 locations
```java
src/java/org/apache/commons/lang/time/StopWatch.java: 118
FAULT_OF_OMISSION
```

```java
src/java/org/apache/commons/lang/time/StopWatch.java: 119
FAULT_OF_OMISSION
```
<br><br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 1
    * T3F (1): 276
<br><br>

## 4. Examples of correct patches
### 4.1. 276th patch - T3F
#### I. Fixed Result
```java
src/java/org/apache/commons/lang/time/StopWatch.java: 118-119
+   if (this.runningState!=STATE_SUSPENDED) {
        stopTime = System.currentTimeMillis();
+   }
    this.runningState = STATE_STOPPED;
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 2 chunks
* The number of fixed locations: 2 locations
```java
src/java/org/apache/commons/lang/time/StopWatch.java: 118
A location was inserted in front of Location 118.
```

```java
src/java/org/apache/commons/lang/time/StopWatch.java: 119
A location was inserted in front of Location 119.
```

#### III. Explanation
Because ```runningState``` only can be STATE_RUNNING or STATE_SUSPENDED, ```runningState == STATE_RUNNING``` indicates ```runningState != STATE_STATE_SUSPENDED```.
<br><br>