# Time 7
* <h4>Bug type: Type 3 (T3B / T3F)</h4>
* <h4>The number of chunks: 2 chunks (2 used chunks / 2 fixed chunks)</h4>
* <h4>The number of locations: 2 locations (2 used locations / 2 fixed locations)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/main/java/org/joda/time/format/DateTimeFormatter.java: 707-710
    Chronology chrono = instant.getChronology();            
+   int defaultYear = DateTimeUtils.getChronology(chrono).year().get(instantMillis);            
    long instantLocal = instantMillis + chrono.getZone().getOffset(instantMillis);            
    chrono = selectChronology(chrono);            
-   int defaultYear = chrono.year().get(instantLocal);
```
<br>

## 2. Used chunks and locations - T3B
* The number of used chunks: 2 chunks
* The number of used locations: 2 locations
```java
src/main/java/org/joda/time/format/DateTimeFormatter.java: 708
FAULT_OF_OMISSION
```

```java
src/main/java/org/joda/time/format/DateTimeFormatter.java: 710
int defaultYear = chrono.year().get(instantLocal);
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 1
    * T3F (1): 3
<br><br>

## 4. Examples of correct patches
### 4.1. 3rd patch - T3F
#### I. Fixed Result
```java
src/main/java/org/joda/time/format/DateTimeFormatter.java: 708-710            
+   int defaultYear = DateTimeUtils.getChronology(chrono).year().get(instantMillis);            
    long instantLocal = instantMillis + chrono.getZone().getOffset(instantMillis);            
    chrono = selectChronology(chrono);            
-   int defaultYear = chrono.year().get(instantLocal);
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 2 chunks
* The number of fixed locations: 2 locations
```java
src/main/java/org/joda/time/format/DateTimeFormatter.java: 708
A location was inserted in front of Location 708.
```

```java
src/main/java/org/joda/time/format/DateTimeFormatter.java: 710
Location 710 was deleted.
```
<br><br>