# Closure 102
* <h4>Bug type: Type 3 (T3B / T3F)</h4>
* <h4>The number of chunks: 3 chunks (2 used chunks / 2, 3 fixed chunks)</h4>
* <h4>The number of locations: 3 locations (2 used locations / 2, 3 fixed locations)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/com/google/javascript/jscomp/Normalize.java: 88-94
    NodeTraversal.traverse(compiler, root, this);            
+   removeDuplicateDeclarations(root);            
    if (MAKE_LOCAL_NAMES_UNIQUE) {            
        MakeDeclaredNamesUnique renamer = new MakeDeclaredNamesUnique();            
        NodeTraversal t = new NodeTraversal(compiler, renamer);            
        t.traverseRoots(externs, root);            
    }            
-   removeDuplicateDeclarations(root);
```
<br>

## 2. Used chunks and locations - T3B
* The number of used chunks: 2 chunks
* The number of used locations: 2 locations
```java
src/com/google/javascript/jscomp/Normalize.java: 89
FAULT_OF_OMISSION
```

```java
src/com/google/javascript/jscomp/Normalize.java: 94
removeDuplicateDeclarations(root);
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 4
    * T3F (4): 14, 231, 755, 848
<br><br>

## 4. Examples of correct patches
### 4.1. 14th patch - T3F
#### I. Fixed Result
```java
src/com/google/javascript/jscomp/Normalize.java: 86-97
(Locations 95-96 are divided.)
    @Override            
    public void process(Node externs, Node root) {
        NodeTraversal.traverse(compiler, root, this);
+       removeDuplicateDeclarations(root);
        if (MAKE_LOCAL_NAMES_UNIQUE) {
            MakeDeclaredNamesUnique renamer = new MakeDeclaredNamesUnique();
            NodeTraversal t = new NodeTraversal(compiler, renamer);
            t.traverseRoots(externs, root);
        }
-       removeDuplicateDeclarations(root);
        new PropogateConstantAnnotations(compiler, assertOnChange)
            .process(externs, root);
    }
```

#### II. Fixed chunks and locations 
* The number of fixed chunks: 2 chunks
* The number of fixed locations: 2 locations
```java
src/com/google/javascript/jscomp/Normalize.java: 89
A location was inserted in front of Location 89.
```

```java
src/com/google/javascript/jscomp/Normalize.java: 94
Location 94 was deleted.
```
<br>

### 4.2. 755th patch - T3F
#### I. Fixed Result
```java
src/com/google/javascript/jscomp/Normalize.java: 88-97
    NodeTraversal.traverse(compiler, root, this);     
+   removeDuplicateDeclarations(root);            
    if (MAKE_LOCAL_NAMES_UNIQUE) {            
        MakeDeclaredNamesUnique renamer = new MakeDeclaredNamesUnique();            
        NodeTraversal t = new NodeTraversal(compiler, renamer);            
        t.traverseRoots(externs, root);            
    }            
-   removeDuplicateDeclarations(root);
```

```java
src/com/google/javascript/jscomp/Normalize.java: 95-97
(Locations 95-96 are divided.)
        new PropogateConstantAnnotations(compiler, assertOnChange)            
            .process(externs, root);
+   return;
    }
```

#### II. Fixed chunks and locations 
* The number of fixed chunks: 3 chunks
* The number of fixed locations: 3 locations
```java
src/com/google/javascript/jscomp/Normalize.java: 89
A location was inserted in front of Location 89.
```

```java
src/com/google/javascript/jscomp/Normalize.java: 94
Location 94 was deleted.
```

```java
src/com/google/javascript/jscomp/Normalize.java: 97
A location was inserted in front of Location 97.
```

#### III. Explanation
A ```void``` method is equivalent to a method that performs ```return;```.
<br><br>