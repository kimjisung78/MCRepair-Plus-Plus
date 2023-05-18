# Lang 20
* <h4>Bug type: Type 3 (T3B / T3F)</h4>
* <h4>The number of chunks: 2 chunks (2 used chunks / 2 fixed chunks)</h4>
* <h4>The number of locations: 2 locations (2 used locations / 2 fixed locations)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/main/java/org/apache/commons/lang3/StringUtils.java: 3298
-   StringBuilder buf = new StringBuilder((array[startIndex] == null ? 16 : array[startIndex].toString().length()) + 1);
+   StringBuilder buf = new StringBuilder(noOfItems * 16);
```

```java
src/main/java/org/apache/commons/lang3/StringUtils.java: 3383
-   StringBuilder buf = new StringBuilder((array[startIndex] == null ? 16 : array[startIndex].toString().length()) + separator.length());
+   StringBuilder buf = new StringBuilder(noOfItems * 16);
```
<br>

## 2. Used chunks and locations - T3B
* The number of used chunks: 2 chunks
* The number of used locations: 2 locations
```java
src/main/java/org/apache/commons/lang3/StringUtils.java: 3298
StringBuilder buf = new StringBuilder((array[startIndex] == null ? 16 : array[startIndex].toString().length()) + 1);
```

```java
src/main/java/org/apache/commons/lang3/StringUtils.java: 3383
StringBuilder buf = new StringBuilder((array[startIndex] == null ? 16 : array[startIndex].toString().length()) + separator.length());
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 1
    * T3F (1): 11,616
<br><br>

## 4. Examples of correct patches
### 4.1. 33rd patch - T2F
#### I. Fixed Result
```java
src/main/java/org/apache/commons/lang3/StringUtils.java: 3298
-   StringBuilder buf = new StringBuilder((array[startIndex] == null ? 16 : array[startIndex].toString().length()) + 1);
+   StringBuilder buf = new StringBuilder(array[startIndex] == null ? 16 : array[startIndex].toString().length());
```

```java
src/main/java/org/apache/commons/lang3/StringUtils.java: 3383
-   StringBuilder buf = new StringBuilder((array[startIndex] == null ? 16 : array[startIndex].toString().length()) + separator.length());
+   StringBuilder buf = new StringBuilder(array[startIndex] == null ? 16 : array[startIndex].toString().length());
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 2 chunks
* The number of fixed locations: 2 locations
```java
src/main/java/org/apache/commons/lang3/StringUtils.java: 3298
StringBuilder buf = new StringBuilder(array[startIndex] == null ? 16 : array[startIndex].toString().length());
```

```java
src/main/java/org/apache/commons/lang3/StringUtils.java: 3383
StringBuilder buf = new StringBuilder(array[startIndex] == null ? 16 : array[startIndex].toString().length());
```

#### III. Explanation
To fix the bug, its source code must be changed that it avoids ```NullPointerException``` exceptions. The patch avoided the exceptions.
<br><br>