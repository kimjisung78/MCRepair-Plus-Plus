# Closure 40
* <h4>Bug type: Type 3 (T3B / T1F, T3F)</h4>
* <h4>The number of chunks: 3 chunks (2 used chunks / 1, 2, 3 fixed chunks)</h4>
* <h4>The number of locations: 4 locations (3 used locations / 1, 3, 4 fixed locations)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/com/google/javascript/jscomp/NameAnalyzer.java: 633-640
    NameInformation ns = createNameInformation(t, nameNode, n);
    if (ns != null && ns.onlyAffectsClassDef) {
-       JsName name = getName(ns.name, false);
+       JsName name = getName(ns.name, true);
-       if (name != null) {
            refNodes.add(new ClassDefiningFunctionNode(
                name, n, parent, parent.getParent()));
-        }
    }
```
<br>

## 2. Used chunks and locations - T3B
* The number of used chunks: 2 chunks
* The number of used locations: 3 locations
```java
src/com/google/javascript/jscomp/NameAnalyzer.java: 635-636
JsName name = getName(ns.name, false);
if (name != null) {
```

```java
src/com/google/javascript/jscomp/NameAnalyzer.java: 639
}
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 10
    * T1F (1): 708
    * T3F (9): 224, 229, 245, 246, 320, 559, 578, 658, 693
<br><br>

## 4. Examples of correct patches
### 4.1. 229th patch - T3F
#### I. Fixed Result
```java
src/com/google/javascript/jscomp/NameAnalyzer.java: 634-640
(Locations 637-638 are divided.)
    if (ns != null && ns.onlyAffectsClassDef) {
-       JsName name = getName(ns.name, false);
+       JsName name = getName(ns.name, true);
-       if (name != null) {
+       if (name != null)
            refNodes.add(new ClassDefiningFunctionNode(
                name, n, parent, parent.getParent()));
-       }
-   }
+   } else {
+   }
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 2 chunks
* The number of fixed locations: 4 locations
```java
src/com/google/javascript/jscomp/NameAnalyzer.java: 635-636
JsName name = getName(ns.name, true);
if (name != null)
```

```java
src/com/google/javascript/jscomp/NameAnalyzer.java: 639-640
} else {
}
```
<br><br>

### 4.2. 246th patch - T3F
#### I. Fixed Result
```java
src/com/google/javascript/jscomp/NameAnalyzer.java: 635-639
(Locations 637-638 are divided.)
-   JsName name = getName(ns.name, false);
+   JsName name = getName(ns.name, true);
-   if (name != null) {
+   if (name != null)
        refNodes.add(new ClassDefiningFunctionNode(
            name, n, parent, parent.getParent()));
-   }
+   else
+       return;
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 2 chunks
* The number of fixed locations: 4 locations
```java
src/com/google/javascript/jscomp/NameAnalyzer.java: 635-636
JsName name = getName(ns.name, true);
if (name != null)
```

```java
src/com/google/javascript/jscomp/NameAnalyzer.java: 639
else
    return;
```
<br><br>

### 4.3. 559th patch - T3F
#### I. Fixed Result
```java
src/com/google/javascript/jscomp/NameAnalyzer.java: 635-639
(Locations 637-638 are divided.)
-   JsName name = getName(ns.name, false);
+   JsName name = getName(ns.name, true);
-   if (name != null) {
+   if (name != null)
        refNodes.add(new ClassDefiningFunctionNode(
            name, n, parent, parent.getParent()));
-   }
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 2 chunks
* The number of fixed locations: 3 locations
```java
src/com/google/javascript/jscomp/NameAnalyzer.java: 635-636
JsName name = getName(ns.name, true);
if (name != null)
```

```java
src/com/google/javascript/jscomp/NameAnalyzer.java: 639
Location 639 was deleted.
```

#### III. Explanation
```getName(ns.name, true)``` returns the name of ````ns.name`` after null-checking.
<br><br>

### 4.4. 658th patch - T3F
#### I. Fixed Result
```java
src/com/google/javascript/jscomp/NameAnalyzer.java: 595-596
-   @Override
    public void visit(NodeTraversal t, Node n, Node parent) {
```

```java
src/com/google/javascript/jscomp/NameAnalyzer.java: 635-639
(Locations 637-638 are divided.)
-   JsName name = getName(ns.name, false);
+   JsName name = getName(ns.name, true);
-   if (name != null) {
+   if (name != null)
        refNodes.add(new ClassDefiningFunctionNode(
            name, n, parent, parent.getParent()));
-   }
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 3 chunks
* The number of fixed locations: 4 locations
```java
src/com/google/javascript/jscomp/NameAnalyzer.java: 595
Location 595 was deleted.
```

```java
src/com/google/javascript/jscomp/NameAnalyzer.java: 635-636
JsName name = getName(ns.name, true);
if (name != null)
```

```java
src/com/google/javascript/jscomp/NameAnalyzer.java: 639
Location 639 was deleted.
```

#### III. Explanation
```getName(ns.name, true)``` returns the name of ````ns.name`` after null-checking.
<br><br>

### 4.5. 708th patch - T1F
#### I. Fixed Result
```java
src/com/google/javascript/jscomp/NameAnalyzer.java: 635-639
(Locations 637-638 are divided.)
-   JsName name = getName(ns.name, false);
+   JsName name = getName(ns.name, true);
    if (name != null) {
        refNodes.add(new ClassDefiningFunctionNode(
            name, n, parent, parent.getParent()));
    }
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/com/google/javascript/jscomp/NameAnalyzer.java: 635
JsName name = getName(ns.name, true);
```

#### III. Explanation
Its reason is the same as the reason in the 559th patch.
<br><br>