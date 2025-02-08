# Number Container System

## Problem Description

The task is to design a **Number Container System** that can store numbers at specific indices and allow for inserting or replacing numbers at these indices. Additionally, the system should allow you to retrieve the smallest index for a given number.

### Functionalities:

1. **`change(int index, int number)`**: This function will fill the container at the given index with the given number. If there is already a number at that index, it will replace it with the new number.

2. **`find(int number)`**: This function will return the smallest index that is filled with the given number. If there is no index filled with that number, return -1.

### Example Walkthrough

Consider the following sequence of operations:

```plaintext
["NumberContainers", "find", "change", "change", "change", "change", "find", "change", "find"]
[[], [10], [2, 10], [1, 10], [3, 10], [5, 10], [10], [1, 20], [10]]
