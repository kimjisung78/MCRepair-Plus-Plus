# Closure 122
* <h4>Bug type: Type 1 (T1B / T1F)</h4>
* <h4>The number of chunks: 1 chunk (1 used chunk / 1 fixed chunk)</h4>
* <h4>The number of locations: 1 location (1 used location / 1 fixed location)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/com/google/javascript/jscomp/parsing/IRFactory.java: 249-252
    * Check to see if the given block comment looks like it should be JSDoc.
    */
    private void handleBlockComment(Comment comment) {
+   Pattern p = Pattern.compile("(/|(\n[ \t]*))\\*[ \t]*@[a-zA-Z]");
-   if (comment.getValue().indexOf("/* @") != -1 || comment.getValue().indexOf("\n * @") != -1) {
+   if (p.matcher(comment.getValue()).find()) {
```
<br>

## 2. Used chunks and locations - T1B
* The number of used chunks: 1 chunk
* The number of used locations: 1 location
```java
src/com/google/javascript/jscomp/parsing/IRFactory.java: 252
if (comment.getValue().indexOf("/* @") != -1 || comment.getValue().indexOf("\n * @") != -1) {
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 1
    * T1F (1): 204
<br><br>

## 4. Examples of correct patches
### 4.1. 204th patch - T1F
#### I. Fixed Result
```java
src/com/google/javascript/jscomp/parsing/IRFactory.java: 252
-   if (comment.getValue().indexOf("/* @") != -1 || comment.getValue().indexOf("\n * @") != -1) {
+   if (comment.getValue().indexOf("/* @") != -1 || comment.getValue().indexOf("@") != -1) {
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/com/google/javascript/jscomp/parsing/IRFactory.java: 252
if (comment.getValue().indexOf("/* @") != -1 || comment.getValue().indexOf("@") != -1) {
```

#### III. Explanation
To fix the bug, ```if (comment.getValue().indexOf("/* @") != -1 || comment.getValue().indexOf("\n * @") != -1) {``` must changed that it must find comments that include the ```@``` character.
<br><br>