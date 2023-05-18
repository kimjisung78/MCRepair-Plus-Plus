# Closure 86
* <h4>Bug type: Type 3 (T1B / T1F, T2F, T3F)</h4>
* <h4>The number of chunks: 2 chunks (1 used chunk / 1, 2 fixed chunks)</h4>
* <h4>The number of locations: 3 locations (1 used location / 1, 2, 3 fixed locations)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/com/google/javascript/jscomp/NodeUtil.java: 2461-2466
    case Token.NEW:
        // TODO(nicksantos): This needs to be changed so that it
        // returns true iff we're sure the value was never aliased from inside
        // the constructor (similar to callHasLocalResult)
-       return true;
+       return false;
    case Token.FUNCTION:
```
<br>

## 2. Used chunks and locations - T1B
* The number of used chunks: 1 chunk
* The number of used locations: 1 location
```java
src/com/google/javascript/jscomp/NodeUtil.java: 2465
return true;
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 10
    * T1F (6): 12, 143, 161, 162, 186, 279
    * T2F (3): 245, 290, 344
    * T3F (1): 570
<br><br>

## 4. Examples of correct patches
### 4.1. 12nd patch - T1F
#### I. Fixed Result
```java
src/com/google/javascript/jscomp/NodeUtil.java: 2465
-   return true;
+   return false;
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/com/google/javascript/jscomp/NodeUtil.java: 2465
return false;
```
<br>

### 4.2. 245th patch - T2F
#### I. Fixed Result
```java
src/com/google/javascript/jscomp/NodeUtil.java: 2464-2465
-   case Token.NEW:
+   case Token.NEW:{
-       return true;
+       return false; 
+   }
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 3 locations
```java
src/com/google/javascript/jscomp/NodeUtil.java: 2464-2465
case Token.NEW:{
    return false;
}
```
<br>

### 4.3. 570th patch - T3F
#### I. Fixed Result
```java
src/com/google/javascript/jscomp/NodeUtil.java: 2424
-   static boolean evaluatesToLocalValue(Node value, Predicate<Node> locals) {
+   private static boolean evaluatesToLocalValue(Node value, Predicate<Node> locals) {
```

```java
src/com/google/javascript/jscomp/NodeUtil.java: 2465
-   return true;
+   return false;
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 2 chunks
* The number of fixed locations: 2 locations
```java
src/com/google/javascript/jscomp/NodeUtil.java: 2424
private static boolean evaluatesToLocalValue(Node value, Predicate<Node> locals) {
```

```java
src/com/google/javascript/jscomp/NodeUtil.java: 2465
return false;
```
<br>