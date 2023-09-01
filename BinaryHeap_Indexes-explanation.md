## Binary Heap 
In ***Binary Heap*** data structure we often use an ***array*** as backed storage.<br>In this case no any links present between the nodes.<br>
However we can imagine a Heap as a ***tree***, to get a simple and clearer picture of what is going on between the elements.

Assume we have ***[1 - N]*** elements in out data structure.<br>
Element with index ***1*** is the ***root*** and parent of all nodes. 

Main operations are following:
1. To get the ***left child*** index: `int child = parent * 2;`
2. To get the ***right child*** index: `int child = leftChild++;`
2. To get the ***parent*** index: `int parent = child / 2`;

### Bounds:
- `parent >= 1` - the 1st node is the  ***root***;
- `leftChild <= N` - the ***last child***

#### Keep in mind:
Usually array indexes are in the range ***[0 : array.length - 1]***.<br>
It's tricky, cause in this case we can't use mentioned above formulas.<br>
Assume you need to get a left child of the root:
```java
int root = 0;
int leftChild = root * 2;

leftChild == 0, which is incorrect (should be 1)
```

Same is with getting a parent of a rightChild:
```java
int rightChild = 8;
	int parent = 8 / 2 	
parent == 4, which is incorrect (should be 3)
```
BE CAREFULL

***ADD A PICTURE WITH 2 TREES WITH INDEXES AND CLEAR EXPLANATION OF WHY INDEXES ARE TO BE SHIFTED***
To deal with array starting from index 0, there could be several approaches:
1. Calculate Nodes in following way:
```
int leftChild = (parent + 1) * 2 - 1;
int parent = (child + 1) / 2 - 1;
```
Looks quite tricky comparing to how simple is the approach with indexes starting from 1.
2. Convert an array to a new one with `length == oldArray.length + 1`. Copy all nodes from the old array to the new one with starting index ***1***.<br>
```java
Comparable[] newArray = new Comparable[oldArray.length + 1];
System.arraycopy(oldArray, 0, newArray, 1, oldArray.length);

```
This approach is great, however cons are, that
- We need to copy original array in any case
- In every method we have to be aware, that the amount of elements is `newArray.length - 1`, and we don't use ***index 0***
3. _Sedgewick's_ approach, which he uses in his Princeton "Algorithms Part 1" course. The idea is, that we can 
- pass an array with usual indexes `[0 : array.length - 1]`. 
- Every function, aka `sink(int parent)` and `swim(int child)`, uses shifted indexes as arguments. The trick is to have `less()` and `exch()` methods which shifts indexes one step back before _compare_ and _exchange_ operations.<br>
This looks following:
```java
private static void boolean less(Comparable[] arr, int i, int j) {
	return arr[i - 1].compareTo(arr[j - 1]);
}

private static void exch(Comparable[] arr, int i, int j) {
	Comparable[] swp = arr[i - 1];
	arr[i - 1] = arr[j - 1];
	arr[j - 1] = arr[i - 1];
}
```
The main con is, that you need to be aware of this implicit shift.
And if you are not involved in the process, it is hard to understand, why this shift happens at all, in my opinion. Otherwise the solution is great.

Two main methods are:
- `sink(int parent)` - compares a parent with a ***greatest*** child. Exchanges nodes `if (greatestChild > parent)`
- `swim(int child)` - compares a child with a parent

### Move this code. This is just temporary snippet:
Assume we have an ***int[] array*** with ***[size = 20]***, filled with data:
```java
int[] array = new Random().ints(20, 0, 10).toArray();
```
***Task:*** Copy data from indexes ***[4 : 13]*** to new array of ***[size = 10]***

***Simple solution:***
```java
int start = 4, end = 13;
int newSize = end - start + 1;
int[] newArray = new int[newSize];
```
- ***java.lang.**** package have a great one-linear:<br>

`System.arraycopy(array, 0, newArray, 0, array.length);`

- Manual approach would be:
```java
for (int i = start, i < newSize; i++) {
	newArray[i - start] = array[i];
}
```

### Generate random Integer[] array:
```java
Integer[] randomNumbers = new Random()
                .ints(10, 0, 20)
                .boxed()
                .toArray(Integer[]::new);
```

### Generate int[] array of 10 random unique numbers:
```java
int[] uniqueNumbers = new Random()
                .ints(1, 11).distinct().limit(10)
                .toArray();			
```

