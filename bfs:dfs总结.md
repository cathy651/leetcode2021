##BFS DFS 总结

BFS Ineration Level order traversal

```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        //init
        List<List<Integer>> res = new ArrayList<>();
        Queue<TreeNode> queue = new LinkedList<>();

        //corner
        if(root == null) return res;
        //add root
        queue.add(root);
        while(!queue.isEmpty()) {
            //mark size
            int curSize = queue.size();
            List<Integer> curList = new ArrayList<>();
            for(int i = 0; i < curSize; i++) {
                //get node
                TreeNode curNode = queue.poll();
                curList.add(curNode.val);
                if(curNode.left != null) queue.add(curNode.left);
                if(curNode.right != null) queue.add(curNode.right);
            }
            res.add(curList);
        }
        return res;
    }
}
```

###Breadth First Search

queue

- 经典题：单源最短路径、计算最小操作次数，Open the Lock， Perfect Squares

```java
queue<type> q;
q.push(初始状态);
while (!q.empty())
{
  type t = q.front() ;
  q.pop();
  遍历 t 的各个Next状态  next
  {
    if (next is legal)
      q.push(next); 计数或维护等;
  }
}
```

###Depth First Search（https://www.cnblogs.com/handsomelixinan/p/10346065.html）

stack

使用栈保存未被检测的结点，结点按照深度优先的次序被访问并依次被压入栈中，并以相反的次序出栈进行新的检测。

应用：需要遍历所有元素，或者是查找某一种问题的全部情况时

- 经典题：Number of Islands, Clone Graph，course schedule, Target Sum, The Maze 走迷宫

模版：3 个条件，2 个递归：

条件 1：是否出现“撞南墙” ，有条件不成立的信息

条件 2：是否存在“终点” ，有条件成立的信息

常见的方法有数组法和 HashSet 法

```java
boolean[] visited = new boolean[length] ; //数组表示，每访问过一个节点，数组将对应元素置为true

Set<类型> set = new HashSet<>() ; //建立set，每访问一个节点，将该节点加入到set中去
```

条件 3：是否需要记录轨迹，记录节点

递归 1:方向盘，用来把控下一个节点应该访问哪里

递归 2:计数器，记录递归后的大小

```java
DFS（顶点）
{
　　处理当前顶点，记录为已访问
　　遍历与当前顶点相邻的所有未访问顶点
　　{
　　　　　　标记更改;
　　　　　　DFS( 下一子状态);
　　　　　　恢复更改;
　　}
}
```

递归

```java
public 参数1 DFS(参数2)
{
    if(返回条件成立) return 参数 ；
    DFS(进行下一步的搜索遍历) ；
}
```

```java
public void dfs(){
  如果不成立，return；
  如果成功走完一条路，return;
  (标记已经走过的地方)option
  DFS 方向盘，把控下一个节点应该访问哪里；
}

public 主方程（）{
  //corner case
  if(grid == null || grid.length == 0){
    return -1;
  }
  //在某个循环内
  if (条件成立) {
    更新res;
    DFS(进行下一步的搜索遍历);
  }
  return res;
}
```

```java
DFS（int x, int y） //这里假设存的是二维数组，x、y表示两个坐标
{
     if (找到解){
     }
      for (......){
 //每到一个点下一步都有上下左右四个方向可以走，这里用一个循环遍历方向数组表示四个方向
            // 如果这个点(a,b)符合要求并且没走过
            flag[a][b] = 1; //标记‘1’表示走过
            DFS(a, b);      //进入下一次递归
            flag[a][b] = 0; //回溯，标记‘0’表示可以走
      }
}
```

https://romantic-chopin.blog.csdn.net/article/details/81629800?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1.pc_relevant_paycolumn_v3&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1.pc_relevant_paycolumn_v3&utm_relevant_index=1

https://blog.csdn.net/weixin_44668898/article/details/104115884

https://blog.csdn.net/weixin_44668898/article/details/104110988

```java

public 主函数{
  //corner case
  //前提条件
  dfs();
  return res;
}
public dfs 函数{
  // 完成目标
  如果不成功，return;
  如果成功，return;
  // 标记已经走过的
  visit = 1/ true;

  //for loop
  for(){
    // 如果在valid 范围   visited = false; i >= 0; i < length
    if() {

      dfs（） 下一层；
      （有必要时候visit = false）;
    }
  }
  return;
}
```

