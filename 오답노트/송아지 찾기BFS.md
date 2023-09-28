![image](https://github.com/cwangg897/learning/assets/79621675/04df9808-8df3-4a34-8fa7-b4d13fcc5bbb) <br>
다음과 같이 BFS는 레벨탐색이니까 레벨에서 만나면 빨리 끝난다. 그런데 여기서 5일때 다시 재 탐색하는것은 같은것을 반복하기때문에 제외시켜주면 시간 오버를 해결할 수 있다 <br>
즉 체크해야할부분은 반복해서 봐야하는가 최단거리라서 이전에 했던거는 확인안해도된다. <br>
상태트리를 짜야한다. <br>

#### 중요한점
넣을때 이미 방문 여부를 체크해야한다 만약 같은레벨에서 여러번 넣을수 있기떄문이다 <br>
다음 이동 위치 상태가 고정되어있다면 int[] 배열을 사용하자 그리고 배열index를 넘는지도 검사하자 <br>

### 개선 코드
```java

import java.util.*;


public class Main {
    public static int solution(int s, int e) {
        boolean[] visited = new boolean[10001];
        int[] dis = {1, -1, 5};
        Queue<Integer> queue = new LinkedList<>();
        int L = 0;
        queue.offer(s);
        visited[s] = true;
        while (!queue.isEmpty()) {
            int len = queue.size();
            for (int i = 0; i < len; i++) {
                int poll = queue.poll();
                if (poll == e) {
                    return L;
                }
                for(int j=0; j<dis.length; j++){
                    int next = dis[j] + poll;
                    if(next >= 1 &&  next<= 10000 && !visited[next]){
                        queue.offer(next);
                        visited[next] = true;
                    }
                }
            }
            L += 1;
        }
        return 1;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int s = sc.nextInt();
        int e = sc.nextInt();
        System.out.println(solution(s, e));
    }


}
```


### 좀더 빠른거
```java

import java.util.*;


public class Main {
    public static int solution(int s, int e) {
        boolean[] visited = new boolean[10001];
        int[] dis = {1, -1, 5};
        Queue<Integer> queue = new LinkedList<>();
        int L = 0;
        queue.offer(s);
        visited[s] = true;
        while (!queue.isEmpty()) {
            int len = queue.size();
            for (int i = 0; i < len; i++) {
                int poll = queue.poll();
                for(int j=0; j<dis.length; j++){
                    int next = dis[j] + poll;
                    if(next == e){
                        return L+1;
                    }
                    if(next >= 1 &&  next<= 10000 && !visited[next]){
                        queue.offer(next);
                        visited[next] = true;
                    }
                }
            }
            L += 1;
        }
        return 1;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int s = sc.nextInt();
        int e = sc.nextInt();
        System.out.println(solution(s, e));
    }


}


```



### 깔끔하지 못한 코드
```java
import java.util.*;


public class Main {
    public static int solution(int s, int e) {
        boolean[] visited = new boolean[10001];
        int[] dis = {1, -1, 5};
        Queue<Integer> queue = new LinkedList<>();
        int L = 0;
        queue.offer(s);
        visited[s] = true;
        while (!queue.isEmpty()) {
            int len = queue.size();
            for (int i = 0; i < len; i++) {
                int poll = queue.poll();
                if (poll == e) {
                    return L;
                }
                if (!visited[poll + 1] && poll + 1 <= 10000) {
                    queue.offer(poll + 1);
                    visited[poll+1] = true;
                }
                if (!visited[poll - 1] && poll - 1 > 0) {
                    queue.offer(poll - 1);
                    visited[poll-1] = true;
                }
                if (!visited[poll + 5] && poll + 5 <= 10000) {
                    queue.offer(poll + 5);
                    visited[poll+5] = true;
                }

            }
            L += 1;
        }
        return 1;
    }


    // 재귀함수는 스택이다
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int s = sc.nextInt();
        int e = sc.nextInt();
        System.out.println(solution(s, e));
    }


}

```
