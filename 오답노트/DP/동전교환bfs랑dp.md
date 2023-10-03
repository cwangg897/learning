그림 그려보니 레벨탐색인거같았다 그래서 bfs로 했는데 dp로 풀어야지 정석이다 <br>
내가 실수했던거는 dy에 대한 정의이고 dy를 무조건 dy[n-1] 이렇게 바로뒤에로만 생각하고 n번으로 끝낼거같은데 <br>
그게 아니다. 2중 for문이 오히려 더 많았고 LIS처럼 만족하는것처럼 찾는거중 dy정의한대로 <br>

### DP
![image](https://github.com/cwangg897/learning/assets/79621675/a433abcf-8a59-4edf-b017-ea3f067e3f57)


#### BFS
```java

import java.util.*;
import java.util.List;


public class Main {
    static int[] visited;
    static int[] arr;
    static int m;

    public static int bfs(int num){
        Queue<Integer> queue = new LinkedList<>();
        queue.offer(num);
        int L = 0;
        while(!queue.isEmpty()){
            int len = queue.size();
            for(int i=0; i<len; i++){
                int poll = queue.poll();
                if(poll == m){
                    return L;
                }
                for(int j=0; j<arr.length; j++){
                    int nx = poll+ arr[j];
                    if(nx>m){
                        continue;
                    }
                    if(visited[nx] == 0){
                        visited[nx] = visited[poll]+1;
                        queue.offer(nx);
                    }
                }
            }
            L+=1;
        }
        return L;
    }



    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        arr = new int[n];
        for(int i=0; i< arr.length; i++){
            arr[i] = sc.nextInt();
        }
        m = sc.nextInt();
        visited = new int[m+1];
        System.out.println(bfs(0));
    }
}

```