490. The Maze

```java
class Solution {
    public int[][] dire = {{0,1},{0,-1},{1,0},{-1,0}};
    public boolean hasPath(int[][] maze, int[] start, int[] destination) {
       // corner case
        if(maze = null || maze.length = 0 || maze[0].length = 0){
            return false;
        }
        //
        boolean[][] visit = new boolean[maze.length][maze[0].length];
        return dfs(maze, start, destination, isVisited);
    }
    public boolean dfs(int[][] maze, int[] cur, int[] des, visit){
     // dfs 里面变量 cur, visit . 不变 maze, des
        //invalid
        if (x < 0 || x >= maze.length || y < 0 || y >= maze[0].length || visit) {
            return false;
        }
        if(x == dest[0] && y == dest[1]) return true;
        if(isVisited[x][y]) return false;
        isVisited[x][y] = true;
        int x = cur[0];
        int y = cur[1];
        for (int[][] d:dire) {
          //需要re define x, y in this for loop. because the x , y would be change in x = x + d[0]; however we want it to be cur at beginning.
            x = cur[0];
            y = cur[1];
            while(x + d[0] >= 0 && x + d[0] < maze.length && y + d[1] >= 0 && y + d[1] < maze[0].length && maze[x + d[0]][y + d[1]] == 0) {
              x = x + d[0];
              y = y + d[1];
            }
            res = dfs(maze, new int[]{x, y}, dest, isVisited);
            if(res) {
                return true;
            }
        }
        return false;


    }
}
```

```java
class Solution {
    public int[][] directions = {{0,1}, {0,-1}, {1,0}, {-1,0}};

    public boolean hasPath(int[][] maze, int[] start, int[] destination) {
        // corner case
        if(maze == null || maze.length == 0 || maze[0].length == 0){
            return false;
        }
        boolean[][] isVisited = new boolean[maze.length][maze[0].length];

        return dfs(maze, start, destination, isVisited);
    }
    public boolean dfs(int[][] maze, int[] cur, int[] destination, boolean[][] isVisited){
        int x = cur[0];
        int y = cur[1];
        // corner
        // if over edges false
        // if visited false
        // if == destination true
        // if is 1 false
        if(x == destination[0] && y == destination[1]) {
            return true;
        }
        // pos2:
        if(x < 0 || y < 0 || x >= maze.length || y >= maze[0].length || isVisited[x][y] || (maze[x][y] == 1)) {
            return false;
        }
        // run the loop
        //*000*
        // 从左走到右，把起始点和重点变成true *
        isVisited[x][y] = true;
        for(int[] d:directions) {
            x = cur[0];
            y = cur[1];
            while(x + d[0] >= 0 && x + d[0] < maze.length && y + d[1] >= 0 && y + d[1] < maze[0].length && maze[x + d[0]][y + d[1]] == 0) {
                x = x + d[0];
                y = y + d[1];
            }
            // pos1:
            // nextInput,
            // ahead, visited[x][y] = true;
            boolean nextRes = dfs(maze, new int[]{x, y}, destination, isVisited);
            // unvisited
            if(nextRes) return true;
        }
        return false;
    }
}

class Solution {
    public char[][] updateBoard(char[][] board, int[] click) {
        // corner case
        if(board == null || board.length == 0){
            return board;
        }

        // initials
        int x = click[0];
        int y = click[1];

        // corner case
        if(board[x][y] == 'X' || board[x][y] == 'M'){
            board[x][y] = 'X';
            return board;
        }

        // dfs
        boolean[][] seen = new boolean[board.length][board[0].length];
        return dfs(board, x, y, seen);
    }

    public char[][] dfs(char[][] board, int x, int y, boolean[][] seen){
        int rows = board.length;
        int cols = board[0].length;
        //  in the matirx
        if(!isValid(x, y, rows, cols) || seen[x][y]){
            return board;
        } else {
            seen[x][y] = true;
            int mineNumber = calMine(board, x, y);

            if(mineNumber > 0){
                board[x][y] = (char)(mineNumber + '0');
                return board;
            } else {
                board[x][y] = 'B';
                for(int i = -1; i < 2; i++){
                    for(int j = -1; j < 2; j++){
                        if (i == 0 && j == 0) continue;
                        int m = x + i;
                        int n = y + j;
                        dfs(board, m, n, seen);
                    }
                }
                // dfs(board, x+1, y, seen);
                // dfs(board, x+1, y+1, seen);
                // dfs(board, x-1, y, seen);
                // dfs(board, x-1, y-1, seen);
                // dfs(board, x+1, y-1, seen);
                // dfs(board, x-1, y+1, seen);
                // dfs(board, x, y-1, seen);
                // dfs(board, x, y+1, seen);
            }
        }
        return board;
    }

    public int calMine(char[][] board, int x, int y){
        int count = 0;
        int rows = board.length;
        int cols = board[0].length;
        for(int i = -1; i < 2; i++){
            for(int j = -1; j < 2; j++){
                if (i == 0 && j == 0) continue;
                int m = x + i;
                int n = y + j;
                if(isValid(m, n, rows, cols) && board[m][n] == 'M') count++;
            }
        }
        return count;
    }

    public boolean isValid(int x, int y, int rows, int cols){
        if(x < 0 || y < 0 || x >= rows || y >= cols){
            return false;
        }
        return true;
    }
}
```

