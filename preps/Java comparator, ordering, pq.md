## Object.compareTo()

## Comparator
[Java 8 doc](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html)
Usage
* be passed to a sort method (such as Collections.sort or Arrays.sort) to allow precise control over the sort order
* be used to control the order of certain data structures (such as sorted sets or sorted maps)
* to provide an ordering for collections of objects that don't have a natural ordering.


For numbers, `a - b` gives the nature order, same as `a.compareTo(b)`
* -1: a less than
* 0 : a equal
* 1: a greater than

Caution should be exercised when using a comparator capable of imposing an ordering inconsistent with equals to order a sorted set (or sorted map).


### Common usages
Used in collection/array sort
initialize sorted data structure: 
* `PriorityQueue(Comparator<? super E> comparator)`, `PriorityQueue(int initialCapacity, Comparator<? super E> comparator)`
* `TreeMap(Comparator<? super K> comparator)`
* `TreeSet(Comparator<? super E> comparator)`

### Templates
#### Inline Style with Anonymous Class 
```
Arrays.sort(arr, new Comparator<E>() {
    public int compare(E e1, E e2) {
        return e1.val - e2.val;
    }
})

Collections.sort(...)

```
#### 

```
public class SortByErrorComparator implements Comparator<WorkflowError> {
    public int compare(WorkflowError obj1, WorkflowError obj2) {
        return obj1.getErrorCode().compareTo(obj2.getErrorCode());
    }
}
Collections.sort(list, new SortByErrorComparator()) ;

```
#### Lambda function
```
Collections.sort(list, (a, b) -> a.getErrorCode().compareTo(b.getErrorCode()));
```

#### Functional programming
list.sort(Comparator.comparing(WorkflowError::getErrorCode))

```
PriorityQueue<E> pq = new PriorityQueue<E>(initialCap, new )
```
## PQ
order direction!!!

