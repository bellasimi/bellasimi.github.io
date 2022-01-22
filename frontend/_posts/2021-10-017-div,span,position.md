# div와 span의 차이

div는 값이 없어도 display 기본값이 block이라서 영역이 한칸씩 설정되지만
span은 display 기본값이 inline이라서 값이 없으면 영역이 없고 값을 입력시에도 값이 들어간 부분만 일렬로 영역화 된다.

이 아이들의 display를 바꾸면 영역이 달라진다. 

display: inline-block으로 하면 한줄에 일렬로 영역을 둘 수 있다.

position의 경우 

'''

div {
  left: 20px;
  top: 20px;
}

'''
을 띄우고 싶은데 그냥 저렇게만 쓰면 css적용이 되지 않는다. 
왜냐하면 기본값 position이 static이기 때문이다. 

변화를 주고 싶다면 다른 설정을 줘야된다. 

### 1. 만약 현재 div의 위치를 기준으로 저렇게 띄우고 싶다면, relative를 

### 2. 상위 div를 기준으로 저렇게 띄우고 싶다면, absolute를

### 3. page를 기준으로 저렇게 띄우고 싶다면, fixed를

### 4. scroll을 할 때도 원래 자리에 있기를 바란다면, sticky를 쓰면 된다. 


# css호환가능 여부 


항상 모든 브라우저에서 호환이 되는지 확인을 해야된다. 
can i use.com을 가면 확인이 가능하다. 

internet explorer 지원 안되는거 많은데 어짜피 세계적으로 1.5%만 사용하는거라 외국에서도 개발할 떄 무시함
다만, 엣지의 경우 postcss같은 프레임워크를 쓰면 prefix같은걸 넣어서 버전에 맞게 수정해주기도... 
