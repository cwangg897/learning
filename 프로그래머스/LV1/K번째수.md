정렬문제이다 그냥 단순하다
여기서 배열에서 copyOfRange로 범위를 복사할 수 있다

```java
import java.util.*;


class Solution {
    public int[] solution(int[] array, int[][] commands) {
        int[] answer = new int[commands.length];
        List<Integer> list = new ArrayList<>();

        for(int i=0; i< commands.length; i++){
            int[] ints = Arrays.copyOfRange(array, commands[i][0]-1, commands[i][1]);
            Arrays.sort(ints);
            int anInt = ints[commands[i][2]-1];
            list.add(anInt);
        }
        for(int i=0; i<list.size(); i++){
            answer[i] = list.get(i);
        }
        return answer;
    }
}
```
