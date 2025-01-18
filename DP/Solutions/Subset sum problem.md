### Subset sum problem

```
class Solution {
    public int maxSumIS(int arr[]) {
        // code here.
        
        int[] dp = new int[arr.length];
        
        for (int i = 0; i < arr.length; i++) {
             dp[i] = arr[i];   
        }
        
        for (int curr = 1; curr < arr.length; curr++ ) {
            for (int prev = 0; prev < curr; prev++ ) {
                if (arr[prev] < arr[curr]) {
                     dp[curr] = Math.max(dp[curr], dp[prev] + arr[curr]);
                }
            }
        }
        
        int maxSum = 0;
        for (int num: dp){
            maxSum = Math.max(maxSum, num);
        }
        
        return maxSum;
    }
}
```
