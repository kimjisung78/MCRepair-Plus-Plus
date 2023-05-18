# Lang 10
* <h4>Bug type: Type 3 (T3B / T2F, T3F)</h4>
* <h4>The number of chunks: 3 chunks (2 used chunks / 1, 2, 3 fixed chunks)</h4>
* <h4>The number of locations: 10 locations (9 used locations / 8, 9, 10 fixed locations)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/main/java/org/apache/commons/lang3/time/FastDateParser.java: 304-314
-   boolean wasWhite=false;
    for(int i= 0; i<value.length(); ++i) {
        char c= value.charAt(i);
-       if(Character.isWhitespace(c)) {
-           if(!wasWhite) {
-               wasWhite=true;
-               regex.append("\\s*+");
-           }
-           continue;
-       }
-       wasWhite= false;
```
<br>

## 2. Used chunks and locations - T3B
* The number of used chunks: 2 chunks
* The number of used locations: 9 locations
```java
src/main/java/org/apache/commons/lang3/time/FastDateParser.java: 304
boolean wasWhite=false;
```

```java
src/main/java/org/apache/commons/lang3/time/FastDateParser.java: 307-314
if(Character.isWhitespace(c)) {
    if(!wasWhite) {
        wasWhite=true;
        regex.append("\\s*+");
    }
    continue;
}
wasWhite= false;
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 8
    * T2F (1): 377
    * T3F (7): 9, 39, 57, 60, 65, 445, 483
<br><br>

## 4. Examples of correct patches
### 4.1. 9th patch - T3F
#### I. Fixed Result
```java
src/main/java/org/apache/commons/lang3/time/FastDateParser.java: 304-314
-   boolean wasWhite=false;
    for(int i= 0; i<value.length(); ++i) {
        char c= value.charAt(i);
-       if(Character.isWhitespace(c)) {
-           if(!wasWhite) {
-               wasWhite=true;
-               regex.append("\\s*+");
-           }
-           continue;
-       }
-       wasWhite= false;
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 2 chunks
* The number of fixed locations: 9 locations
```java
src/main/java/org/apache/commons/lang3/time/FastDateParser.java: 304
Location 304 was deleted.
```

```java
src/main/java/org/apache/commons/lang3/time/FastDateParser.java: 307-314
Location 307 was deleted.
Location 308 was deleted.
Location 309 was deleted.
Location 310 was deleted.
Location 311 was deleted.
Location 312 was deleted.
Location 313 was deleted.
Location 314 was deleted.
```
<br><br>

### 4.2. 39th patch - T3F
#### I. Fixed Result
```java
src/main/java/org/apache/commons/lang3/time/FastDateParser.java: 304-314
-   boolean wasWhite=false;
+   boolean wasWhite=true;
    for(int i= 0; i<value.length(); ++i) {
        char c= value.charAt(i);
-       if(Character.isWhitespace(c)) {
-           if(!wasWhite) {
-               wasWhite=true;
-               regex.append("\\s*+");
-           }
-           continue;
-       }
-       wasWhite= false;
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 2 chunks
* The number of fixed locations: 9 locations
```java
src/main/java/org/apache/commons/lang3/time/FastDateParser.java: 304
boolean wasWhite=true;
```

```java
src/main/java/org/apache/commons/lang3/time/FastDateParser.java: 307-314
Location 307 was deleted.
Location 308 was deleted.
Location 309 was deleted.
Location 310 was deleted.
Location 311 was deleted.
Location 312 was deleted.
Location 313 was deleted.
Location 314 was deleted.
```

#### III. Explanation
Because ```boolean wasWhite``` variable is not called in its method, the varible is equivalent to its deletion.
<br><br>

### 4.3. 377th patch - T2F
#### I. Fixed Result
```java
src/main/java/org/apache/commons/lang3/time/FastDateParser.java: 304-314
    boolean wasWhite=false;
    for(int i= 0; i<value.length(); ++i) {
        char c= value.charAt(i);
-       if(Character.isWhitespace(c)) {
-           if(!wasWhite) {
-               wasWhite=true;
-               regex.append("\\s*+");
-           }
-           continue;
-       }
-       wasWhite= false;
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 8 locations
```java
src/main/java/org/apache/commons/lang3/time/FastDateParser.java: 307-314
Location 307 was deleted.
Location 308 was deleted.
Location 309 was deleted.
Location 310 was deleted.
Location 311 was deleted.
Location 312 was deleted.
Location 313 was deleted.
Location 314 was deleted.
```

#### III. Explanation
Its reason is the same as the reason in the 39th patch.
<br><br>

### 4.4. 445th patch - T3F
#### I. Fixed Result
```java
src/main/java/org/apache/commons/lang3/time/FastDateParser.java: 304-314
-   boolean wasWhite=false;
    for(int i= 0; i<value.length(); ++i) {
        char c= value.charAt(i);
-       if(Character.isWhitespace(c)) {
-           if(!wasWhite) {
-               wasWhite=true;
-               regex.append("\\s*+");
-           }
-           continue;
-       }
-       wasWhite= false;
```

```java
src/main/java/org/apache/commons/lang3/time/FastDateParser.java: 318-320
    if(++i==value.length()) {
-       return regex;
+       break;
    }
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 3 chunks
* The number of fixed locations: 10 locations
```java
src/main/java/org/apache/commons/lang3/time/FastDateParser.java: 304
Location 304 was deleted.
```

```java
src/main/java/org/apache/commons/lang3/time/FastDateParser.java: 307-314
Location 307 was deleted.
Location 308 was deleted.
Location 309 was deleted.
Location 310 was deleted.
Location 311 was deleted.
Location 312 was deleted.
Location 313 was deleted.
Location 314 was deleted.
```

```java
src/main/java/org/apache/commons/lang3/time/FastDateParser.java: 319
break;
```

#### III. Explanation
The patch returned ```regex``` variable using the break statement in Location 319;
<br><br>