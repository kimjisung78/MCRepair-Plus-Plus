# Closure 11
* <h4>Bug type: Type 3 (T2B / T2F, T3F)</h4>
* <h4>The number of chunks: 2 chunks (1 used chunk / 1, 2 fixed chunks)</h4>
* <h4>The number of locations: 3 locations (2 used locations / 2, 3 fixed locations)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/com/google/javascript/jscomp/TypeCheck.java: 1312-1315
    if (childType.isDict()) {
        report(t, property, TypeValidator.ILLEGAL_PROPERTY_ACCESS, "'.'", "dict");
-   } else if (n.getJSType() != null && parent.isAssign()) {
-       return;
```
<br>

## 2. Used chunks and locations - T2B
* The number of used chunks: 1 chunk
* The number of used locations: 2 locations
```java
src/com/google/javascript/jscomp/TypeCheck.java: 1314-1315
} else if (n.getJSType() != null && parent.isAssign()) {
    return;
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 2
    * T2F (1): 19
    * T3F (1): 37
<br><br>

## 4. Examples of correct patches
### 4.1. 19th patch - T2F
#### I. Fixed Result
```java
src/com/google/javascript/jscomp/TypeCheck.java: 1314-1315
-   } else if (n.getJSType() != null && parent.isAssign()) {            
-       return;
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 2 locations
```java
src/com/google/javascript/jscomp/TypeCheck.java: 1314-1315
Location 1314 was deleted.
Location 1315 was deleted.
```
<br><br>

### 4.2. 37th patch - T3F
#### I. Fixed Result
```java
src/com/google/javascript/jscomp/TypeCheck.java: 1314-1315
-   } else if (n.getJSType() != null && parent.isAssign()) {            
-       return;
```

```java
src/com/google/javascript/jscomp/TypeCheck.java: 1320-1321
        ensureTyped(t, n);           
+       return;
    }
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 2 chunks
* The number of fixed locations: 3 locations
```java
src/com/google/javascript/jscomp/TypeCheck.java: 1314-1315
Location 1314 was deleted.
Location 1315 was deleted.
```

```java
src/com/google/javascript/jscomp/TypeCheck.java: 1321
A location was inserted in front of Location 1321.
```

#### III. Explanation
A ```void``` method is equivalent to a method that performs ```return;```.
<br><br>