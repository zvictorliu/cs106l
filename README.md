---
description: A brief intro to this course
---

# Introduction

Why I am doing this? I just think I should improve my cpp skills, learning more than cin cout staff. Perhaps it won't help right now. However, oneday it may enable me to adapt to a new area efficiently, who knows.

So this course leaves a goal that understanding why these are differenct and the second is better.

```cpp
double GetAverage(double arr[], int numElems) {
 double total = 0.0;
 for(int h = 0; h < numElems; ++h)
 total += arr[h] / numElems;
 
 return total;
 }
```

```cpp
template <typename ForwardIterator>
 double GetAverage(ForwardIterator begin, ForwardIterator end) {
 return accumulate(begin, end, 0.0) / distance(begin, end);
 }
```

So let's roll!
