

# Count All Triplets with Given Sum in Sorted Array

### **Difficulty**: Medium  
### **Accuracy**: 48.57%  
### **Points**: 4  

## Problem Statement
Given a sorted array `arr[]` and a target value, the task is to count triplets `(i, j, k)` of valid indices, such that:
- `arr[i] + arr[j] + arr[k] = target`  
- `i < j < k`

### **Examples**

#### **Example 1**:
**Input**:  
`arr[] = [-3, -1, -1, 0, 1, 2], target = -2`  
**Output**:  
`4`  
**Explanation**:  
Four triplets that add up to `-2` are:
- `arr[0] + arr[3] + arr[4] = (-3) + 0 + 1 = -2`
- `arr[0] + arr[1] + arr[5] = (-3) + (-1) + 2 = -2`
- `arr[0] + arr[2] + arr[5] = (-3) + (-1) + 2 = -2`
- `arr[1] + arr[2] + arr[3] = (-1) + (-1) + 0 = -2`

---

#### **Example 2**:
**Input**:  
`arr[] = [-2, 0, 1, 1, 5], target = 1`  
**Output**:  
`0`  
**Explanation**:  
There is no triplet whose sum is equal to `1`.

---

### **Constraints**
- `3 ≤ arr.size() ≤ 10^4`
- `-10^5 ≤ arr[i], target ≤ 10^5`

---

## Solution

```java
//{ Driver Code Starts
// Initial Template for Java
import java.io.*;
import java.util.*;
import java.util.stream.Collectors;

public class Main {
    public static void main(String[] args) throws Exception {
        Scanner sc = new Scanner(System.in);
        int t = Integer.parseInt(sc.nextLine());
        while (t-- > 0) {
            String[] arr1Str = sc.nextLine().split(" ");
            int[] arr = Arrays.stream(arr1Str).mapToInt(Integer::parseInt).toArray();
            int target = Integer.parseInt(sc.nextLine());

            Solution ob = new Solution();
            int ans = ob.countTriplets(arr, target);
            System.out.println(ans);
            System.out.println("~");
        }
    }
}
// } Driver Code Ends

class Solution {
    public int countTriplets(int[] arr, int target) {
        int n = arr.length, res = 0;
        for (int i = 0; i < n - 2; i++) {
            int left = i + 1, right = n - 1;
            while (left < right) {
                int sum = arr[i] + arr[left] + arr[right];
                if (sum < target) {
                    left++;
                } else if (sum > target) {
                    right--;
                } else {
                    if (arr[left] == arr[right]) {
                        int count = right - left + 1;
                        res += count * (count - 1) / 2;
                        break;
                    } else {
                        int cnt1 = 1, cnt2 = 1;
                        while (left + 1 < right && arr[left] == arr[left + 1]) {
                            left++;
                            cnt1++;
                        }
                        while (right - 1 > left && arr[right] == arr[right - 1]) {
                            right--;
                            cnt2++;
                        }
                        res += cnt1 * cnt2;
                        left++;
                        right--;
                    }
                }
            }
        }
        return res;
    }
}
```

---

### **Explanation**

1. **Outer Loop**: Iterate through the array with index `i` from `0` to `n - 3`.
2. **Two-Pointer Technique**: For each `i`, use two pointers (`left` and `right`) to find pairs in the range `i+1` to `n-1` that sum with `arr[i]` to the target.
3. **Count Combinations**:
   - If `arr[left] == arr[right]`, calculate combinations directly.
   - Otherwise, count identical values for both pointers and multiply their counts.
4. **Efficiency**: This approach avoids checking all triplet combinations explicitly, making it more efficient for large arrays.

---

### **Complexity Analysis**

- **Time Complexity**:  
  \( O(n^2) \), where \( n \) is the size of the array. The two-pointer technique for each element reduces redundant checks.

- **Space Complexity**:  
  \( O(1) \), as no additional data structures are used.

---



