# Math 34
* <h4>Bug type: Type 1 (T1B / T1F)</h4>
* <h4>The number of chunks: 1 chunk (1 used chunk / 1 fixed chunk)</h4>
* <h4>The number of locations: 1 location (1 used location / 1 fixed location)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/main/java/org/apache/commons/math3/genetics/ListPopulation.java: 208-210
    public Iterator<Chromosome> iterator() {
-       return chromosomes.iterator();
+       return getChromosomes().iterator();
    }
```
<br>

## 2. Used chunks and locations - T1B
* The number of used chunks: 1 chunk
* The number of used locations: 1 location
```java
src/main/java/org/apache/commons/math3/genetics/ListPopulation.java: 209
return chromosomes.iterator();
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 1
    * T1F (1): 341
<br><br>

## 4. Examples of correct patches
### 4.1. 341st patch - T1F
#### I. Fixed Result
```java
src/main/java/org/apache/commons/math3/genetics/ListPopulation.java: 209
-   return chromosomes.iterator();
+   return chromosomes.stream().iterator();
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/main/java/org/apache/commons/math3/genetics/ListPopulation.java: 209
return chromosomes.stream().iterator();
```

#### III. Explanation
To fix the bug, its source code must be changed that it returns an iterator of ```chromosomes``` field.
<br><br>