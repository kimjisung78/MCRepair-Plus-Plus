# Closure 19
* <h4>Bug type: Type 2 (T1B / T1F, T2F)</h4>
* <h4>The number of chunks: 1 chunk (1 used chunk / 1 fixed chunk)</h4>
* <h4>The number of locations: 2 locations (1 used location / 1, 2 fixed locations)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/com/google/javascript/jscomp/type/ChainableReverseAbstractInterpreter.java: 172-176
+   case Token.THIS:
    // "this" references aren't currently modeled in the CFG.
+       break;

    default:
        throw new IllegalArgumentException("Node cannot be refined. \n" +
            node.toStringTree());
```
<br>

## 2. Used chunks and locations - T1B
* The number of used chunks: 1 chunk
* The number of used locations: 1 location
```java
src/com/google/javascript/jscomp/type/ChainableReverseAbstractInterpreter.java: 174
FAULT_OF_OMISSION
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 3
    * T1F (2): 808, 809
    * T2F (1): 811
<br><br>

## 4. Examples of correct patches
### 4.1. 808th patch - T1F
#### I. Fixed Result
```java
src/com/google/javascript/jscomp/type/ChainableReverseAbstractInterpreter.java: 175-177
(Locations 176-177 are divided.)
    default:
+       throw new IllegalArgumentException("Node cannot be refined. \n" + node.toStringTree());
-       break;
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/com/google/javascript/jscomp/type/ChainableReverseAbstractInterpreter.java: 176-177
(Locations 176-177 are divided.)
break;
```

#### III. Explanation
```IllegalArgumentException``` indicates that a method has been passed an illegal or inappropriate argument. Therefore, throwing the exception is optional. Therefore, the change to remove the throwing does not affect its source code.
<br><br>

### 4.2. 811st patch - T2F
#### I. Fixed Result
```java
src/com/google/javascript/jscomp/type/ChainableReverseAbstractInterpreter.java: 175-177
(Locations 176-177 are divided.)
-   default:
-       throw new IllegalArgumentException("Node cannot be refined. \n" + node.toStringTree());
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 2 locations
```java
src/com/google/javascript/jscomp/type/ChainableReverseAbstractInterpreter.java: 175-177
(Locations 176-177 are divided.)
Location 175 was deleted.
Divided Locations 176 and 177 were deleted.
```

#### III. Explanation
Its reason is the same as the reason in the 808th patch.
<br><br>