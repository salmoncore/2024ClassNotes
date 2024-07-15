<< [README](./README.md)

# ArraysLists

## Contents
- [Overview](#overview)
- [See Also](#see-also)

# Overview

- Dynamic array, grows as you add more data to it
- Doesn't shrink dynamically
- Use trimToSize() method
- Default starting capacity is 10
- Grows by 50% if capacity is reached
- Lookup is O(1) with the index
- Insertion (with no resizing) is O(1) at the beginning and end of the array
- Insertion with resizing or insertion within the list is O(n)

## See Also
- [Arrays](./Arrays.md)