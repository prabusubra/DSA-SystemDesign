### Cutting Rods

```
public int cutRod(int[] price) {
    int n = price.length; // The rod length is the size of the price array
    int[][] memo = new int[n + 1][n + 1];

    // Initialize memo table with -1 (indicating unsolved subproblems)
    for (int i = 0; i <= n; i++) {
        for (int j = 0; j <= n; j++) {
            memo[i][j] = -1;
        }
    }

    return cutting(price, n, n, memo);
}

private int cutting(int[] price, int max, int index, int[][] memo) {
    // Base case: no rod left to cut or no more pieces available
    if (index == 0 || max == 0) {
        return 0;
    }

    // Return cached result if already computed
    if (memo[index][max] != -1) {
        return memo[index][max];
    }

    // If the piece is larger than the remaining length, skip it
    if (index > max) {
        memo[index][max] = cutting(price, max, index - 1, memo);
    } else {
        // Otherwise, consider both include and exclude options
        memo[index][max] = Math.max(
            price[index - 1] + cutting(price, max - index, index, memo), // Include the piece
            cutting(price, max, index - 1, memo)                        // Exclude the piece
        );
    }

    return memo[index][max];
}

```
