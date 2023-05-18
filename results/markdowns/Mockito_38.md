# Mockito 38
* <h4>Bug type: Type 1 (T1B / T1F)</h4>
* <h4>The number of chunks: 1 chunk (1 used chunk / 1 fixed chunk)</h4>
* <h4>The number of locations: 1 location (1 used location / 1 fixed location)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/org/mockito/internal/verification/argumentmatching/ArgumentMatchingTool.java: 48
-   return StringDescription.toString(m).equals(arg.toString());
+   return StringDescription.toString(m).equals(arg == null ? "null" : arg.toString());
```
<br>

## 2. Used chunks and locations - T1B
* The number of used chunks: 1 chunk
* The number of used locations: 1 location
```java
src/org/mockito/internal/verification/argumentmatching/ArgumentMatchingTool.java: 48
return StringDescription.toString(m).equals(arg.toString());
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 2
    * T1F (1): 355, 403
<br><br>

## 4. Examples of correct patches
### 4.1. 355th patch - T1F
#### I. Fixed Result
```java
src/org/mockito/internal/verification/argumentmatching/ArgumentMatchingTool.java: 48
-   return StringDescription.toString(m).equals(arg.toString());
+   return StringDescription.toString(m).equals(arg + "");
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/org/mockito/internal/verification/argumentmatching/ArgumentMatchingTool.java: 48
return StringDescription.toString(m).equals(arg + "");
```

#### III. Explanation
```arg + ""``` is equivalent to ```arg == null ? "null" : arg.toString()``` as follows.
```java
System.out.println(null  + "")); // "null"
System.out.println(346 + "")); // "346"
```
<br>

### 4.2. 403rd patch - T1F
#### I. Fixed Result
```java
src/org/mockito/internal/verification/argumentmatching/ArgumentMatchingTool.java: 48
-   return StringDescription.toString(m).equals(arg.toString());
+   return StringDescription.toString(m).equals(String.valueOf(arg));
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/org/mockito/internal/verification/argumentmatching/ArgumentMatchingTool.java: 48
return StringDescription.toString(m).equals(String.valueOf(arg));
```

#### III. Explanation
```String.valueOf(arg)``` is equivalent to ```arg == null ? "null" : arg.toString()``` as follows.
```java
System.out.println(String.valueOf(null)); // "null"
System.out.println(String.valueOf(346)); // "346"
```
<br><br>