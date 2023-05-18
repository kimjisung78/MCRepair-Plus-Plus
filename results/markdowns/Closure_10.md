# Closure 10
* <h4>Bug type: Type 1 (T1B / T1F)</h4>
* <h4>The number of chunks: 1 chunk (1 used chunk / 1 fixed chunk)</h4>
* <h4>The number of locations: 1 location (1 used location / 1 fixed location)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/com/google/javascript/jscomp/NodeUtil.java: 1416-1420
    if (recurse) {
-       return allResultsMatch(n, MAY_BE_STRING_PREDICATE);
+       return anyResultsMatch(n, MAY_BE_STRING_PREDICATE);
    } else {
        return mayBeStringHelper(n);
    }
```
<br>

## 2. Used chunks and locations - T1B
* The number of used chunks: 1 chunk
* The number of used locations: 1 location
```java
src/com/google/javascript/jscomp/NodeUtil.java: 1417
return allResultsMatch(n, MAY_BE_STRING_PREDICATE);
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 4
    * T1F (4): 4, 385, 407, 717
<br><br>

## 4. Examples of correct patches
### 4.1. 4th patch - T1F
#### I. Fixed Result
```java
src/com/google/javascript/jscomp/NodeUtil.java: 1417
-   return allResultsMatch(n, MAY_BE_STRING_PREDICATE);
+   return anyResultsMatch(n, MAY_BE_STRING_PREDICATE);
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/com/google/javascript/jscomp/NodeUtil.java: 1417
return anyResultsMatch(n, MAY_BE_STRING_PREDICATE);
```
<br>

### 4.2. 407th patch - T1F
#### I. Fixed Result
```java
src/com/google/javascript/jscomp/NodeUtil.java: 1417
-   return allResultsMatch(n, MAY_BE_STRING_PREDICATE);
+   return (anyResultsMatch(n, MAY_BE_STRING_PREDICATE));
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/com/google/javascript/jscomp/NodeUtil.java: 1417
return (anyResultsMatch(n, MAY_BE_STRING_PREDICATE));
```
<br><br>