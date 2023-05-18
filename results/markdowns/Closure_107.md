# Closure 107
* <h4>Bug type: Type 2 (T1B / T1F, T2F)</h4>
* <h4>The number of chunks: 1 chunk (1 used chunk / 1 fixed chunk)</h4>
* <h4>The number of locations: 3 locations (1 used location / 1, 2, 3 fixed locations)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/com/google/javascript/jscomp/CommandLineRunner.java: 844-862
    if (!flags.translationsFile.isEmpty()) {
        try {
            options.messageBundle = new XtbMessageBundle(
            new FileInputStream(flags.translationsFile),
                flags.translationsProject);
        } catch (IOException e) {
            throw new RuntimeException("Reading XTB file", e);
        }
    } else if (CompilationLevel.ADVANCED_OPTIMIZATIONS == level) {
        // In SIMPLE or WHITESPACE mode, if the user hasn't specified a
        // translations file, they might reasonably try to write their own
        // implementation of goog.getMsg that makes the substitution at
        // run-time.
        //
        // In ADVANCED mode, goog.getMsg is going to be renamed anyway,
        // so we might as well inline it. But shut off the i18n warnings,
        // because the user didn't really ask for i18n.
        options.messageBundle = new EmptyMessageBundle();
+       options.setWarningLevel(JsMessageVisitor.MSG_CONVENTIONS, CheckLevel.OFF);
    }
```
<br>

## 2. Used chunks and locations - T1B
* The number of used chunks: 1 chunk
* The number of used locations: 1 location
```java
src/com/google/javascript/jscomp/CommandLineRunner.java: 862
FAULT_OF_OMISSION
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 3
    * T1F (1): 78
    * T2F (2): 373, 714
<br><br>

## 4. Examples of correct patches
### 4.1. 78th patch - T1F
#### I. Fixed Result
```java
src/com/google/javascript/jscomp/CommandLineRunner.java: 861-862
        options.messageBundle = new EmptyMessageBundle();
+       options.messageBundle = null;
    }
```
<br>

#### II. Fixed chunks and locations 
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/com/google/javascript/jscomp/CommandLineRunner.java: 862
A location was inserted in front of Location 862.
```

#### III. Explanation
```EmptyMessageBundle ``` class only includes empty and null values. Therefore, ```options.messageBundle = new EmptyMessageBundle();``` is optional. Also, the deletion does not occur with any warnings and errors.
<br>

### 4.2.373rd patch - T1F
#### I. Fixed Result
```java
src/com/google/javascript/jscomp/CommandLineRunner.java: 862
        options.messageBundle = new EmptyMessageBundle();
+       options.messageBundle = null;
+   else {
+       options.messageBundle = null;
    }
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 3 locations
```java
src/com/google/javascript/jscomp/CommandLineRunner.java: 862
Three locations were inserted in front of Location 862.
```

#### III. Explanation
Its reason is the same as the reason in the 78th patch.
<br><br>

### 4.3. 714th patch - T2F
#### I. Fixed Result
```java
src/com/google/javascript/jscomp/CommandLineRunner.java: 852-862
-   } else if (CompilationLevel.ADVANCED_OPTIMIZATIONS == level) {
        // In SIMPLE or WHITESPACE mode, if the user hasn't specified a
        // translations file, they might reasonably try to write their own
        // implementation of goog.getMsg that makes the substitution at
        // run-time.
        //
        // In ADVANCED mode, goog.getMsg is going to be renamed anyway,
        // so we might as well inline it. But shut off the i18n warnings,
        // because the user didn't really ask for i18n.
-       options.messageBundle = new EmptyMessageBundle();
    }
```
* Locations 853-860 are not comment locations related to "FAULT_OF_OMISSION." 

#### II. Fixed chunks and locations 
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 2 locations
```java
src/com/google/javascript/jscomp/CommandLineRunner.java: 852
}

src/com/google/javascript/jscomp/CommandLineRunner.java: 861-862
Location 861 was deleted.
Location 862 was deleted.
```

#### III. Explanation
Its reason is the same as the reason in the 78th patch.
<br><br>