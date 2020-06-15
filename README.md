# Clean-Code
A Handbook of Agile Software Craftsmanship

## Chapter2: Meaningful Names

### Use Intention-Revealing Names
The name should tell you why it exist, what it does, and how it is used.

**bad code**:
```java
int d; // elapsed time in days
```

We should choose a name that specifies what is being mesured and the unit of that measurement.

**good code**:
```java
int elapsedTimeInDays;
int daysSinceCreation;
int daysSinceModification;
int fileAgeInDays;
```

Choosing names that reveal intent can make it much easier to understand and change code.

**bad code**:
```java
public List<int[]> getThem() {
    List<int[]> list1 = new ArrayList<int[]>();
    for (int[] x : theList)
        if (x[0] == 4)
            list1.add(x);
    return list1;
}
```

The code implicitly requires that we know the answers to questions such as:
1. What kinds of things are in `theList`?
2. What is the significance of the zeroth subscript of an item in `theList`?
3. What is the significance of the value `4`?
4. How would I use the list being returned?

Say that we're working in a mine sweeper game. We find that the board is list of cells called `theList`. Let's rename that to `gameBoard`.

Each cell on the board is represented by a simple array. We further find that the zeroth subscript is the location of a status value and that a status value of 4 means "flagged".

**good code**:
```java
public List<int[]> getFlaggedCells() {
    List<int[]> flaggedCells = new ArrayList<int[]>();
    for (int[] cell : gameBoard)
        if (cell[STATUS_VALUE] == FLAGGED)
            flaggedCells.add(cell);
    return flaggedCells;
}
```

We can go further and write a simple class for cells instead of using an array of `int`s. It can include an intention-revealing function (call it `isFlagged`) to hide the magic numbers.

**good code**:
```java
public List<Cell> getFlaggedCells() {
    List<Cell> flaggedCells = new ArrayList<Cell>();
    for (Cell cell : gameBoard)
        if (cell.isFlagged())
            flaggedCells.add(cell);
    return flaggedCells;
}
```

### Avoid Disinformation
Do not refer to a grouping of accounts as an `accountList` unless it's actually a `List`. If the container holding the accounts is not actually a `List`, it may lead to false conclusions. So `accountGroup` or `bunchOfAccounts` or just plain `accounts` would be better.

Beware of using names which vary in small ways for example `XYZControllerForEfficientHandlerOfStrings` and `XYZControllerForEfficientStorageOfStrings`.

A truly awful example of disinformative names would be the use of lower-case `L` or uppercase `O` as variable names, especialy in combination. The problem, of course, is that they look almost entirely like the constants one and zero.

**bad code**:
```java
int a = 1;
if (O == 1)
    a = O1;
else
    l = 01;
```

### Make Meaningful Distinctions
It is not sufficient to add number series or noise words, even though the compiler is satisfied. If names must be different, then they should also mean something different.

Consider, for example, the truly hideous practice of creating a variable named `klass` just because the name `class` was used for something else.

Number-series naming `(a1, a2, .. aN)` is the opposite of intentional naming.

**bad code**:
```java
public static void copyChars(char[] a1, char[] a2) {
    for (int i = 0; i < a1.length; i++)
        a2[i] = a1[i];
}
```

This function reads much better when `source` and `destination` are used for the argument names.

Noise words are another meaningless distinction. Imagine that you have a `Product` class. If you have another called `ProductInfo` or `ProductData`, you have made names different without making them mean anything different. `Info` and `Data` are indistinct noise words like `a`, `an`, and `the`.

Noise words are redundant. The word `variable` should never appear in a variable name. The word `table` should never appear in a table name.

**bad code**:
```java
getActiveAccount();
getActiveAccounts();
getActiveAccountInfo();
```

How are the programmers in this project supposed to know which of these functions to call.

### Use Pronounceable Names
If you can't pronounce it, you can't discuss it without sounding like an idiot.

**bad code**:
```java
class DtaRcrd102 {
    private Date genymdhms; // generation date, year, month, day, hour, minute and second
    private Date modymdhms;
    private final String pszqint = "102";
}
```

**good code**:
```java
class Customer {
    private Date generationTimestamp;
    private Date modificationTimestamp;
    private final String recordId = "102";
}
```

### Use Searchable Names
