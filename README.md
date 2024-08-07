# Heavy Sort Algorithm

## Introduction
The Heavy Sort algorithm simulates the process of pushing numbers into a water bucket, where they settle at positions corresponding to their values. When the numbers sink or float, they are sorted in ascending order.

## How It Works
1. **Initialization**:
   - Find the minimum and maximum values in the input array.
   - Create a dictionary structure to represent the bucket, where each number value is a position in the bucket.

2. **Pushing Numbers into the Bucket**:
   - Iterate through each number in the input array.
   - For each number, place it in the corresponding position in the dictionary, and count its occurrences.

3. **Creating the Sorted Array**:
   - Iterate through all values from the minimum to the maximum.
   - If the value exists in the dictionary, add its occurrences to the result array.

## Python Code

```python
# Copyright © Bùi Nguyễn Tấn Sang (EndermanPC) 2024

def heavy_sort(arr):
    if not arr:
        return arr

    min_value = min(arr)
    max_value = max(arr)
    
    buckets = {}
    
    for num in arr:
        if num not in buckets:
            buckets[num] = 0
        buckets[num] += 1
    
    sorted_arr = []
    for num in range(min_value, max_value + 1):
        if num in buckets:
            sorted_arr.extend([num] * buckets[num])
    
    return sorted_arr

arr = [1, 3, 6, 7]
sorted_arr = heavy_sort(arr)
print("Sorted Array:", sorted_arr)
```

## C++ Code
```cpp
// Copyright © Bùi Nguyễn Tấn Sang (EndermanPC) 2024

#include <iostream>
#include <vector>
#include <unordered_map>
#include <algorithm>

std::vector<int> heavy_sort(const std::vector<int>& arr) {
    if (arr.empty()) {
        return arr;
    }

    int min_value = *std::min_element(arr.begin(), arr.end());
    int max_value = *std::max_element(arr.begin(), arr.end());
    
    // Step 1: Create a map to act as the bucket
    std::unordered_map<int, int> buckets;
    
    // Step 2: Push numbers into the bucket
    for (int num : arr) {
        buckets[num]++;
    }
    
    // Step 3: Create the sorted array
    std::vector<int> sorted_arr;
    for (int num = min_value; num <= max_value; ++num) {
        if (buckets.find(num) != buckets.end()) {
            sorted_arr.insert(sorted_arr.end(), buckets[num], num);
        }
    }
    
    return sorted_arr;
}

// Example usage
int main() {
    std::vector<int> arr = {1, 3, 6, 7};
    std::vector<int> sorted_arr = heavy_sort(arr);
    std::cout << "Sorted array: ";
    for (int num : sorted_arr) {
        std::cout << num << " ";
    }
    std::cout << std::endl;
    return 0;
}
```

## Other Code
You can find code for other languages ​​above (source.*)

## Complexity Analysis
**Space**:
- Uses a dictionary to store elements by their values. In the worst case, this requires O(N) space if all elements are unique.

**Time**:
- **Finding min and max values**: O(N).
- **Pushing numbers into the bucket (dictionary)**: O(N).
- **Creating the sorted array from the dictionary**: O(N + M), where M is the range between the smallest and largest numbers.

## Comparison with Other Algorithms
- **Bubble Sort, Selection Sort, Insertion Sort**: O(N^2) time complexity in the worst case, O(1) space complexity.
- **Merge Sort**: O(N log N) time complexity in all cases, O(N) space complexity.
- **Quick Sort**: Average O(N log N) time complexity, worst case O(N^2), O(log N) space complexity.
- **Counting Sort**: O(N + K) time complexity, O(K) space complexity.
- **Radix Sort**: O(N * k) time complexity, O(N + K) space complexity.

## Performance on test data:
- **Array of size 10^6, randomly generated numbers from 1 to 100**: runs in `0.113055s`.
- **Array of size 10^5, randomly generated numbers from 0 to 100**: runs in `0.016916s`.

## Some notes about the algorithm
- The algorithm works well if your data is `dense` (meaning the gap between the smallest and largest numbers ​​is not too large, for example: `75, 81, 90`). This is the ideal condition to use it.
+ If your data is too `sparse` (for example: `1, 2, 1000`) it will perform worse than other algorithms. 
- The algorithm is faster than Bubble Sort, Selection Sort, and Insertion Sort only if there aren't huge gaps between the numbers (as mentioned above) but it will be slower than Quick Sort and Merge Sort.

## Conclusion
The Heavy Sort algorithm is an innovative and intuitive approach based on the idea of weight and the sinking/floating of numbers. While it may not be space-efficient when the largest value is too large, using a dictionary optimizes memory usage and keeps the time complexity acceptable. This makes the algorithm a unique and effective solution in many practical scenarios.

## Contact
For any questions or contributions, please reach out to me at [endermatday@gmail.com].

## License
This project is licensed under the Apache 2.0 License.
