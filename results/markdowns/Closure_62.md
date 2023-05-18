# Closure 62
* <h4>Bug type: Type 1 (T1B / T1F)</h4>
* <h4>The number of chunks: 1 chunk (1 used chunk / 1 fixed chunk)</h4>
* <h4>The number of locations: 1 location (1 used location / 1 fixed location)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/com/google/javascript/jscomp/LightweightMessageFormatter.java: 97-101
    if (excerpt.equals(LINE)
-       && 0 <= charno && charno < sourceExcerpt.length()) {
+       && 0 <= charno && charno <= sourceExcerpt.length()) {
    for (int i = 0; i < charno; i++) {
        char c = sourceExcerpt.charAt(i);
        if (Character.isWhitespace(c)) {
```
<br>

## 2. Used chunks and locations - T1B
* The number of used chunks: 1 chunk
* The number of used locations: 1 location
```java
src/com/google/javascript/jscomp/LightweightMessageFormatter.java: 97-98
(Locations 97-98 are divided.)
if (excerpt.equals(LINE) && 0 <= charno && charno < sourceExcerpt.length()) {
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 1
    * T1F (1): 62
<br><br>

## 4. Examples of correct patches
### 4.1. 62nd patch - T1F
#### I. Fixed Result
```java
src/com/google/javascript/jscomp/LightweightMessageFormatter.java: 97-98
(Locations 97-98 are divided.)
-   if (excerpt.equals(LINE) && 0 <= charno && charno < sourceExcerpt.length()) {
+   if (excerpt.equals(LINE) && 0 <= charno && charno <= sourceExcerpt.length()) {
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/com/google/javascript/jscomp/LightweightMessageFormatter.java: 97-98
(Locations 97-98 are divided.)
if (excerpt.equals(LINE) && 0 <= charno && charno <= sourceExcerpt.length()) {
```
<br><br>