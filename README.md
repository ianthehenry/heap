# heap

This is a pure-Janet implementation of a min-max heap that uses a custom comparator function to order elements.

Quick example, using [`cmp`](https://github.com/ianthehenry/cmp) as a convenient way to construct comparator functions.

```janet
(import heap)
(use cmp/import)

(def users (heap/new (by :score)))

(heap/push users {:name "Ian" :score 20})
(heap/push users {:name "Johnny" :score 15})

(heap/peek-min users)
# {:name "Johnny" :score 15}

(heap/pop-max users)
# {:name "Ian" :score 20}

(heap/pop-max users)
# {:name "Johnny" :score 15}
```

API:

```janet
# create a heap (constant time)
(heap/new cmp)

# add values to the heap (log time)
(heap/push heap value)

# inspect values (constant time)
#   raises if the heap is empty, unless
#   you supply a default value
(heap/peek-min heap &opt default)
(heap/peek-max heap &opt default)

# remove and return values (log time)
#   raises if the heap is empty, unless
#   you supply a default value
(heap/pop-min heap &opt default)
(heap/pop-max heap &opt default)

# constant time
#   Note! The native versions of these functions
#   will give the wrong answers
(heap/length heap)
(heap/empty? heap)

# linear time
(heap/contains? heap value)
```

The implementation makes no guarantees about pop order for elements that compare identically (it does not try to enforce FIFO or LIFO ordering).
