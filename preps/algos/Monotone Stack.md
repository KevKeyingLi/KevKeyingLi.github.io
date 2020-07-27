https://www.youtube.com/watch?v=QqJ7xtuy2z8
Basic template:

//Increasing stack, nums[] 
```
for (int i = 0; i < n; i++) {
    while (!s.isEmpty() && nums[s.peek()] > nums[i]) {
        s.pop();
    }
    s.push(i);
}
```
Here, we compare the numbers, but store the index, thus, we not only know what are numbers in the stack, but also their indexes.

^ This looks simple, but what can it do?
1. information about stack top(current): 
    - the first number on the right that is less than current(l): this is when stack top gets popped
    - first number on the left of current, that is less(r): the next element in stack.
    - With previous two: we can find a subarray that current is the largest(r - l)
2. newly added number
    - to the left, first larger number: the one get popped first
    - to the left, the number that is larger but closest to current: the last one that get popped
    - to the left, continuously numbers that is larger then current. 


Problems we can solve
* first one on the left/right...
* a subarray that the current is the min/max
