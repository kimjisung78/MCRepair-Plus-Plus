# Math 75
* <h4>Bug type: Type 3 (T1B / T1F, T2F, T3F)</h4>
* <h4>The number of chunks: 2 chunks (1 used chunk / 1, 2 fixed chunks)</h4>
* <h4>The number of locations: 2 locations (1 used location / 1, 2 fixed locations)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/main/java/org/apache/commons/math/stat/Frequency.java: 301-304
    @Deprecated
    public double getPct(Object v) {
-       return getCumPct((Comparable<?>) v);
+       return getPct((Comparable<?>) v);
    }
```
<br>

## 2. Used chunks and locations - T1B
* The number of used chunks: 1 chunk
* The number of used locations: 1 location
```java
src/main/java/org/apache/commons/math/stat/Frequency.java: 303
return getCumPct((Comparable<?>) v);
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 13
    * T1F (7): 96, 385, 434, 436, 466, 503, 562
    * T2F (5): 573, 574, 575, 576, 577
    * T3F (1): 864
<br><br>

## 4. Examples of correct patches
### 4.1. 8th patch - T1F
#### I. Fixed Result
```java
src/main/java/org/apache/commons/math/stat/Frequency.java: 303
-   return getCumPct((Comparable<?>) v);
+   return getPct((Comparable<?>) v);
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/main/java/org/apache/commons/math/stat/Frequency.java: 303
return getPct((Comparable<?>) v);
```  
<br>

### 4.2. 573rd patch - T2F
#### I. Fixed Result
```java
src/main/java/org/apache/commons/math/stat/Frequency.java: 303
-   return getCumPct((Comparable<?>) v);
+   double value = getPct((Comparable<?>) v);
+   return value;
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 2 locations
```java
src/main/java/org/apache/commons/math/stat/Frequency.java: 303
double value = getPct((Comparable<?>) v);
return value;
```  
<br>

### 4.3. 864th patch - T3F
#### I. Fixed Result
```java
src/main/java/org/apache/commons/math/stat/Frequency.java: 301-304
-   @Deprecated
    public double getPct(Object v) {
-       return getCumPct((Comparable<?>) v);
+       return getPct((Comparable<?>) v);
    }
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 2 chunks
* The number of fixed locations: 2 locations
```java
src/main/java/org/apache/commons/math/stat/Frequency.java: 301
Location 301 was deleted.
```  

```java
src/main/java/org/apache/commons/math/stat/Frequency.java: 303
return getPct((Comparable<?>) v);
```  
<br><br>