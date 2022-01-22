
#제이쿼리 함수 attr와 prop의 차이

	1.attr	
	*HTML의 속성 취급
	*$("#아이디").attr("태그요소",넣어줄값)또는$("#아이디").attr("태그요소") => 태그 속성의 값을 세팅 또는 조회
	*속성이 없는 경우 undefined로 출력
	
	*element 요소가 갖는 속성값이나 정보를 조회(style,scr,value,rowspan...)하고 세팅함
	
	2.prop	:JavaScript 프로퍼티 취급
	*$("#아이디").prop("태그요소")	=> 태그 속성의 상태를 출력 true,false
	*속성이 없는 경우 false
	
	*element 요소가 갖는 상태(checked)를 제어 ; form 요소의 disa