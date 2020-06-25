
Suppose if you have to burst N Balloons, which are like N Steps. 
In the the i th step we have n - i balloons left. This will become O(N!).
Well, it is slow, probably works for n < 12 only.

dp[i][j]: coins obtained from bursting all the balloons between index i and j (not including i or j)

dp[i][j] = max(nums[i] * nums[k] * nums[j] + dp[i][k] + dp[k][j]) (k in (i+1,j))


If k is the index of the last balloon burst in (i, j), the coins that burst will get are nums[i] * nums[k] * nums[j], and to calculate dp[i][j], we also need to add the coins obtained from bursting balloons between i and k, and between k and j, i.e., dp[i][k] and dp[k][j]


```java 



public int maxCoins(int[] nums) {
        int n = nums.length;
        if (n == 0) return 0;
        if (n == 1) return nums[0];

        int[][] coin = new int[n + 2][n + 2];

        int[] list = new int[n + 2];
        list[0] = 1;
        list[n + 1] = 1; // Setting up the 

        for (int i = 0; i < n; i++) {
            list[i + 1] = nums[i];
        }

        for (int len = 1; len <= n; len++) {
            for (int i = 1; i <= n - len + 1; i++) {
                int j = len + i - 1;
                for (int k = i; k <= j; k++) {
                    coin[i][j] = Math.max(coin[i][j],
                            coin[i][k - 1] + list[i - 1] * list[k] * list[j + 1] + coin[k + 1][j]);
                }
            }
        }
        return coin[1][n];
    }

```