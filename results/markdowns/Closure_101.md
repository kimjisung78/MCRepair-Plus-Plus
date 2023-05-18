# Closure 101
* <h4>Bug type: Type 2 (T2B / T2F)</h4>
* <h4>The number of chunks: 1 chunk (1 used chunk / 1 fixed chunk)</h4>
* <h4>The number of locations: 4 locations (4 used locations / 4 fixed locations)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/com/google/javascript/jscomp/CommandLineRunner.java: 430-438
    for (FormattingOption formattingOption : flags.formatting) {
        formattingOption.applyToOptions(options);
    }
-   if (flags.process_closure_primitives) {
-       options.closurePass = true;
-   }

+   options.closurePass = flags.process_closure_primitives;
    initOptionsFromFlags(options);
    return options;
```
<br>

## 2. Used chunks and locations - T2B
* The number of used chunks: 1 chunk
* The number of used locations: 4 locations
```java
src/com/google/javascript/jscomp/CommandLineRunner.java: 433-435
if (flags.process_closure_primitives) {
    options.closurePass = true;
}

src/com/google/javascript/jscomp/CommandLineRunner.java: 437
FAULT_OF_OMISSION
```
* Location 436 is not a blank location related to "FAULT_OF_OMISSION."
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 1
    * T2F (1): 16
<br><br>

## 4. Examples of correct patches
### 4.1. 16th patch - T2F
#### I. Fixed Result
```java
src/com/google/javascript/jscomp/CommandLineRunner.java: 433-438
-   if (flags.process_closure_primitives) {
-       options.closurePass = true;
-   }

+   options.closurePass = flags.process_closure_primitives;
    initOptionsFromFlags(options);
    return options;
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 4 locations
```java
src/com/google/javascript/jscomp/CommandLineRunner.java: 433-435
Location 433 was deleted.
Location 434 was deleted.
Location 435 was deleted.

src/com/google/javascript/jscomp/CommandLineRunner.java: 437
A location was inserted in front of Location 437.
```
<br><br>