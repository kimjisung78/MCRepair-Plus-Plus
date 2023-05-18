# Lang 51
* <h4>Bug type: Type 2 (T1B / T1F, T2F)</h4>
* <h4>The number of chunks: 1 chunk (1 used chunk / 1 fixed chunk)</h4>
* <h4>The number of locations: 3 locations (1 used location / 1, 3 fixed locations)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/java/org/apache/commons/lang/BooleanUtils.java: 670-684
    case 3: {
        char ch = str.charAt(0);
        if (ch == 'y') {
            return 
                (str.charAt(1) == 'e' || str.charAt(1) == 'E') &&
                (str.charAt(2) == 's' || str.charAt(2) == 'S');
        }
        if (ch == 'Y') {
            return 
                (str.charAt(1) == 'E' || str.charAt(1) == 'e') &&
                (str.charAt(2) == 'S' || str.charAt(2) == 's');
        }
+       return false;
    }
    case 4: {            
        char ch = str.charAt(0);
```
<br>

## 2. Used chunks and locations - T1B
* The number of used chunks: 1 chunk
* The number of used locations: 1 location
```java
src/java/org/apache/commons/lang/BooleanUtils.java: 682
FAULT_OF_OMISSION
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 4
    * T1F (2): 14, 18
    * T2F (2): 4, 21
<br><br>

## 4. Examples of correct patches
### 4.1. 4th patch - T2F
#### I. Fixed Result
```java
src/java/org/apache/commons/lang/BooleanUtils.java: 681
-   }
+   } else {
+       break;
+   }
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 3 locations
```java
src/java/org/apache/commons/lang/BooleanUtils.java: 681
} else {
    break;
}
```

#### Explanation
To fix the bug, its source code must changed that it prevents the fall through problem about ```case 3```. Also, ```if (ch == 'Y')``` statement occurs the problem. The patch prevented the fall through problem.
<br><br>

### 4.2. 14th patch - T1F
#### I. Fixed Result
```java
src/java/org/apache/commons/lang/BooleanUtils.java: 682
+   break;
    }
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/java/org/apache/commons/lang/BooleanUtils.java: 682
A location was inserted in front of Location 682.
```

#### Explanation
To fix the bug, its source code must changed that it prevents the fall through problem about ```case 3```. The patch prevented the fall through problem.
<br><br>

### 4.3. 18th patch - T1F
#### I. Fixed Result
```java
src/java/org/apache/commons/lang/BooleanUtils.java: 682
+   return false;
    }
```

#### II. Fixed chunks and locations 
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/java/org/apache/commons/lang/BooleanUtils.java: 682
A location was inserted in front of Location 682.
```
<br><br>

### 4.4. 21st patch - T2F
#### I. Fixed Result
```java
src/java/org/apache/commons/lang/BooleanUtils.java: 681
-   }
+   } else {
+       return false;
+   }
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 3 locations
```java
src/java/org/apache/commons/lang/BooleanUtils.java: 681
} else {
    return false;
}
```

#### Explanation
Its reason is the same as the reason in the 4th patch.
<br><br>