# Chart 1
* <h4>Bug type: Type 3 (T1B / T1F, T2F, T3F)</h4>
* <h4>The number of chunks: 2 chunks (1 used chunk / 1, 2 fixed chunks)</h4>
* <h4>The number of locations: 2 locations (1 used location / 1, 2 fixed locations)</h4>
<br>

## 1. Developer's patch
* `-`: A fixed and deleted location
* `+`: A fixed and added location
```java
source/org/jfree/chart/renderer/category/AbstractCategoryItemRenderer.java: 1796-1799
    CategoryDataset dataset = this.plot.getDataset(index);
-   if (dataset != null) {
+   if (dataset == null) {
        return result;
    }
```
<br>

## 2. Used chunks and locations - T1B
* The number of used chunks: 1 chunk
* The number of used locations: 1 location
```java
source/org/jfree/chart/renderer/category/AbstractCategoryItemRenderer.java: 1797
if (dataset != null) {
```
<br>

## 3. Correct combined patches per fixed bug type
* The number of correct combined patches: 11
    * T1F (9): 56, 121, 130, 229, 323, 324, 333, 672, 705
    * T2F (1): 743
    * T3F (1): 747
<br><br>

## 4. Examples of correct patches
### 4.1. 56th patch - T1F
#### I. Fixed Result
```java
source/org/jfree/chart/renderer/category/AbstractCategoryItemRenderer.java: 1797
-   if (dataset != null) {
+   if (dataset == null) {
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 1 location
```java
source/org/jfree/chart/renderer/category/AbstractCategoryItemRenderer.java: 1797
if (dataset == null) {
```
<br>

### 4.3. 743rd patch - T2F
#### I. Fixed Result
```java
source/org/jfree/chart/renderer/category/AbstractCategoryItemRenderer.java: 1797-1799
-   if (dataset != null) {
+   if (dataset == null) {
-       return result;
+       return null;
    }
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 1 chunk
* The number of fixed locations: 2 locations
```java
source/org/jfree/chart/renderer/category/AbstractCategoryItemRenderer.java: 1797-1798
if (dataset == null) {
    return null;
```
<br><br>

### 4.2. 747th patch - T3F
#### I. Fixed Result
```java
source/org/jfree/chart/renderer/category/AbstractCategoryItemRenderer.java: 1797-1799
-   if (dataset != null) {
+   if (dataset == null) {
        return result;
-   }
```

#### II. Fixed chunks and locations
* The number of fixed chunks: 2 chunks
* The number of fixed locations: 2 locations
```java
source/org/jfree/chart/renderer/category/AbstractCategoryItemRenderer.java: 1797
if (dataset == null)
```

```java
source/org/jfree/chart/renderer/category/AbstractCategoryItemRenderer.java: 1799
Location 1799 was deleted.
```
<br>