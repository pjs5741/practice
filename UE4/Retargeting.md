# 리타기팅
애니메이션 리타기팅 은 스켈레톤 애셋을 공유하나 비율이 크게 다른 캐릭터간에 애니메이션을 재사용할 수 있도록 해 주는 기능입니다.



![1](https://user-images.githubusercontent.com/48274630/158174285-e9f9191b-e669-4ecc-ab44-1471d0770aee.PNG)

비율이 맞지않아 부자연스러운 모습

------


T본 포즈의 캐릭터 애셋을 드로그앤 드랍한 후에 기타에 Convert Scene Unit을 체크해 FBX Unit을 언리얼 엔진 Unit 크기로 맞춘다.

![2](https://user-images.githubusercontent.com/48274630/158175507-408ba1f1-223b-4aa7-9373-ec74753568e0.PNG)

그 후 애니메이션도 똑같이 Convert Scene Unit 체크 후 임포트 한다.



![ezgif com-gif-maker](https://user-images.githubusercontent.com/48274630/158176430-e7930559-33d8-4a14-a26c-e411316830a7.gif)

일단 애니메이션은 정상 작동하는것을 볼 수 있다.

---

이제 임포트한 캐릭터의 스켈레탈 메시를 더블 클릭하여 창을 열고 리타겟 매니저를 클릭 후에 릭 선택을 휴머노이드로 바꾼후에 자동 매핑을 클릭해준다.


![4](https://user-images.githubusercontent.com/48274630/158177251-79c413b6-5b34-4430-9e2f-a4fe8a4a0988.PNG)

자동 매핑후에 혹시 다른 부분이 있을지도 모르니 부분적으로 고쳐준다.

![5-1](https://user-images.githubusercontent.com/48274630/158180128-6014fb02-b0f7-488c-9e8f-281cecc6b749.PNG)
![5-2](https://user-images.githubusercontent.com/48274630/158180127-4df6a86f-41c1-4293-9965-598ca5b23409.PNG)
![5-3](https://user-images.githubusercontent.com/48274630/158180124-32bf4cb2-a6b7-4897-b331-31baa216d1fd.PNG)

그후 고급 표시로 가서

![5-4](https://user-images.githubusercontent.com/48274630/158180123-203a3617-7c70-4e96-8c33-6b3a227ea1be.PNG)
![5-5](https://user-images.githubusercontent.com/48274630/158180122-89e08f5f-365b-449a-97eb-72942c692858.PNG)
![5-6](https://user-images.githubusercontent.com/48274630/158180117-c04203d0-6f47-4959-9846-8caeeacdd8e6.PNG)
![5-7](https://user-images.githubusercontent.com/48274630/158180116-dbe118e4-20e5-422d-a40c-b25b07885ae8.PNG)
![5-8](https://user-images.githubusercontent.com/48274630/158180113-bf09b549-5c65-488e-9bb5-b59466a4a056.PNG)

아래 나머지는 none

![6](https://user-images.githubusercontent.com/48274630/158180111-acec7ce3-d59e-4f9b-9ee3-ee59a8a17696.PNG)

매핑이 끝났으면 기본으로 주어지는 스켈레탈 메시와 받아온 스켈레탈 메시가 포즈가 서로 다름으로 기본 스켈레탈메시의 어깨를 50도 팔꿈치 20도 손목을 10도 올려서 맞춰주고(믹사모사용기준) 포즈변경->현재 포즈사용 클릭


마지막으로 받아온 애니메이션을 우클릭->애님 에셋 리타깃-> 애님 에셋 복제후 리타깃 클릭

![7](https://user-images.githubusercontent.com/48274630/158180110-08f90c23-6ebb-4075-adac-5b075a7f1354.PNG)

리타깃 하면 끝난다.

![ezgif com-gif-maker (1)](https://user-images.githubusercontent.com/48274630/158180367-ee0e4854-a747-4e32-98ef-9d6d834893d1.gif)
