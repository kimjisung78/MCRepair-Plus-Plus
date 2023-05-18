# Time 17
* <h4>Bug type: Type 3 (T3B / T2F)</h4>
* <h4>The number of chunks: 2 chunks (2 used chunks / 1 fixed chunk)</h4>
* <h4>The number of locations: 5 locations (5 used locations / 2 fixed locations)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
src/main/java/org/joda/time/DateTimeZone.java: 1167-1179
-   long instantBefore = convertUTCToLocal(instant - 3 * DateTimeConstants.MILLIS_PER_HOUR);
+   long instantBefore = instant - 3 * DateTimeConstants.MILLIS_PER_HOUR;
-   long instantAfter = convertUTCToLocal(instant + 3 * DateTimeConstants.MILLIS_PER_HOUR);
+   long instantAfter = instant + 3 * DateTimeConstants.MILLIS_PER_HOUR;
+   long offsetBefore = getOffset(instantBefore);
+   long offsetAfter = getOffset(instantAfter);
-   if (instantBefore == instantAfter) {
+   if (offsetBefore <= offsetAfter) {
        return instant;  // not an overlap (less than is a gap, equal is normal case)
    }

    // work out range of instants that have duplicate local times
+   long diff = offsetBefore - offsetAfter;
-   long local = convertUTCToLocal(instant);
+   long transition = nextTransition(instantBefore);
+   long overlapStart = transition - diff;
+   long overlapEnd = transition + diff;
-   return convertLocalToUTC(local, false, earlierOrLater ? instantAfter : instantBefore);
+   if (instant < overlapStart || instant >= overlapEnd) {
+       return instant;  // not an overlap
+   }

    // calculate result
+   long afterStart = instant - overlapStart;
+   if (afterStart >= diff) {
        // currently in later offset
+       return earlierOrLater ? instant : instant - diff;
+   } else {
        // currently in earlier offset
+       return earlierOrLater ? instant + diff : instant;
+   }
```
<br>

## 2. Used chunks and locations - T3B
* The number of used chunks: 2 chunks
* The number of used locations: 5 locations
```java
src/main/java/org/joda/time/DateTimeZone.java: 1167-1169
long instantBefore = convertUTCToLocal(instant - 3 * DateTimeConstants.MILLIS_PER_HOUR);
long instantAfter = convertUTCToLocal(instant + 3 * DateTimeConstants.MILLIS_PER_HOUR);
if (instantBefore == instantAfter) {
```

```java
src/main/java/org/joda/time/DateTimeZone.java: 1174-1175
long local = convertUTCToLocal(instant);
return convertLocalToUTC(local, false, earlierOrLater ? instantAfter : instantBefore);
```
<br>

## 3. Correct combined patches per bug type
* The number of correct combined patches: 2
    * T2F (2): 206, 382
<br><br>

## 4. Examples of correct patches
### 4.1. 206th patch - T2F
#### I. Fixed Result
```java
src/main/java/org/joda/time/DateTimeZone.java: 1167-1169
-   long instantBefore = convertUTCToLocal(instant - 3 * DateTimeConstants.MILLIS_PER_HOUR);
+   long instantBefore = (instant - 3 * DateTimeConstants.MILLIS_PER_HOUR);
-   long instantAfter = convertUTCToLocal(instant + 3 * DateTimeConstants.MILLIS_PER_HOUR);
+   long instantAfter = (instant + 3 * DateTimeConstants.MILLIS_PER_HOUR);
    if (instantBefore == instantAfter) {
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 2 locations
```java
src/main/java/org/joda/time/DateTimeZone.java: 1167-1168
long instantBefore = (instant - 3 * DateTimeConstants.MILLIS_PER_HOUR);
long instantAfter = (instant + 3 * DateTimeConstants.MILLIS_PER_HOUR);
```

#### III. Explanation
To fix the bug, its source code should be changed that it compares two instants wihtout ```convertUTCToLocal``` method.
<br><br>
