# Closure 6
* <h4>Bug type: Type 3 (T3B / T3F)</h4>
* <h4>The number of chunks: 4 chunks (4 used chunks / 3 fixed chunks)</h4>
* <h4>The number of locations: 8 locations (8 used locations / 7 fixed locations)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/com/google/javascript/jscomp/TypeValidator.java: 365-368
    if (!leftType.isNoType() && !rightType.canAssignTo(leftType)) {
-       if ((leftType.isConstructor() || leftType.isEnumType()) && (rightType.isConstructor() || rightType.isEnumType())) {
-           registerMismatch(rightType, leftType, null);
-       } else {
```

```java
src/com/google/javascript/jscomp/TypeValidator.java: 385-387
-       }
        return false;
    }
```

```java
src/com/google/javascript/jscomp/TypeValidator.java: 404-411
    if (!rightType.canAssignTo(leftType)) {
-       if ((leftType.isConstructor() || leftType.isEnumType()) && (rightType.isConstructor() || rightType.isEnumType())) {
-           registerMismatch(rightType, leftType, null);
-       } else {
        mismatch(t, n, msg, rightType, leftType);
-       }
        return false;
    }
```
<br>

## 2. Used chunks and locations - T3B
* The number of used chunks: 4 chunks
* The number of used locations: 8 locations
```java
src/com/google/javascript/jscomp/TypeValidator.java: 365-368
-   if ((leftType.isConstructor() || leftType.isEnumType()) && (rightType.isConstructor() || rightType.isEnumType())) {
-       registerMismatch(rightType, leftType, null);
-   } else {
```

```java
src/com/google/javascript/jscomp/TypeValidator.java: 385
-   }
```

```java
src/com/google/javascript/jscomp/TypeValidator.java: 405-407
-   if ((leftType.isConstructor() || leftType.isEnumType()) && (rightType.isConstructor() || rightType.isEnumType())) {
-       registerMismatch(rightType, leftType, null);
-   } else {
```

```java
src/com/google/javascript/jscomp/TypeValidator.java: 409
-   }
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 2
    * T3F (2): 19,792, 19,808
<br><br>

## 4. Examples of correct patches
### 4.1. 19,808th patch - T3F
#### I. Fixed Result
```java
src/com/google/javascript/jscomp/TypeValidator.java: 365-368
-   if ((leftType.isConstructor() || leftType.isEnumType()) && (rightType.isConstructor() || rightType.isEnumType())) {
-       registerMismatch(rightType, leftType, null);
-   } else {
+   if (!leftType.isConstructor ( ) && !rightType.canAssignTo(leftType)) {
```

```java
src/com/google/javascript/jscomp/TypeValidator.java: 405-409
-   if ((leftType.isConstructor() || leftType.isEnumType()) && (rightType.isConstructor() || rightType.isEnumType())) {
-       registerMismatch(rightType, leftType, null);
-   } else {
+   if (leftType.isConstructor() || leftType.isEnumType())
+   mismatch(t, n, msg, rightType, leftType);
+   else
    mismatch(t, n, msg, rightType, leftType);
-   }
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 3 chunks
* The number of fixed locations: 7 locations
```java
src/com/google/javascript/jscomp/TypeValidator.java: 365-368
if (!leftType.isConstructor ( ) && !rightType.canAssignTo(leftType)) {
```

```java
src/com/google/javascript/jscomp/TypeCheck.java: 405-407
if (leftType.isConstructor() || leftType.isEnumType())
    mismatch(t, n, msg, rightType, leftType);
else
```

```java
src/com/google/javascript/jscomp/TypeValidator.java: 409
Location 409 was deleted.
```

#### III. Explanation
To fix the bug, its source code must be changed that it removes ```registerMismatch(rightType, leftType, null)``` calls about ```leftType``` and ```rightType``` that are constructors or enums. The patch removed the calls.
<br><br>