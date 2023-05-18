# Closure 57
* <h4>Bug type: Type 1 (T1B / T1F)</h4>
* <h4>The number of chunks: 1 chunk (1 used chunk / 1 fixed chunk)</h4>
* <h4>The number of locations: 1 location (1 used location / 1 fixed location)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/com/google/javascript/jscomp/ClosureCodingConvention.java: 195-200
    if (functionName.equals(qualifiedName)) {
        Node target = callee.getNext();
-       if (target != null) {
+       if (target != null && target.getType() == Token.STRING) {
            className = target.getString();
        }
    }
```
<br>

## 2. Used chunks and locations - T1B
* The number of used chunks: 1 chunk
* The number of used locations: 1 location
```java
src/com/google/javascript/jscomp/ClosureCodingConvention.java: 197
if (target != null) {
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 1
    * T1F (1): 775
<br><br>

## 4. Examples of correct patches
### 4.1. 775th patch - T1F
#### I. Fixed Result
```java
src/com/google/javascript/jscomp/ClosureCodingConvention.java: 196-199           
    Node target = callee.getNext();
-   if (target != null) {
+   if (target != null && target.getType() == Token.STRING) {
        className = target.getString();
    }
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/com/google/javascript/jscomp/ClosureCodingConvention.java: 197
if (target != null && target.getType() == Token.STRING) {
```
<br><br>