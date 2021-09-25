![image](https://user-images.githubusercontent.com/79133602/134349650-d70c558b-8cb2-4e79-8379-afa2909c3db6.png)

# 원인

고유값으로 지정해 둔 키에 중복값을 넣었기 때문에 에러가 발생한 것입니다. 

저같은 경우 회원테이블의 id를 고유값 설정해 뒀는데 그만 까먹고 다시 Insert를 하려다 해당 오류가 발생했습니다. Member 테이블을 조회해 보니 admin이란 id로 이미 가입이 된 것을 알 수 있습니다. 

![image](https://user-images.githubusercontent.com/79133602/134350253-370a0dbe-3b18-41d2-bb0a-efe78f45fe30.png)

<br/><br/><br/>


# 해결

기존의 값을 지우고 넣거나 중복값을 새로운 값으로 바꿔줍니다. 
<br/><br/><br/>

# 에러 메세지 

```
Error Code: 1062. Duplicate entry 'admin' for key 'member.UK_jp8ds32yg1soswx2rkiagm768'
```