---
Title: '.floor()'
Description: 'Returns a new tensor with the largest integer less than or equal to each element of the input tensor.'
Subjects:
  - 'Computer Science'
  - 'Data Science'
Tags:
  - 'Deep Learning'
  - 'Functions'
  - 'Methods'
  - 'PyTorch'
  - 'Tensor'
CatalogContent:
  - 'intro-to-py-torch-and-neural-networks'
  - 'paths/data-science'
---

The **`.floor()`** method in PyTorch returns a new [tensor](https://www.codecademy.com/resources/docs/pytorch/tensors) with the largest integer less than or equal to each element of the input tensor. This operation rounds down each value to the nearest integer toward negative infinity, which is useful in data preprocessing, quantization operations, and mathematical transformations where downward rounding is required.

## Syntax

```pseudo
torch.floor(input, *, out=None)
```

**Parameters:**

- `input` (Tensor): The input tensor containing values to be floored.
- `out` (Tensor, optional): The output tensor to store the result. If provided, it must have the same shape as the input tensor.

**Return value:**

The `.floor()` function returns a new tensor containing the floor values of each element in the input tensor. The result tensor has the same shape as the input tensor and preserves the original data type.

## Example 1: Basic Usage of `.floor()` with Different Value Types

This example demonstrates how `.floor()` handles various types of numerical values:

```py
import torch

# Create a tensor with positive and negative floating-point values
tensor = torch.tensor([[-3.7, 2.5], [1.2, -0.8], [5.0, -2.3]])

# Apply the floor operation
floor_tensor = torch.floor(tensor)

print("Original Tensor:")
print(tensor)

print("\nFloor Tensor:")
print(floor_tensor)

# Example with edge cases
edge_cases = torch.tensor([0.0, -0.0, 3.99999, -1.00001])
floor_edges = torch.floor(edge_cases)

print("\nEdge Cases:")
print("Original:", edge_cases)
print("Floored: ", floor_edges)
```

This example results in the following output:

```shell
Original Tensor:
tensor([[-3.7000,  2.5000],
        [ 1.2000, -0.8000],
        [ 5.0000, -2.3000]])

Floor Tensor:
tensor([[-4.,  2.],
        [ 1., -1.],
        [ 5., -3.]])

Edge Cases:
Original: tensor([ 0.0000, -0.0000,  3.9999, -1.0000])
Floored:  tensor([ 0.,  0.,  3., -1.])
```

The `.floor()` operation consistently rounds toward negative infinity:

- **Positive values**: 2.5 → 2.0, 1.2 → 1.0, 3.99999 → 3.0
- **Negative values**: -3.7 → -4.0, -0.8 → -1.0, -2.3 → -3.0
- **Integer values**: 5.0 remains 5.0, -1.0 remains -1.0

## Example 2: Data Quantization with `.floor()`

The `.floor()` function is commonly used for quantizing continuous data into discrete bins. Here's an example of creating histograms or binning data:

```py
import torch

# Simulate continuous data (e.g., sensor readings, pixel intensities)
continuous_data = torch.tensor([
    [12.7, 25.3, 8.9, 31.1],
    [19.8, 6.2, 28.4, 15.6],
    [22.1, 33.7, 11.5, 27.9]
])

# Normalize to range [0, 10) and then quantize to integer bins
normalized = continuous_data / 3.5  # Scale down
quantized_bins = torch.floor(normalized)

print("Original continuous data:")
print(continuous_data)
print("\nNormalized data:")
print(normalized)
print("\nQuantized bins (0-9):")
print(quantized_bins)

# Count elements in each bin
unique_bins, counts = torch.unique(quantized_bins, return_counts=True)
print("\nBin distribution:")
for bin_val, count in zip(unique_bins, counts):
    print(f"Bin {int(bin_val)}: {count} elements")
```

Here is the output:

```shell
Original continuous data:
tensor([[12.7000, 25.3000,  8.9000, 31.1000],
        [19.8000,  6.2000, 28.4000, 15.6000],
        [22.1000, 33.7000, 11.5000, 27.9000]])

Normalized data:
tensor([[3.6286, 7.2286, 2.5429, 8.8857],
        [5.6571, 1.7714, 8.1143, 4.4571],
        [6.3143, 9.6286, 3.2857, 7.9714]])

Quantized bins (0-9):
tensor([[3., 7., 2., 8.],
        [5., 1., 8., 4.],
        [6., 9., 3., 7.]])

Bin distribution:
Bin 1: 1 elements
Bin 2: 1 elements
Bin 3: 2 elements
Bin 4: 1 elements
Bin 5: 1 elements
Bin 6: 1 elements
Bin 7: 2 elements
Bin 8: 2 elements
Bin 9: 1 elements
```

This example demonstrates how `.floor()` can be used to convert continuous values into discrete categories, which is useful for creating histograms, implementing quantization layers in neural networks, or preparing data for discrete algorithms.

## Example 3: Implementing Custom Step Functions

The `.floor()` function can be used to create custom step functions and piecewise constant functions commonly used in neural network architectures:

```py
import torch

# Create a custom step activation function using floor
def step_activation(x, num_steps=5):
    """
    Custom step activation function that creates discrete output levels
    """
    # Scale input to desired range and apply floor
    scaled = x * num_steps
    stepped = torch.floor(scaled) / num_steps
    return stepped

# Test the step activation function
input_data = torch.linspace(-2, 2, 20)
stepped_output = step_activation(input_data, num_steps=4)

print("Input data:")
print(input_data)
print("\nStepped output (4 levels):")
print(stepped_output)

# Visualize the step function behavior
print("\nInput -> Output mapping:")
for i in range(0, len(input_data), 3):
    print(f"{input_data[i].item():.3f} -> {stepped_output[i].item():.3f}")
```

Here is the output:

```shell
Input data:
tensor([-2.0000, -1.7895, -1.5789, -1.3684, -1.1579, -0.9474, -0.7368, -0.5263,
        -0.3158, -0.1053,  0.1053,  0.3158,  0.5263,  0.7368,  0.9474,  1.1579,
         1.3684,  1.5789,  1.7895,  2.0000])

Stepped output (4 levels):
tensor([-2.0000, -1.7500, -1.7500, -1.5000, -1.2500, -1.0000, -1.0000, -0.7500,
        -0.5000, -0.2500,  0.0000,  0.2500,  0.5000,  0.7500,  0.7500,  1.0000,
         1.2500,  1.5000,  1.5000,  1.7500])

Input -> Output mapping:
-2.000 -> -2.000
-1.368 -> -1.500
-0.737 -> -1.000
-0.105 -> -0.250
0.526 -> 0.500
1.158 -> 1.000
1.789 -> 1.500
```
