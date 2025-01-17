## Longest Increasing Subsequence
- Use a DP array `dp` where `dp[i]` represents the length of the longest increasing subsequence ending at index i.
- For each element nums[i], examine all previous elements nums[j] where j < i. If nums[j] < nums[i], update dp[i] using the formula:
dp[i] = max(dp[i], dp[j] + 1)
- The final result is the maximum value found in the `dp` array.

---

```java
import java.util.Arrays;

public class Solution {
    public int lengthOfLIS(int[] nums) {
        // Edge case: If the array is empty, return 0
        if (nums == null || nums.length == 0) {
            return 0;
        }

        // Initialize an array to track the length of the LIS ending at each index
        int[] lisLengths = new int[nums.length];
        Arrays.fill(lisLengths, 1); // Each element is an LIS of length 1 by default

        int maxLength = 1; // Variable to track the global maximum LIS length

        // Iterate through each element in the array
        for (int current = 1; current < nums.length; current++) {
            // Compare the current element with all previous elements
            for (int previous = 0; previous < current; previous++) {
                // If nums[current] can extend the LIS ending at nums[previous]
                if (nums[previous] < nums[current]) {
                    // Update the LIS length for the current index
                    lisLengths[current] = Math.max(lisLengths[current], lisLengths[previous] + 1);
                }
            }
            // Update the global maximum LIS length
            maxLength = Math.max(maxLength, lisLengths[current]);
        }

        return maxLength; // Return the length of the longest increasing subsequence
    }
}
```
