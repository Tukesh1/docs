---
Title: '.removeprefix()'
Description: 'Removes a specified prefix from the beginning of a string and returns a new string.'
Subjects:
  - 'Data Science'
  - 'Computer Science'
Tags:
  - 'Strings'
  - 'Methods'
  - 'Functions'
CatalogContent:
  - 'learn-python-3'
  - 'paths/computer-science'
---

The **`.removeprefix()`** method is a built-in [string](https://www.codecademy.com/resources/docs/python/strings) method in Python that removes a specified prefix from the beginning of a string. This method was introduced in Python 3.9 and provides a clean and intuitive way to remove a known prefix from the start of a string. If the string does not start with the specified prefix, the original string is returned unchanged.

The `.removeprefix()` method is particularly useful for text processing tasks such as removing URL schemes, file extensions, prefixes in naming conventions, and cleaning data that follows consistent formatting patterns. Unlike methods like `.lstrip()`, which removes characters from the left side, `.removeprefix()` only removes the exact prefix if it matches completely.

## Syntax

```pseudo
string.removeprefix(prefix)
```

**Parameters:**

- `prefix` (required): A string specifying the prefix to be removed from the beginning of the string. The prefix must match exactly from the start of the string.

**Return value:**

The `.removeprefix()` method returns a new string with the specified prefix removed from the beginning if it exists. If the string does not start with the prefix, the original string is returned unchanged. The original string remains unmodified since strings in Python are immutable.

## Example 1: Basic Prefix Removal

The following example demonstrates the fundamental usage of the `.removeprefix()` method with simple string manipulation:

```py
# Original string with a prefix
url = "https://www.example.com"

# Remove the protocol prefix
clean_url = url.removeprefix("https://")
print(f"Original: {url}")
print(f"Without prefix: {clean_url}")

# Try removing a prefix that doesn't exist
no_change = url.removeprefix("ftp://")
print(f"No change: {no_change}")
```

The output produced by this code is:

```shell
Original: https://www.example.com
Without prefix: www.example.com
No change: https://www.example.com
```

This example shows how `.removeprefix()` removes the exact prefix when it matches from the beginning of the string, and leaves the string unchanged when the prefix is not found.

## Example 2: File Path Processing

The following example demonstrates using `.removeprefix()` for cleaning file paths and removing common directory prefixes:

```py
# List of file paths with common prefixes
file_paths = [
    "/home/user/documents/report.pdf",
    "/home/user/documents/data.csv", 
    "/home/user/images/photo.jpg",
    "/var/log/system.log"
]

# Remove the common prefix for user files
base_prefix = "/home/user/"

print("Cleaned file paths:")
for path in file_paths:
    cleaned_path = path.removeprefix(base_prefix)
    if cleaned_path != path:
        print(f"  {cleaned_path}")
    else:
        print(f"  {path} (no prefix removed)")
```

The output of this code will be:

```shell
Cleaned file paths:
  documents/report.pdf
  documents/data.csv
  images/photo.jpg
  /var/log/system.log (no prefix removed)
```

This example illustrates how `.removeprefix()` can be used to normalize file paths by removing common directory prefixes, making the paths more readable or suitable for relative operations.

## Codebyte Example: Data Processing with Multiple Prefixes

This example shows how `.removeprefix()` is used in a data processing scenario to clean identifiers and extract meaningful information:

```codebyte/python
# Sample data with various prefixes that need to be cleaned
data_entries = [
    "ID_USER_12345",
    "ID_PRODUCT_67890", 
    "REF_ORDER_54321",
    "ID_ADMIN_99999",
    "TEMP_SESSION_11111",
    "USER_23456"  # No standard prefix
]

# Define prefixes to remove
prefixes_to_remove = ["ID_USER_", "ID_PRODUCT_", "REF_ORDER_", "ID_ADMIN_", "TEMP_SESSION_"]

print("Data cleaning results:")
print("-" * 40)

for entry in data_entries:
    original_entry = entry
    
    # Try to remove each prefix
    for prefix in prefixes_to_remove:
        cleaned_entry = entry.removeprefix(prefix)
        if cleaned_entry != entry:
            print(f"Original: {original_entry}")
            print(f"Cleaned:  {cleaned_entry}")
            print(f"Removed:  '{prefix}'")
            print()
            break
    else:
        # No prefix was removed
        print(f"No change: {original_entry}")
        print()

# Demonstrate case sensitivity
print("Case sensitivity test:")
test_string = "Hello World"
result1 = test_string.removeprefix("hello")  # lowercase 'h'
result2 = test_string.removeprefix("Hello")  # correct case
print(f"'{test_string}'.removeprefix('hello') = '{result1}'")
print(f"'{test_string}'.removeprefix('Hello') = '{result2}'")
```

This example demonstrates how `.removeprefix()` can be used effectively in data cleaning operations to remove various identifier prefixes while maintaining the integrity of data that doesn't match the expected patterns.

## Frequently Asked Questions

### 1. What Python version introduced `.removeprefix()`?

The `.removeprefix()` method was introduced in Python 3.9. If you're using an older version of Python, you can achieve similar functionality using string slicing or the `.startswith()` method combined with slicing.

### 2. How does `.removeprefix()` differ from `.lstrip()`?

While both methods remove characters from the beginning of a string, they work differently:
- `.removeprefix()` removes an exact prefix string if it matches completely from the start
- `.lstrip()` removes individual characters from the left side until it encounters a character not in the specified set

Example:
```py
text = "ababcdef"
print(text.removeprefix("ab"))    # "abcdef" (removes one "ab")
print(text.lstrip("ab"))          # "cdef" (removes all 'a' and 'b' characters)
```
### 3. Is `.removeprefix()` case-sensitive?

Yes, `.removeprefix()` is case-sensitive. The prefix must match exactly, including the case of each character.

### 4. What happens if the prefix is longer than the string?

If the prefix is longer than the string, `.removeprefix()` returns the original string unchanged since the prefix cannot match.

### 5. Can I remove multiple prefixes at once?

No, `.removeprefix()` only removes one prefix per call. To remove multiple possible prefixes, you would need to call the method multiple times or use a loop as shown in the examples above.
