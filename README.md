# week-2-Linked-List-assignment-CSI
singly linked list using Object-Oriented Programming (OOP) principles. 
Implementation includes the following: A Node class to represent each node in the list. A LinkedList class to manage the nodes, with methods to: Add a node to the end of the list Print the list Delete the nth node (where n is a 1-based index) Include exception handling to manage edge cases such as: Deleting a node from an empty list Deleting a node with an index out of range Test your implementation with at least one sample list.

## Output

![linked list](https://github.com/user-attachments/assets/1e8d607b-990d-4e3a-a742-2f20de057426)

# Singly Linked List Implementation

A Python implementation of a singly linked list using Object-Oriented Programming (OOP) principles with comprehensive exception handling.

## Features

- **Node Class**: Represents individual nodes in the linked list
- **LinkedList Class**: Manages the nodes with essential operations
- **Exception Handling**: Handles edge cases like empty list operations and out-of-range indices
- **1-based Indexing**: User-friendly indexing starting from 1
- **Comprehensive Testing**: Includes test cases for all functionality

## Code Implementation

```python
class Node:
    """
    A class to represent a single node in the linked list.
    """
    def __init__(self, data):
        """
        Initialize a node with data and next pointer set to None.

        Args:
            data: The data to store in the node
        """
        self.data = data
        self.next = None


class LinkedListError(Exception):
    """Custom exception class for LinkedList operations."""
    pass


class LinkedList:
    """
    A class to implement a singly linked list with basic operations.
    """

    def __init__(self):
        """Initialize an empty linked list."""
        self.head = None
        self.size = 0

    def add(self, data):
        """
        Add a new node with the given data to the end of the list.

        Args:
            data: The data to add to the list
        """
        new_node = Node(data)

        # If list is empty, make new node the head
        if not self.head:
            self.head = new_node
        else:
            # Traverse to the end of the list and add new node
            current = self.head
            while current.next:
                current = current.next
            current.next = new_node

        self.size += 1

    def print_list(self):
        """
        Print all elements in the list in order.
        """
        if not self.head:
            print("List is empty")
            return

        elements = []
        current = self.head
        while current:
            elements.append(str(current.data))
            current = current.next

        print(" -> ".join(elements))

    def delete_nth(self, n):
        """
        Delete the nth node from the list (1-based indexing).

        Args:
            n (int): The position of the node to delete (1-based)

        Raises:
            LinkedListError: If the list is empty or index is out of range
        """
        # Check if list is empty
        if not self.head:
            raise LinkedListError("Cannot delete from empty list")

        # Check if index is valid
        if n < 1 or n > self.size:
            raise LinkedListError(f"Index {n} out of range. Valid range: 1 to {self.size}")

        # If deleting the first node
        if n == 1:
            self.head = self.head.next
            self.size -= 1
            return

        # Traverse to the (n-1)th node
        current = self.head
        for i in range(n - 2):
            current = current.next

        # Delete the nth node by updating the link
        node_to_delete = current.next
        current.next = node_to_delete.next
        self.size -= 1

    def is_empty(self):
        """
        Check if the list is empty.

        Returns:
            bool: True if list is empty, False otherwise
        """
        return self.head is None

    def get_size(self):
        """
        Get the current size of the list.

        Returns:
            int: The number of nodes in the list
        """
        return self.size

    def get_element_at(self, n):
        """
        Get the data at the nth position (1-based indexing).

        Args:
            n (int): The position to retrieve data from (1-based)

        Returns:
            The data at the specified position

        Raises:
            LinkedListError: If index is out of range
        """
        if n < 1 or n > self.size:
            raise LinkedListError(f"Index {n} out of range. Valid range: 1 to {self.size}")

        current = self.head
        for i in range(n - 1):
            current = current.next

        return current.data


def test_linked_list():
    """
    Test function to demonstrate the LinkedList implementation.
    """
    print("=== Testing Singly Linked List Implementation ===\n")

    # Create a new linked list
    ll = LinkedList()

    # Test adding elements
    print("1. Adding elements to the list:")
    elements_to_add = [10, 20, 30, 40, 50]
    for element in elements_to_add:
        ll.add(element)
        print(f"   Added {element}")

    print("\n   Current list:")
    print("   ", end="")
    ll.print_list()
    print(f"   Size: {ll.get_size()}")

    # Test getting elements
    print("\n2. Getting elements by position:")
    try:
        for i in range(1, 4):
            element = ll.get_element_at(i)
            print(f"   Element at position {i}: {element}")
    except LinkedListError as e:
        print(f"   Error: {e}")

    # Test deleting valid nodes
    print("\n3. Testing valid deletions:")

    # Delete middle node (position 3)
    try:
        print(f"   Deleting node at position 3 (value: {ll.get_element_at(3)})")
        ll.delete_nth(3)
        print("   List after deletion:")
        print("   ", end="")
        ll.print_list()
        print(f"   Size: {ll.get_size()}")
    except LinkedListError as e:
        print(f"   Error: {e}")

    # Delete first node
    try:
        print(f"\n   Deleting first node (value: {ll.get_element_at(1)})")
        ll.delete_nth(1)
        print("   List after deletion:")
        print("   ", end="")
        ll.print_list()
        print(f"   Size: {ll.get_size()}")
    except LinkedListError as e:
        print(f"   Error: {e}")

    # Test exception handling
    print("\n4. Testing exception handling:")

    # Test out of range deletion
    try:
        print("   Attempting to delete node at position 10 (out of range):")
        ll.delete_nth(10)
    except LinkedListError as e:
        print(f"   Caught exception: {e}")

    # Test negative index
    try:
        print("   Attempting to delete node at position -1 (invalid):")
        ll.delete_nth(-1)
    except LinkedListError as e:
        print(f"   Caught exception: {e}")

    # Delete remaining nodes to test empty list
    print("\n5. Testing deletion from empty list:")
    current_size = ll.get_size()
    for i in range(current_size):
        ll.delete_nth(1)  # Always delete first node

    print("   All nodes deleted. Current list:")
    print("   ", end="")
    ll.print_list()

    # Try to delete from empty list
    try:
        print("   Attempting to delete from empty list:")
        ll.delete_nth(1)
    except LinkedListError as e:
        print(f"   Caught exception: {e}")

    print("\n=== Test completed successfully! ===")


if __name__ == "__main__":
    test_linked_list()
```

## How to Run

1. Save the code to a file (e.g., `linked_list.py`)
2. Run the file using Python:
   ```bash
   python linked_list.py
   ```

## Usage Example

```python
# Create a new linked list
my_list = LinkedList()

# Add elements
my_list.add(10)
my_list.add(20)
my_list.add(30)

# Print the list
my_list.print_list()  # Output: 10 -> 20 -> 30

# Delete the 2nd node
my_list.delete_nth(2)
my_list.print_list()  # Output: 10 -> 30

# Get list size
print(f"Size: {my_list.get_size()}")  # Output: Size: 2
```

## Sample Output

```
=== Testing Singly Linked List Implementation ===

1. Adding elements to the list:
   Added 10
   Added 20
   Added 30
   Added 40
   Added 50

   Current list:
   10 -> 20 -> 30 -> 40 -> 50
   Size: 5

2. Getting elements by position:
   Element at position 1: 10
   Element at position 2: 20
   Element at position 3: 30

3. Testing valid deletions:
   Deleting node at position 3 (value: 30)
   List after deletion:
   10 -> 20 -> 40 -> 50
   Size: 4

   Deleting first node (value: 10)
   List after deletion:
   20 -> 40 -> 50
   Size: 3

4. Testing exception handling:
   Attempting to delete node at position 10 (out of range):
   Caught exception: Index 10 out of range. Valid range: 1 to 3
   Attempting to delete node at position -1 (invalid):
   Caught exception: Index -1 out of range. Valid range: 1 to 3

5. Testing deletion from empty list:
   All nodes deleted. Current list:
   List is empty
   Attempting to delete from empty list:
   Caught exception: Cannot delete from empty list

=== Test completed successfully! ===
```

## Class Structure

### Node Class
- **Purpose**: Represents individual nodes in the linked list
- **Attributes**: 
  - `data`: Stores the node's data
  - `next`: Points to the next node in the list

### LinkedList Class
- **Purpose**: Manages the linked list operations
- **Attributes**:
  - `head`: Points to the first node
  - `size`: Tracks the number of nodes

### Available Methods

| Method | Description | Parameters | Returns |
|--------|-------------|------------|---------|
| `add(data)` | Adds a node to the end of the list | `data`: Data to store | None |
| `print_list()` | Prints all elements in the list | None | None |
| `delete_nth(n)` | Deletes the nth node (1-based index) | `n`: Position to delete | None |
| `is_empty()` | Checks if list is empty | None | Boolean |
| `get_size()` | Returns the size of the list | None | Integer |
| `get_element_at(n)` | Gets data at nth position | `n`: Position (1-based) | Data |

## Exception Handling

The implementation includes robust exception handling:

- **LinkedListError**: Custom exception class
- **Empty List Operations**: Prevents deletion from empty lists
- **Index Out of Range**: Validates indices before operations
- **Clear Error Messages**: Provides specific error information

## Requirements Fulfilled

✅ **Object-Oriented Programming principles**  
✅ **Node class implementation**  
✅ **LinkedList class with required methods**  
✅ **Add node functionality**  
✅ **Print list functionality**  
✅ **Delete nth node functionality (1-based indexing)**  
✅ **Exception handling for empty list**  
✅ **Exception handling for out-of-range indices**  
✅ **Comprehensive testing implementation**

## Features

- Clean, readable code with comprehensive documentation
- Proper error han
