# 886. Possible Bipartition

Given a set of `N` people (numbered `1, 2, ..., N`), we would like to split everyone into two groups of **any** size.

Each person may dislike some other people, and they should not go into the same group. 

Formally, if `dislikes[i] = [a, b]`, it means it is not allowed to put the people numbered `a` and `b` into the same group.

Return `true` if and only if it is possible to split everyone into two groups in this way.

**Example 1:**

```
Input: N = 4, dislikes = [[1,2],[1,3],[2,4]]
Output: true
Explanation: group1 [1,4], group2 [2,3]
```

**Example 2:**

```
Input: N = 3, dislikes = [[1,2],[1,3],[2,3]]
Output: false
```

**Example 3:**

```
Input: N = 5, dislikes = [[1,2],[2,3],[3,4],[4,5],[1,5]]
Output: false
```

## Solution

This problem is used by dyeing method.

First, we initialize an adjacency list to store the dislike connection. Then traverse each point in the graph and judge whether the point has been dyed. If the point isn't dyed, execute the dfs() function.

```C++
class Solution {
public:
    vector<vector<int> > graph;
    vector<int> color;
    
    bool dfs(int u, int c) {
        color[u] = c;
        for (int x : graph[u]) {
            if (!color[x]) {
                if (!dfs(x, 3 - c)) return false;
            }
            else {
                if (color[x] == c) return false;
            }
        }
        return true;
    }
    
    bool possibleBipartition(int N, vector<vector<int>>& dislikes) {
        graph.resize(N + 1);
        color.resize(N + 1);
        for (vector<int> edge : dislikes) {
            graph[edge[0]].push_back(edge[1]);
            graph[edge[1]].push_back(edge[0]);
        }
        
        bool flag = true;
        for (int i = 1; i <= N; i ++) {
            if (!color[i]) {
                if (!dfs(i, 1)) {
                    flag = false;
                    break;
                }
            }
        }
        return flag;
    }
};
```

​     