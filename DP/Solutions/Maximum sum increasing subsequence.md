### Maximum sum increasing subsequence

```
public int maxSumIncreasingSubsequence(int[] arr) {
    int n = arr.length;
    // DP array to store the maximum sum of increasing subsequences ending at each index
    int[] dp = new int[n];

    // Initialize dp array with the values of the original array
    for (int i = 0; i < n; i++) {
        dp[i] = arr[i];
    }

    // Fill the DP array based on the recurrence relation
    for (int curr = 1; curr < n; curr++) {
        for (int prev = 0; prev < curr; prev++) {
            // If arr[curr] can extend the subsequence ending at arr[prev]
            if (arr[prev] < arr[curr]) {
                dp[curr] = Math.max(dp[curr], dp[prev] + arr[curr]);
            }
        }
    }

    // Find the maximum value in the dp array
    int maxSum = 0;
    for (int sum : dp) {
        maxSum = Math.max(maxSum, sum);
    }

    return maxSum;
}

```
