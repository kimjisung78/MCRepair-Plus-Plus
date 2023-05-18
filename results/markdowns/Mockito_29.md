# Mockito 29
* <h4>Bug type: Type 1 (T1B / T1F)</h4>
* <h4>The number of chunks: 1 chunk (1 used chunk / 1 fixed chunk)</h4>
* <h4>The number of locations: 1 location (1 used location / 1 fixed location)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/org/mockito/internal/matchers/Same.java: 29
-   description.appendText(wanted.toString());
+   description.appendText(wanted == null ? "null" : wanted.toString());
```
<br>

## 2. Used chunks and locations - T1B
* The number of used chunks: 1 chunk
* The number of used locations: 1 location
```java
src/org/mockito/internal/matchers/Same.java: 29
description.appendText(wanted.toString());
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 1
    * T1F (1): 444
<br><br>

## 4. Examples of correct patches
### 4.1. 444th patch - T1F
#### I. Fixed Result
```java
src/org/mockito/internal/matchers/Same.java: 29
-   description.appendText(wanted.toString());
+   description.appendText(String.valueOf(wanted));
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/org/mockito/internal/matchers/Same.java: 29
description.appendText(String.valueOf(wanted));
```

#### III. Explanation
```String.valueOf(wanted)``` is equivalent to ```wanted == null ? "null" : wanted.toString()``` as follows.
```java
System.out.println(String.valueOf(null)); // "null"
System.out.println(String.valueOf("346")); // "346"
```
<br><br>