# Mockito 22
* <h4>Bug type: Type 3 (T1B / T3F)</h4>
* <h4>The number of chunks: 2 chunks (1 used chunk / 2 fixed chunks)</h4>
* <h4>The number of locations: 5 locations (1 used location / 5 fixed locations)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/org/mockito/internal/matchers/Equality.java: 12-20
    public static boolean areEqual(Object o1, Object o2) {
+       if (o1 == o2) {            
+           return true;
-       if (o1 == null || o2 == null) {
+       } else if (o1 == null || o2 == null) {
            return o1 == null && o2 == null;
        } else if (isArray(o1)) {
            return isArray(o2) && areArraysEqual(o1, o2);
        } else {
            return o1.equals(o2);
        }
    }
```
<br>

## 2. Used chunks and locations - T1B
* The number of used chunks: 1 chunk
* The number of used locations: 1 location
```java
src/org/mockito/internal/matchers/Equality.java: 13
if (o1 == null || o2 == null) {
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 2
    * T3F (2): 823, 826
<br><br>

## 4. Examples of correct patches
### 4.1. 823rd patch - T3F
#### I. Fixed Result
```java
    public static boolean areEqual(Object o1, Object o2) {
+       try{
-       if (o1 == null || o2 == null) {
+       if (o1 == null) {
            return o1 == null && o2 == null;
        } else if (isArray(o1)) {
            return isArray(o2) && areArraysEqual(o1, o2);
        } else {
            return o1.equals(o2);
        }
+       } catch (Exception ex) {
+           return true;
+       } 
    }
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 2 chunks
* The number of fixed locations: 5 locations
```java
src/org/mockito/internal/matchers/Equality.java: 13
A location was inserted in front of Location 13.
if (o1 == null) {
```

```java
src/org/mockito/internal/matchers/Equality.java: 20
Three locations were inserted in front of Location 20.
```

#### III. Explanation
To fix the bug, its source code must changed that it returns ```true``` for comprison between bad equals. The patch returned ```true``` for the comparison using its try-catch statement.
<br><br>