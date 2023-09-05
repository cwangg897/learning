#### git add, commit
```
작업폴더, staging area, repository (저장소)
작업폴더 -> stagking area : 스테이킹 한다 라고한다 - commit 파일 골라놓았다라는뜻

파일 app.txt, app2.txt있으면 git add app.txt app2.txt 라던지 모든파일 스테이징은 git add .
git status : 상태창으로 어떤파일 스테이징했는지 이런거 알 수 있음 등등
git log --all --oneline : 커밋한 내역을 쭉보고싶은경우
oneline안하면 조금 이상하게 정렬됨

```


#### git branch, switch, merge
![image](https://github.com/cwangg897/learning/assets/79621675/c3a9e763-36be-4101-a5ea-95119a2914b1)
```
git diff로하면 전이랑 현재파일 차이점을 분석해서 보여준다 j/k로 스크롤바 조작 q는 종료
하지만 터미널의 한계로 별로인거같음 그래서 잘안씀
이거보다 좋은 git difftool 을 쓰면 비주얼적으로 더 훌륭함

git difftool ???? (커밋아이디) 이런거 칠수있음
커밋아아디란 git log에서 커밋 고유아이디가 있음 현재파일 vs 특정커밋 비교가능

커밋아이디 2개 가능
git difftool 커밋1 커밋2 로 1과 2간의 차이점을 비교가능

git꼭 터미널로 조작해라 이딴거는 꼰대같은마인드다 본인이 편한것사용하면된다

파일보갓본 만들어서 거기에 먼저 코드짜보면 안심

HEAD는 현재위치를 의미한다 

git merge는 주로 깃허브하는데 만약 내가 쿠폰기능1, 기능2이렇게개발할수도있음
그래서 이러한것을 머지하는경우가생길 수 있다
따라서 merge할려면은 기준이 되는 브렌치로 가야한다 ex)coupon 브랜치를 main브랜치에 합치고싶다
하면은 main으로 가야한다

conflict는 하나의 커밋 브렌치가 합쳐지면서 이 충돌 커밋내역
그래서 이거를 해결해야함 : 컴퓨터가 어느것을 먼저해야할지 헷갈리기때문
그러면 coupon브렌치도 합쳐진곳을 바라고복 main도 합쳐진곳을 바라보게됨
```
![image](https://github.com/cwangg897/learning/assets/79621675/bd09db8d-bce7-4506-b9c4-02063b6a16b2) <br>


![image](https://github.com/cwangg897/learning/assets/79621675/f80d4240-ee15-4907-ba31-cbb5f9c23455)<br>
이그림과 같이 합쳐지면 하나의 곳을 바라보게됨 coupon도 합쳐진곳을 보고 master도 합쳐진곳을 보게됨 <br>
그런데 만약 합치고 coupon으로 계속하면 그림이 어떻게되는지 실습해보기 <br> 
merge를 master에서 하니까 충돌나면은 충돌난 상태에서 coupon으로 옮기질 못한다 <br>


![image](https://github.com/cwangg897/learning/assets/79621675/e95e3ee4-6552-432b-bcbc-c65c1a2eb823) <br>
충돌나도 어차피 충돌난  한곳을 바라보게됨

