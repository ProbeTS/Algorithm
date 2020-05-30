# 200. Number of Islands

Given a 2d grid map of `'1'`s (land) and `'0'`s (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example 1:**

```
Input:
11110
11010
11000
00000

Output: 1
```

**Example 2:**

```
Input:
11000
11000
00100
00011

Output: 3
```

## Solution

This is the flood fill algorithm template. It is based on Breadth-First Search.

```C++
class Solution {
public:
    vector<vector<bool> > g;
    int res;
    
    void bfs(int x, int y, vector<vector<char>>& grid) {
        queue<pair<int,int> > q;
        int dx[]={0,1,0,-1},dy[]={1,0,-1,0};
        
        q.push({x, y});
        g[x][y] = true;
        
        while (q.size()) {
            auto t = q.front();
            q.pop();
    
            for (int i = 0; i < 4; i ++) {
                int a = t.first + dx[i], b = t.second + dy[i];
                if (a >= 0 && b >= 0 && a < grid.size() && b < grid[0].size() && !g[a][b] && grid[a][b] == '1') {
                    q.push({a, b});
                    g[a][b] = true;
                }
            }
        }
        
        res ++;
        return;
    }
    
    int numIslands(vector<vector<char>>& grid) {
        if (grid.empty()) return 0;
        int row = grid.size(), col = grid[0].size();
        vector<bool> tmp(col);
        g.resize(row, tmp);
        
        for (int i = 0; i < row; i ++)
            for (int j = 0; j < col; j ++)
                if (!g[i][j] && grid[i][j] == '1') 
                    bfs(i, j, grid);
                
        return res;
    }
};
```

​     