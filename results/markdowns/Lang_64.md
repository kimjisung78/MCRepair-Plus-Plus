# Lang 64
* <h4>Bug type: Type 3 (T3B / T1F)</h4>
* <h4>The number of chunks: 2 chunks (2 used chunks / 1 fixed chunk)</h4>
* <h4>The number of locations: 2 locations (2 used locations / 1 fixed location)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/java/org/apache/commons/lang/enums/ValuedEnum.java: 182-184
    public int compareTo(Object other) {            
+       if (other == this) {            
+           return 0;            
+       }            
+       if (other.getClass() != this.getClass()) {            
+           if (other.getClass().getName().equals(this.getClass().getName())) {            
+               return iValue - getValueInOtherClassLoader(other);            
+           }            
+           throw new ClassCastException(            
+               "Different enum class '" + ClassUtils.getShortClassName(other.getClass()) + "'");            
+       }            
        return iValue - ((ValuedEnum) other).iValue;            
    }
```

```java
src/java/org/apache/commons/lang/enums/ValuedEnum.java: 189-196
    * @param other  the object to determine the value for
    * @return the value
    */
+   private int getValueInOtherClassLoader(Object other) {
+       try {
+           Method mth = other.getClass().getMethod("getValue", null);
+           Integer value = (Integer) mth.invoke(other, null);
+           return value.intValue();
+       } catch (NoSuchMethodException e) {
            // ignore - should never happen
+       } catch (IllegalAccessException e) {
            // ignore - should never happen
+       } catch (InvocationTargetException e) {
            // ignore - should never happen
+       }
+       throw new IllegalStateException("This should not happen");
+   }

    /**
```
<br>

## 2. Used chunks and locations - T3B
* The number of used chunks: 2 chunks
* The number of used locations: 2 locations
```java
src/java/org/apache/commons/lang/enums/ValuedEnum.java: 183
FAULT_OF_OMISSION
```

```java
src/java/org/apache/commons/lang/enums/ValuedEnum.java: 195
FAULT_OF_OMISSION
```
* Location 195 is a blank location related to "FAULT_OF_OMISSION". 
<br><br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 1
    * T1F (1): 187
<br><br>

## 4. Examples of correct patches
### 4.1. 187th patch - T1F
#### I. Fixed Result
```java
src/java/org/apache/commons/lang/enums/ValuedEnum.java: 183
+   super.compareTo(other);
    return iValue - ((ValuedEnum) other).iValue;
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/java/org/apache/commons/lang/enums/ValuedEnum.java: 183
A location was inserted in front of Location 183.
```

#### III. Explanation
To fix the bug, its source code must check ```Object other``` argument. Also, ```super.compareTo(other)``` method (```compareTo(other)``` method in ```Enum``` abstract class) already checks the argument the same as its developer's patch as follows:
```java
public int compareTo(Object other) {
    if (other == this) {
        return 0;
    }
    if (other.getClass() != this.getClass()) {
        if (other.getClass().getName().equals(this.getClass().getName())) {
            return iName.compareTo(getNameInOtherClassLoader(other));
        }
    }
    return iName.compareTo(((Enum) other).iName);
}
```
<br><br>