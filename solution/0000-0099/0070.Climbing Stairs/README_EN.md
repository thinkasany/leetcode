# [70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs)

[中文文档](/solution/0000-0099/0070.Climbing%20Stairs/README.md)

## Description

<p>You are climbing a staircase. It takes <code>n</code> steps to reach the top.</p>

<p>Each time you can either climb <code>1</code> or <code>2</code> steps. In how many distinct ways can you climb to the top?</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> n = 2
<strong>Output:</strong> 2
<strong>Explanation:</strong> There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> n = 3
<strong>Output:</strong> 3
<strong>Explanation:</strong> There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= n &lt;= 45</code></li>
</ul>

## Solutions

<!-- tabs:start -->

### **Python3**

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        a, b = 0, 1
        for _ in range(n):
            a, b = b, a + b
        return b
```

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        def mul(a: List[List[int]], b: List[List[int]]) -> List[List[int]]:
            m, n = len(a), len(b[0])
            c = [[0] * n for _ in range(m)]
            for i in range(m):
                for j in range(n):
                    for k in range(len(a[0])):
                        c[i][j] = c[i][j] + a[i][k] * b[k][j]
            return c

        def pow(a: List[List[int]], n: int) -> List[List[int]]:
            res = [[1, 1], [0, 0]]
            while n:
                if n & 1:
                    res = mul(res, a)
                n >>= 1
                a = mul(a, a)
            return res

        a = [[1, 1], [1, 0]]
        return pow(a, n - 1)[0][0]
```

### **Java**

```java
class Solution {
    public int climbStairs(int n) {
        int a = 0, b = 1;
        for (int i = 0; i < n; ++i) {
            int c = a + b;
            a = b;
            b = c;
        }
        return b;
    }
}
```

```java
class Solution {
    public int climbStairs(int n) {
        int[][] a = {{1, 1,}, {1, 0}};
        return pow(a, n - 1)[0][0];
    }

    private int[][] mul(int[][] a, int[][] b) {
        int m = a.length, n = b[0].length;
        int[][] c = new int[m][n];
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                for (int k = 0; k < a[0].length; ++k) {
                    c[i][j] += a[i][k] * b[k][j];
                }
            }
        }
        return c;
    }

    private int[][] pow(int[][] a, int n) {
        int[][] res = {{1, 1}, {0, 0}};
        while (n > 0) {
            if ((n & 1) == 1) {
                res = mul(res, a);
            }
            n >>= 1;
            a = mul(a, a);
        }
        return res;
    }
}
```

### **C++**

```cpp
class Solution {
public:
    int climbStairs(int n) {
        int a = 0, b = 1;
        for (int i = 0; i < n; ++i) {
            int c = a + b;
            a = b;
            b = c;
        }
        return b;
    }
};
```

```cpp
class Solution {
public:
    int climbStairs(int n) {
        vector<vector<long long>> a = {{1, 1}, {1, 0}};
        return pow(a, n - 1)[0][0];
    }

private:
    vector<vector<long long>> mul(vector<vector<long long>>& a, vector<vector<long long>>& b) {
        int m = a.size(), n = b[0].size();
        vector<vector<long long>> res(m, vector<long long>(n));
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                for (int k = 0; k < a[0].size(); ++k) {
                    res[i][j] += a[i][k] * b[k][j];
                }
            }
        }
        return res;
    }

    vector<vector<long long>> pow(vector<vector<long long>>& a, int n) {
        vector<vector<long long>> res = {{1, 1}, {0, 0}};
        while (n) {
            if (n & 1) {
                res = mul(res, a);
            }
            a = mul(a, a);
            n >>= 1;
        }
        return res;
    }
};
```

### **Go**

```go
func climbStairs(n int) int {
	a, b := 0, 1
	for i := 0; i < n; i++ {
		a, b = b, a+b
	}
	return b
}
```

```go
type matrix [2][2]int

func climbStairs(n int) int {
	a := matrix{{1, 1}, {1, 0}}
	return pow(a, n-1)[0][0]
}

func mul(a, b matrix) (c matrix) {
	m, n := len(a), len(b[0])
	for i := 0; i < m; i++ {
		for j := 0; j < n; j++ {
			for k := 0; k < len(a[0]); k++ {
				c[i][j] += a[i][k] * b[k][j]
			}
		}
	}
	return
}

func pow(a matrix, n int) matrix {
	res := matrix{{1, 1}, {0, 0}}
	for n > 0 {
		if n&1 == 1 {
			res = mul(res, a)
		}
		a = mul(a, a)
		n >>= 1
	}
	return res
}
```

### **JavaScript**

```js
/**
 * @param {number} n
 * @return {number}
 */
var climbStairs = function (n) {
    let a = 0,
        b = 1;
    for (let i = 0; i < n; ++i) {
        const c = a + b;
        a = b;
        b = c;
    }
    return b;
};
```

```js
/**
 * @param {number} n
 * @return {number}
 */
var climbStairs = function (n) {
    const a = [
        [1, 1],
        [1, 0],
    ];
    return pow(a, n - 1)[0][0];
};

function mul(a, b) {
    const [m, n] = [a.length, b[0].length];
    const c = Array(m)
        .fill(0)
        .map(() => Array(n).fill(0));
    for (let i = 0; i < m; ++i) {
        for (let j = 0; j < n; ++j) {
            for (let k = 0; k < a[0].length; ++k) {
                c[i][j] += a[i][k] * b[k][j];
            }
        }
    }
    return c;
}

function pow(a, n) {
    let res = [
        [1, 1],
        [0, 0],
    ];
    while (n) {
        if (n & 1) {
            res = mul(res, a);
        }
        a = mul(a, a);
        n >>= 1;
    }
    return res;
}
```

### **TypeScript**

```ts
function climbStairs(n: number): number {
    let p = 1;
    let q = 1;
    for (let i = 1; i < n; i++) {
        [p, q] = [q, p + q];
    }
    return q;
}
```

```ts
function climbStairs(n: number): number {
    const a = [
        [1, 1],
        [1, 0],
    ];
    return pow(a, n - 1)[0][0];
}

function mul(a: number[][], b: number[][]): number[][] {
    const [m, n] = [a.length, b[0].length];
    const c = Array(m)
        .fill(0)
        .map(() => Array(n).fill(0));
    for (let i = 0; i < m; ++i) {
        for (let j = 0; j < n; ++j) {
            for (let k = 0; k < a[0].length; ++k) {
                c[i][j] += a[i][k] * b[k][j];
            }
        }
    }
    return c;
}

function pow(a: number[][], n: number): number[][] {
    let res = [
        [1, 1],
        [0, 0],
    ];
    while (n) {
        if (n & 1) {
            res = mul(res, a);
        }
        a = mul(a, a);
        n >>= 1;
    }
    return res;
}
```

### **Rust**

```rust
impl Solution {
    pub fn climb_stairs(n: i32) -> i32 {
        let (mut p, mut q) = (1, 1);
        for i in 1..n {
            let t = p + q;
            p = q;
            q = t;
        }
        q
    }
}
```

### **PHP**

```php
class Solution {
    /**
     * @param Integer $n
     * @return Integer
     */
    function climbStairs($n) {
        if ($n <= 2) {
            return $n;
        }
        $dp = [0, 1, 2];
        for ($i = 3; $i <= $n; $i++) {
            $dp[$i] = $dp[$i - 2] + $dp[$i - 1];
        }
        return $dp[$n];
    }
}
```

### **...**

```

```

<!-- tabs:end -->
