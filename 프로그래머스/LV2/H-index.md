문제이해가 핵심이고
다른케이스는 [0,1,1,3,4,5] 인경우도 생각하면됨 그래서 개수만 넘는다고 끝이아님

```java
import java.util.*;

class Solution {
    public int solution(int[] citations) {
        int answer = 0;

        Arrays.sort(citations);
        for(int i = 0; i < citations.length; i++) {
            int h = citations.length - i; // 인용된 논문의 수

            if(citations[i] >= h) {
                answer = h;
                break;
            }
        }

        return answer;
    }
}


```
