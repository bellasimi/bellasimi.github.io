#intellij mysql 연동하는법 

1. 상단 메뉴바 View - Tool Windows - Databse 
2. 우측에 뜬 창에서 Database를 클릭
3. Database 메뉴에서 +을 누르고 - Datasource - MySQL을 선택
4. Database에 자신이 사용할 데이터 베이스이름은 입력한다.
	기억이 나지 않는 경우 mysql workbench에서 해당 계정 접속 후 show databases sql문을 입력해 확인한다.
	본인은 board라는 database를 새로 생성해 사용했다.
5. Data Sources and Drivers 에 각각 MySQL 유저명과 비번을 입력한다. 
6. URL은 자동으로 기입된다. 
7. 맨아래 Test connection을 누르면 mysql 연동 여부를 알려준다. 
	만약 실패한다면 테스트했던 url주소 끝부분 test? 뒤에  characterEncoding=UTF-8&serverTimezone=UTC를 추가로 입력한다.(타임존 설정)
	* 대소문자 오타에 유의하자!