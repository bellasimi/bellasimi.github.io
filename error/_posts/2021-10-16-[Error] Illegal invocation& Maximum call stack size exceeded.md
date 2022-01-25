---
title: 
categories:
tags:
- error
last_modified_at:
---

오늘 만난 에러들.. 


<br/>
# 💥 Uncaught TypeError: Illegal invocation

이 에러는 잘못된 변수를 입력했을때 나왔습니다. 아래처럼 addEventListener에 3번째 변수로 checkId의 변수값을 넣었기 때문입니다.

'''
checkIdBtn.addEventListener('click',checkId,id);
'''

원래 3번째 변수로는 option이 들어가야합니다. 
(1번은 이벤틍유형: test, click, scroll... 2번은 함수 참고로 1번은 ''안에 입력, 나머지는 그냥 입력해줍니다.)


사용 가능한 옵션은 다음과 같습니다.

> capture

DOM 트리의 하단에 있는 EventTarget 으로 전송하기 전에, 등록된 listener 로 이 타입의 이벤트의 전송여부를 나타내는 Boolean

> once

 리스너를 추가한 후 한 번만 호출되어야 함을 나타내는 Boolean입니다. true이면 호출할 때 listener 가 자동으로 삭제됩니다.

> passive

true일 경우, listener에서 지정한 함수가 preventDefault()를 호출하지 않음을 나타내는 Boolean입니다.

> mozSystemGroup

listener를 시스템 그룹에 추가해야함을 나타내는 Boolean 입니다. 오직 XBL 혹은 파이어폭스 브라우저의 chrome에서 실행되는 코드에서만 사용할 수 있습니다.

<br/>
<br/>
# 💥 Uncaught RangeError: Maximum call stack size exceeded


이에러는 ajax의 데이터값을 잣못 넣어줬을 때 나왔습니다. 
아래처럼 ajax data에 id:id라고 넣어줬는데 사실 id는 요소입니다. 요소의 값을 넣어주기 위해선 id:id.value라고 입력해야 했습니다. 😫


```

<script  src="https://code.jquery.com/jquery-latest.min.js"></script>
<script>
    $(document).ready(function(){
        const form = document.getElementById('memberForm');

        const id = document.getElementById('id');
        const pw = document.getElementById('pw');
        const name = document.getElementById('name');
        const yourEmail = document.getElementById('email');
        const tel = document.getElementById('tel');

        checkIdBtn.addEventListener('click',checkId);//클릭이벤트

    });//ready

    function checkId(){
        if(id.value==""){
                alert("id는 영문숫자혼합 4-12자로 입력해주세요!");
            }
            else{
                $.ajax({
                    type : "post",
                    async : "false",
                    url: "/checkId",
                    data: {
                        id: id.value

                    },
                    success : function(data, textStatus) {
                        console.log("ajax성공시: "+data.trim());
                        alert(data.trim());
                    },
                    error : function(data, textStatus) {
                        alert("에러가 발생했습니다!"+data);
                    }

                });//ajax*/

            }//조건문 끝
    }
</script>
```
