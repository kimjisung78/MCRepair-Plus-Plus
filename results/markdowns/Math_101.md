# Math 101
* <h4>Bug type: Type 1 (T1B / T1F)</h4>
* <h4>The number of chunks: 1 chunk (1 used chunk / 1 fixed chunk)</h4>
* <h4>The number of locations: 1 location (1 used location / 1 fixed location)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/java/org/apache/commons/math/complex/ComplexFormat.java: 376-379
    int endIndex = startIndex + n;
-   if (
+   if ((startIndex >= source.length()) ||
+       (endIndex > source.length()) ||
        source.substring(startIndex, endIndex).compareTo(
        getImaginaryCharacter()) != 0) {
```
<br>

## 2. Used chunks and locations - T1B
* The number of used chunks: 1 chunk
* The number of used locations: 1 location
```java
src/java/org/apache/commons/math/complex/ComplexFormat.java: 377-379
(Locations 377-379 are divided.)
if (source.substring(startIndex, endIndex).compareTo(getImaginaryCharacter()) != 0) {
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 1
    * T1F (1): 167
<br><br>

## 4. Examples of correct patches
### 4.1. 167th patch - T1F
#### I. Fixed Result
```java
src/java/org/apache/commons/math/complex/ComplexFormat.java: 377-379
(Locations 377-379 are divided.)
-   if (source.substring(startIndex, endIndex).compareTo(getImaginaryCharacter()) != 0) {
+   if (source.substring(startIndex).compareTo(getImaginaryCharacter()) != 0) {
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/java/org/apache/commons/math/complex/ComplexFormat.java: 377-379
(Locations 377-379 are divided.)
if (source.substring(startIndex).compareTo(getImaginaryCharacter()) != 0) {
```  

#### III. Explanation
To fix the bug, its source code must be changed that it prevents ```OutOfBoundsException``` exceptions due to ```endIndex``` variable. Hence, ```endIndex``` variable is not essential. The patch prevented the exceptions.
<br><br>