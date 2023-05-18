# Chart 8
* <h4>Bug type: Type 1 (T1B / T1F)</h4>
* <h4>The number of chunks: 1 chunk (1 used chunk / 1 fixed chunk)</h4>
* <h4>The number of locations: 1 location (1 used location / 1 fixed location)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
source/org/jfree/data/time/Week.java: 173-176
    public Week(Date time, TimeZone zone) {
        // defer argument checking...
-       this(time, RegularTimePeriod.DEFAULT_TIME_ZONE, Locale.getDefault());
+       this(time, zone, Locale.getDefault());
    }
```
<br>

## 2. Used chunks and locations - T1B
* The number of used chunks: 1 chunk
* The number of used locations: 1 location
```java
source/org/jfree/data/time/Week.java: 175
this(time, RegularTimePeriod.DEFAULT_TIME_ZONE, Locale.getDefault());
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 1
    * T1F (1): 486
<br><br>

## 4. Examples of correct patches
### 4.1. 486th patch - T1F
#### I. Fixed Result
```java
source/org/jfree/data/time/Week.java: 175
-   this(time, RegularTimePeriod.DEFAULT_TIME_ZONE, Locale.getDefault());
+   this(time, zone, Locale.getDefault());
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
source/org/jfree/data/time/Week.java: 175
this(time, zone, Locale.getDefault());
```
<br><br>