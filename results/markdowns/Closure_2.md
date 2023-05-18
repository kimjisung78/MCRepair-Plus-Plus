# Closure 2
* <h4>Bug type: Type 3 (T1B / T2F, T3F)</h4>
* <h4>The number of chunks: 2 chunks (1 used chunk / 1, 2 fixed chunks)</h4>
* <h4>The number of locations: 4 locations (1 used location / 2, 3, 4 fixed locations)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/com/google/javascript/jscomp/TypeCheck.java: 1570-1574
    ObjectType implicitProto = interfaceType.getImplicitPrototype();
    Set<String> currentPropertyNames;
+   if (implicitProto == null) {
    // This can be the case if interfaceType is proxy to a non-existent
    // object (which is a bad type annotation, but shouldn't crash).
+       currentPropertyNames = ImmutableSet.of();
+   } else {
        currentPropertyNames = implicitProto.getOwnPropertyNames();
+   }
```
<br>

## 2. Used chunks and locations - T1B
* The number of used chunks: 1 chunk
* The number of used locations: 1 location
```java
src/com/google/javascript/jscomp/TypeCheck.java: 1574
currentPropertyNames = implicitProto.getOwnPropertyNames();
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 11
    * T2F: 57, 118, 136, 190
    * T3F: 358, 378, 380, 384, 396, 400, 408
<br><br>

## 4. Examples of correct patches
### 4.1. 118th patch - T2F
#### I. Fixed Result
```java
src/com/google/javascript/jscomp/TypeCheck.java: 1574
+   if (implicitProto == null) { 
+      return; 
+   } 
    currentPropertyNames = implicitProto . getOwnPropertyNames ( ) ;
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 3 locations
```java
src/com/google/javascript/jscomp/TypeCheck.java: 1574
Three locations were inserted in front of Location 1574.
```

#### III. Explanation
To fix the bug, it must check or handle null about ```implicitProto```. The patch checked the null. 
<br>

### 4.2. 378th patch - T3F
#### I. Fixed Result
```java
src/com/google/javascript/jscomp/TypeCheck.java: 1574
+   if (implicitProto != null) {  
        currentPropertyNames = implicitProto . getOwnPropertyNames ( ) ;
```

```java
src/com/google/javascript/jscomp/TypeCheck.java: 1588-1592
        for (ObjectType iType : interfaceType.getCtorExtendedInterfaces()) {
                checkInterfaceConflictProperties(t, n, functionName, properties,
                    currentProperties, iType);
            }
+       }  
    }
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 2 chunks
* The number of fixed locations: 2 locations
```java
src/com/google/javascript/jscomp/TypeCheck.java: 1574
A location was inserted in front of Location 1574.
```

```java
src/com/google/javascript/jscomp/TypeCheck.java: 1592
A location was inserted in front of Location 1592.
```

#### III. Explanation
To fix the bug, its source code must check or handle null about ```implicitProto```. The patch checked and avoided the null. 
<br><br>

### 4.3. 400st patch - T3F
#### I. Fixed Result
```java
src/com/google/javascript/jscomp/TypeCheck.java: 1574
+   try { 
        currentPropertyNames = implicitProto . getOwnPropertyNames ( ) ;
```

```java
src/com/google/javascript/jscomp/TypeCheck.java: 1588-1591
    for (ObjectType iType : interfaceType.getCtorExtendedInterfaces()) {
        checkInterfaceConflictProperties(t, n, functionName, properties,
            currentProperties, iType);
-   }
+   } catch (Exception e) { 
+       e.printStackTrace(); 
+   }
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 2 chunks
* The number of fixed locations: 4 locations
```java
src/com/google/javascript/jscomp/TypeCheck.java: 1574
A location was inserted in front of Location 1574.
```

```java
src/com/google/javascript/jscomp/TypeCheck.java: 1591
-   }
+   } catch (Exception e) { 
+       e.printStackTrace(); 
+   }
```

#### III. Explanation
To fix the bug, its source code must check or handle null about ```implicitProto```. The patch handled the null.
<br><br>

