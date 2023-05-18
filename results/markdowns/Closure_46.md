# Closure 46
* <h4>Bug type: Type 3 (T2B / T1F, T2F, T3F)</h4>
* <h4>The number of chunks: 3 chunks (1 used chunk / 1, 2, 3 fixed chunks)</h4>
* <h4>The number of locations: 13 locations (13 used locations / 1, 7, 8, 9, 10, 13 fixed locations)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/com/google/javascript/rhino/jstype/RecordType.java: 140-155
-   @Override
-   public JSType getLeastSupertype(JSType that) {
-       if (!that.isRecordType()) {
-           return super.getLeastSupertype(that);            
-       }
-       RecordTypeBuilder builder = new RecordTypeBuilder(registry);
-       for (String property : properties.keySet()) {
-           if (that.toMaybeRecordType().hasProperty(property) && 
-                   that.toMaybeRecordType().getPropertyType(property).isEquivalentTo(
-                   getPropertyType(property))) {
-               builder.addProperty(property, getPropertyType(property),
-                   getPropertyNode(property));
-           }
-       }
-       return builder.build();
-   }
```
<br>

## 2. Used chunks and locations - T2B
* The number of used chunks: 1 chunk
* The number of used locations: 13 locations
```java
src/com/google/javascript/rhino/jstype/RecordType.java: 140-155
(Locations 147-149 and 150-151 are divided.)
@Override
public JSType getLeastSupertype(JSType that) {
    if (!that.isRecordType()) {
        return super.getLeastSupertype(that);            
    }
    RecordTypeBuilder builder = new RecordTypeBuilder(registry);
    for (String property : properties.keySet()) {
        if (that.toMaybeRecordType().hasProperty(property) && that.toMaybeRecordType().getPropertyType(property).isEquivalentTo(getPropertyTy(property))) {
            builder.addProperty(property, getPropertyType(property), getPropertyNode(property));
        }
    }
    return builder.build();
}
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 9
    * T1F (1): 698
    * T2F (4): 836, 838, 846, 847
    * T3F (4): 833, 840, 842, 843
<br><br>

## 4. Examples of correct patches
### 4.1. 698th patch - T1F
#### I. Fixed Result
```java
src/com/google/javascript/rhino/jstype/RecordType.java: 140-144
    @Override
    public JSType getLeastSupertype(JSType that) {
-       if (!that.isRecordType()) {
+       if (isRecordType()) {
            return super.getLeastSupertype(that);            
        }
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
src/com/google/javascript/rhino/jstype/RecordType.java: 142
if (isRecordType()) {
```

#### III. Explanation
To only return ```super.getLeastSupertype(that)``` in ```public JSType getLeastSupertype(JSType that)``` is equivalent to the deletion of the method.
<br><br>

### 4.2. 833rd patch - T3F
#### I. Fixed Result
```java
src/com/google/javascript/rhino/jstype/RecordType.java: 140-155
-   @Override
    public JSType getLeastSupertype(JSType that) {
-       if (!that.isRecordType()) {
            return super.getLeastSupertype(that);            
-       }
-       RecordTypeBuilder builder = new RecordTypeBuilder(registry);
-       for (String property : properties.keySet()) {
-           if (that.toMaybeRecordType().hasProperty(property) && that.toMaybeRecordType().getPropertyType(property).isEquivalentTo(getPropertyTy(property))) {
-               builder.addProperty(property, getPropertyType(property), getPropertyNode(property));
-           }
-       }
-       return builder.build();
    }
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 3 chunks
* The number of fixed locations: 10 locations
```java
src/com/google/javascript/rhino/jstype/RecordType.java: 140
Location 140 was deleted.
```

```java
src/com/google/javascript/rhino/jstype/RecordType.java: 142
Location 142 was deleted.
```

```java
src/com/google/javascript/rhino/jstype/RecordType.java: 144-154
(Locations 147-149 and 150-151 are divided.)
Location 144 was deleted.
Location 145 was deleted.
Location 146 was deleted.
Divided Locations 147-149 were deleted.
Divided Locations 150-151 were deleted.
Location 152 was deleted.
Location 153 was deleted.
Location 154 was deleted.
```

#### III. Explanation
Its reason is the same as the reason in the 698th patch.
<br><br>

### 4.3. 840th patch - T3F
#### I. Fixed Result
```java
src/com/google/javascript/rhino/jstype/RecordType.java: 140-155
    @Override
    public JSType getLeastSupertype(JSType that) {
-       if (!that.isRecordType()) {
            return super.getLeastSupertype(that);            
-       }
-       RecordTypeBuilder builder = new RecordTypeBuilder(registry);
-       for (String property : properties.keySet()) {
-           if (that.toMaybeRecordType().hasProperty(property) && that.toMaybeRecordType().getPropertyType(property).isEquivalentTo(getPropertyTy(property))) {
-               builder.addProperty(property, getPropertyType(property), getPropertyNode(property));
-           }
-       }
-       return builder.build();
    }
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 2 chunks
* The number of fixed locations: 9 locations
```java
src/com/google/javascript/rhino/jstype/RecordType.java: 142
Location 142 was deleted.
```

```java
src/com/google/javascript/rhino/jstype/RecordType.java: 144-154
(Locations 147-149 and 150-151 are divided.)
Location 144 was deleted.
Location 145 was deleted.
Location 146 was deleted.
Divided Locations 147-149 were deleted.
Divided Locations 150-151 were deleted.
Location 152 was deleted.
Location 153 was deleted.
Location 154 was deleted.
```

#### III. Explanation
Its reason is the same as the reason in the 698th patch.
<br><br>

### 4.4. 846th patch - T2F
#### I. Fixed Result
```java
src/com/google/javascript/rhino/jstype/RecordType.java: 140-155
-   @Override
-   public JSType getLeastSupertype(JSType that) {
-       if (!that.isRecordType()) {
-           return super.getLeastSupertype(that);            
-       }
-       RecordTypeBuilder builder = new RecordTypeBuilder(registry);
-       for (String property : properties.keySet()) {
-           if (that.toMaybeRecordType().hasProperty(property) && that.toMaybeRecordType().getPropertyType(property).isEquivalentTo(getPropertyTy(property))) {
-               builder.addProperty(property, getPropertyType(property), getPropertyNode(property));
-           }
-       }
-       return builder.build();
-   }
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 13 locations
```java
src/com/google/javascript/rhino/jstype/RecordType.java: 140-155
(Locations 147-149 and 150-151 are divided.)
Location 140 was deleted.
Location 141 was deleted.
Location 142 was deleted.
Location 143 was deleted.
Location 144 was deleted.
Location 145 was deleted.
Location 146 was deleted.
Divided Locations 147-149 were deleted.
Divided Locations 150-151 were deleted.
Location 152 was deleted.
Location 153 was deleted.
Location 154 was deleted.
Location 155 was deleted.
```
<br><br>