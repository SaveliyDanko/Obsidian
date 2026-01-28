#java 

---
![[Pasted image 20250602133135.png]]
A container for data of a specific primitive type.
A buffer is a linear, finite sequence of elements of a specific primitive type. Aside from its content, the essential properties of a buffer are its capacity, limit, and position:
- A buffer's _capacity_ is the number of elements it contains. The capacity of a buffer is never negative and never changes.
- A buffer's _limit_ is the index of the first element that should not be read or written. A buffer's limit is never negative and is never greater than its capacity.
- A buffer's _position_ is the index of the next element to be read or written. A buffer's position is never negative and is never greater than its limit.

#### Transferring data 
Each subclass of this class defines two categories of _get_ and _put_ operations:
- _Relative_ operations read or write one or more elements starting at the current position and then increment the position by the number of elements transferred.
- _Absolute_ operations take an explicit element index and do not affect the position.

A buffer's _mark_ is the index to which its position will be reset when the `reset` method is invoked. The mark is not always defined, but when it is defined it is never negative and is never greater than the position. If the mark is defined then it is discarded when the position or the limit is adjusted to a value smaller than the mark.

#### Invariants
The following invariant holds for the mark, position, limit, and capacity values:
$0 \leq mark \leq position \leq limit \leq capacity$

A newly-created buffer always has a position of zero and a mark that is undefined. The initial limit may be zero, or it may be some other value that depends upon the type of the buffer and the manner in which it is constructed. Each element of a newly-allocated buffer is initialized to zero.

#### Additional operations
In addition to methods for accessing the position, limit, and capacity values and for marking and resetting, this class also defines the following operations upon buffers:
- `clear()` makes a buffer ready for a new sequence of channel-read or relative put operations: It sets the limit to the capacity and the position to zero.
- `flip()` makes a buffer ready for a new sequence of channel-write or relative get operations: It sets the limit to the current position and then sets the position to zero.
- `rewind()` makes a buffer ready for re-reading the data that it already contains: It leaves the limit unchanged and sets the position to zero.
- The `slice()` and `slice(index,length)` methods create a subsequence of a buffer: They leave the limit and the position unchanged.
- `duplicate()` creates a shallow copy of a buffer: It leaves the limit and the position unchanged.

#### Read-only buffers
Every buffer is readable, but not every buffer is writable. Whether or not a buffer is read-only may be determined by invoking its `isReadOnly` method.

#### No-Thread safety
Buffers are not safe for use by multiple concurrent threads. If a buffer is to be used by more than one thread then access to the buffer should be controlled by appropriate synchronization.