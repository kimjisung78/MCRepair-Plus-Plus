# Lang 6
* <h4>Bug type: Type 1 (T1B / T1F)</h4>
* <h4>The number of chunks: 1 chunk (1 used chunk / 1 fixed chunk)</h4>
* <h4>The number of locations: 1 location (1 used location / 1 fixed location)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/main/java/org/apache/commons/lang3/text/translate/CharSequenceTranslator.java: 94-96
    for (int pt = 0; pt < consumed; pt++) {
-       pos += Character.charCount(Character.codePointAt(input, pos));
+       pos += Character.charCount(Character.codePointAt(input, pt));
    }
```
<br>

## 2. Used chunks and locations - T1B
* The number of used chunks: 1 chunk
* The number of used locations: 1 location
```java
src/main/java/org/apache/commons/lang3/text/translate/CharSequenceTranslator.java: 95
pos += Character.charCount(Character.codePointAt(input, pos));
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 1
    * T1F (1): 146
<br><br>

## 4. Examples of correct patches
### 4.1. 146th patch - T1F
#### I. Fixed Result
```java
src/main/java/org/apache/commons/lang3/text/translate/CharSequenceTranslator.java: 95
-   pos += Character.charCount(Character.codePointAt(input, pos));
+   pos += Character.charCount(Character.codePointAt(input, pt));
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/main/java/org/apache/commons/lang3/text/translate/CharSequenceTranslator.java: 95
pos += Character.charCount(Character.codePointAt(input, pt));
```
<br><br>