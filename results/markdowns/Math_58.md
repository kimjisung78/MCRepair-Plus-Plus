# Math 58
* <h4>Bug type: Type 1 (T1B / T1F)</h4>
* <h4>The number of chunks: 1 chunk (1 used chunk / 1 fixed chunk)</h4>
* <h4>The number of locations: 1 location (1 used location / 1 fixed location)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/main/java/org/apache/commons/math/optimization/fitting/GaussianFitter.java: 120-121
    final double[] guess = (new ParameterGuesser(getObservations())).guess();
-   return fit(new Gaussian.Parametric(), guess);
+   return fit(guess);
```               
<br>

## 2. Used chunks and locations - T1B
* The number of used chunks: 1 chunk
* The number of used locations: 1 location
```java
src/main/java/org/apache/commons/math/optimization/fitting/GaussianFitter.java: 121
return fit(new Gaussian.Parametric(), guess);
```       
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 3
    * T1F (3): 332, 336, 397
<br><br>

## 4. Examples of correct patches
### 4.1. 332nd patch - T1F
#### I. Fixed Result
```java
src/main/java/org/apache/commons/math/optimization/fitting/GaussianFitter.java: 121
-   return fit(new Gaussian.Parametric(), guess);
+   return fit(guess);
```  

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/main/java/org/apache/commons/math/optimization/fitting/GaussianFitter.java: 121
return fit(guess);
```  
<br>

### 4.2. 336th patch - T1F
#### I. Fixed Result
```java
src/main/java/org/apache/commons/math/optimization/fitting/GaussianFitter.java: 121
-   return fit(new Gaussian.Parametric(), guess);
+   return fit((double[]) guess);
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/main/java/org/apache/commons/math/optimization/fitting/GaussianFitter.java: 121
return fit((double[]) guess);
```  
<br><br>