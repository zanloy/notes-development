---
id: bnKl1IekzOkowI5Iwpmdm
title: Chunk Array Into Even Sized Chunks
desc: ''
updated: 1641230104234
created: 1641230047211
---
This snippet will break a list/array into n (evenly sized) chunks.

```python
import math

def chunk_n_times(lst, n):
    per_chunk = math.ceil(len(lst)/n)

    for x in range(0, len(lst), per_chunk):
        next_chunk = lst[x:per_chunk+x]

        if len(next_chunk) < per_chunk:
            next_chunk = next_chunk + [None for y in range(per_chunk-len(next_chunk))]
        yield next_chunk

print(list(chunk_n_times([1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13], 7)))
```