dp

```java
int f( int n ){
    if(n <= 1)
    return n;
    // 先创建一个dp
    int[] dp = new int[n+1];
    // 给出初始值
    dp[0] = 0;
    dp[1] = 1;
    // 找到关系
    for(int i = 2; i <= n; i++){
        dp[i] = dp[i-1] + dp[i-2];
    }
    // 把最终结果返回
    return dp[n];
}
```

总结： level order traversal 改变方式在 add to curlist. queue 加入方式不变。

```java

public List<Integer> inorderTraversal(TreeNode root) {
    List<Integer> res = new ArrayList<>();
    // method 1: recursion
    helper(root, res);
    return res;
}
//helper function
public void preorder(TreeNode root, List<Integer> nums) {
        if (root == null) return;
        nums.add(root.val);
        preorder(root.left, nums);
        preorder(root.right, nums);
}
//Preorder: Node -> Left -> Right
public void preorder(TreeNode root, List<Integer> nums) {
  if (root == null) return;
  nums.add(root.val);
  preorder(root.left, nums);
  preorder(root.right, nums);
}
//Inorder : Left -> Node -> Right
public void inorder(TreeNode root, List<Integer> nums) {
  if (root == null) return;
  inorder(root.left, nums);
  nums.add(root.val);
  inorder(root.right, nums);
}
//Postorder : Left -> Right -> Node
public void postorder(TreeNode root, List<Integer> nums) {
  if (root == null) return;
  postorder(root.left, nums);
  postorder(root.right, nums);
  nums.add(root.val);
}
```

```java
//Pre Order Traverse 中左右
public List<Integer> preorderTraversal(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    Deque<TreeNode> stack = new ArrayDeque<>();
    if (root==null) return result;
    TreeNode p = root;
    while(!stack.isEmpty() || p != null) {
        if(p != null) {
            stack.push(p);
            result.add(p.val);  // Add before going to children
            p = p.left;
        } else {
            TreeNode node = stack.pop();
            p = node.right;
        }
    }
    return result;
}
//Post Order Traverse 左右中 post 就是把pre 三个地方都倒过来写
public List<Integer> postorderTraversal(TreeNode root) {
    LinkedList<Integer> result = new LinkedList<>();
    Deque<TreeNode> stack = new ArrayDeque<>();
    TreeNode cur = root;
    while(!stack.isEmpty() || cur != null) {
        if(cur != null) {
            stack.push(cur);
            result.add(0, cur.val);  // Reverse the process of preorder
            cur = p.right;             // Reverse the process of preorder
        } else {
            cur = stack.pop();
            cur = node.left;           // Reverse the process of preorder
        }
    }
    return result;
}
//In Order Traverse 左中右
public List<Integer> inorderTraversal(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    Deque<TreeNode> stack = new ArrayDeque<>();

    TreeNode p = root;
    while(p!=null || !stack.isEmpty()) {
        if(p != null) {
            stack.push(p);
            p = p.left;
        } else {
            p = stack.pop();
            result.add(p.val);  // Add after all left children
            p = node.right;
        }
    }
    return result;
}

```
