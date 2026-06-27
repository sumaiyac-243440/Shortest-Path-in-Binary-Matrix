class Solution {
public:
    int shortestPathBinaryMatrix(vector<vector<int>>& grid) {

        int n = grid.size();

        if (grid[0][0] == 1 || grid[n - 1][n - 1] == 1)
            return -1;

        vector<vector<int>> dist(n, vector<int>(n, INT_MAX));

        queue<pair<int, int>> q;

        q.push({0, 0});
        dist[0][0] = 1;

        int dx[] = {-1,-1,-1,0,0,1,1,1};
        int dy[] = {-1,0,1,-1,1,-1,0,1};

        while (!q.empty()) {

            int x = q.front().first;
            int y = q.front().second;
            q.pop();

            for (int i = 0; i < 8; i++) {

                int nx = x + dx[i];
                int ny = y + dy[i];

                if (nx >= 0 && nx < n &&
                    ny >= 0 && ny < n &&
                    grid[nx][ny] == 0 &&
                    dist[nx][ny] == INT_MAX) {

                    dist[nx][ny] = dist[x][y] + 1;
                    q.push({nx, ny});
                }
            }
        }

        if (dist[n - 1][n - 1] == INT_MAX)
            return -1;

        return dist[n - 1][n - 1];
    }
};
