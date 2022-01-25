---
title: 
categories:
tags:
- error
last_modified_at:
---

단위테스트를 하다가 다음과같은 오류를 만났습니다. 😥

![image](https://user-images.githubusercontent.com/79133602/136968936-2a03e560-e395-4db3-80f9-95dad6da258b.png)

원래, 
![image](https://user-images.githubusercontent.com/79133602/136969108-1367f81b-2847-46db-b9fd-1af85437b01e.png)

JpaRepository에 @Query 함수를 만들어서 그걸 확인하는 테스트를하던 중이었는데요.

![image](https://user-images.githubusercontent.com/79133602/136969055-88dc26cf-daa8-4abc-ace5-3c7ef4caf9fa.png)

쿼리문이나 테스트 코드상의 문제는 없는거 같아서 인터넷 서치를 해봤습니다. 

<br/>
<br/>
# 원인

lombok의 @Slf4j를 사용할 때 gradle에 의존설정을 추가하지 않아서 발생한 오류였습니다. 

<br/>
<br/>
# 해결

build.gradle 파일을 여시면 의존설정 목록이 보이는데 

![image](https://user-images.githubusercontent.com/79133602/136970020-0a3dd467-e4b2-4ba3-b0df-253b0d9f203a.png)

제가 체크한 저 두부분 모두 'org.projectlombok:lombok' 또는  'org.projectlombok:lombok: 자기버전' 로 바꿔주시면 됩니다. 


# ❗ 테스트코드에 쓸 땐 아래부분을 추가해주세요! 

![image](https://user-images.githubusercontent.com/79133602/136972718-13ef568b-ba97-4042-ae46-f151ed339eb4.png)






