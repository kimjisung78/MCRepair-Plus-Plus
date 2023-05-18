# Math 8
* <h4>Bug type: Type 3 (T3B / T1F, T2F, T3F)</h4>
* <h4>The number of chunks: 2 chunks (2 used chunks / 1, 2 fixed chunks)</h4>
* <h4>The number of locations: 5 locations (2 used locations / 1, 2, 5 fixed locations)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/main/java/org/apache/commons/math3/distribution/DiscreteDistribution.java: 181-195
-   public T[] sample(int sampleSize) throws NotStrictlyPositiveException {
+   public Object[] sample(int sampleSize) throws NotStrictlyPositiveException {
        if (sampleSize <= 0) {
            throw new NotStrictlyPositiveException(LocalizedFormats.NUMBER_OF_SAMPLES,
                    sampleSize);
        }

-       final T[] out = (T[]) java.lang.reflect.Array.newInstance(singletons.get(0).getClass(), sampleSize);
+       final Object[] out = new Object[sampleSize];

        for (int i = 0; i < sampleSize; i++) {
            out[i] = sample();
        }

        return out;

    }
```
<br>

## 2. Used chunks and locations - T3B
* The number of used chunks: 2 chunks
* The number of used locations: 2 locations
```java
src/main/java/org/apache/commons/math3/distribution/DiscreteDistribution.java: 181
public T[] sample(int sampleSize) throws NotStrictlyPositiveException {
```

```java
src/main/java/org/apache/commons/math3/distribution/DiscreteDistribution.java: 187
final T[]out = (T[]) java.lang.reflect.Array.newInstance(singletons.get(0).getClass(), sampleSize);
```
<br><br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 8
    * T1F (3): 213, 217, 762
    * T2F (1): 881
    * T3F (4): 220, 224, 384, 408
<br><br>

## 4. Examples of correct patches
### 4.1. 217th patch - T1F
#### I. Fixed Result
```java
src/main/java/org/apache/commons/math3/distribution/DiscreteDistribution.java: 188
-   final T[] out = (T[]) java.lang.reflect.Array.newInstance(singletons.get(0).getClass(), sampleSize);
+   final T[] out = (T[]) java.lang.reflect.Array.newInstance(singletons.get(1).getClass(), sampleSize);
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/main/java/org/apache/commons/math3/distribution/DiscreteDistribution.java: 188
final T[] out = (T[]) java.lang.reflect.Array.newInstance(singletons.get(1).getClass(), sampleSize);
```

#### III. Explanation
To fix the bug, its source code must be changed that it returns ```Object``` class value or its sub-class value.
<br>

### 4.2. 220th patch - T3F
#### I. Fixed Result
```java
src/main/java/org/apache/commons/math3/distribution/DiscreteDistribution.java: 181
-   public T[] sample(int sampleSize) throws NotStrictlyPositiveException {
+   public Object[] sample(int sampleSize) throws NotStrictlyPositiveException {
```

```java
src/main/java/org/apache/commons/math3/distribution/DiscreteDistribution.java: 188
-   final T[] out = (T[]) java.lang.reflect.Array.newInstance(singletons.get(0).getClass(), sampleSize);
+   final T[] out = (T[]) java.lang.reflect.Array.newInstance(singletons.get(1).getClass(), sampleSize);
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 2 chunks
* The number of fixed locations: 2 locations
```java
src/main/java/org/apache/commons/math3/distribution/DiscreteDistribution.java: 181
public Object[] sample(int sampleSize) throws NotStrictlyPositiveException {
```

```java
src/main/java/org/apache/commons/math3/distribution/DiscreteDistribution.java: 188
final T[] out = (T[]) java.lang.reflect.Array.newInstance(singletons.get(1).getClass(), sampleSize);
```

#### III. Explanation
Its reason is the same as the reason in the 220th patch.
<br>

### 4.3. 762nd patch - T1F
#### I. Fixed Result
```java
src/main/java/org/apache/commons/math3/distribution/DiscreteDistribution.java: 190
-   out[i] = sample();
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/main/java/org/apache/commons/math3/distribution/DiscreteDistribution.java: 190
Location 190 was deleted.
```

#### III. Explanation
Because ```out``` variable is called in Location 190 after converting with Generic, the bug occurs. To fix the bug, Location 190 must be deleted.
<br>

### 4.4. 881st patch - T2F
#### I. Fixed Result
```java
src/main/java/org/apache/commons/math3/distribution/DiscreteDistribution.java: 187-193
(Locations 188 and 192 are not blank locations related to "FAULT_OF_OMISSION".)
-   final T[] out = (T[]) java.lang.reflect.Array.newInstance(singletons.get(0).getClass(), sampleSize);

-   for (int i = 0; i < sampleSize; i++) {
-       out[i] = sample();
-   }

-   return out; 
+   return (T[]) java.lang.reflect.Array.newInstance(singletons.get(0).getClass(), sampleSize);
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 5 locations
```java
src/main/java/org/apache/commons/math3/distribution/DiscreteDistribution.java: 187-193
(Locations 188 and 192 are not blank locations related to "FAULT_OF_OMISSION".)
return (T[]) java.lang.reflect.Array.newInstance(singletons.get(0).getClass(), sampleSize);
```

#### III. Explanation
Its reason is the same as the reason in the 762nd patch.
<br><br>