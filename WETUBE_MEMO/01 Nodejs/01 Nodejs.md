# Nodejs

# Nodejs를 사용해야하는 경우

- Backend, Server를 빌드할 때 interactive하지 않은 정적웹사이트의 경우 어떠한 것을 사용해도 좋음
  - Javascript-Nodejs-Express
  - PHP-Laravel
  - Python-Django
- 거대한 프로젝트의 언어별 장단점을 고려해야함

### Nodejs를 사용해야하는 경우

- Javascrip를 좋아하고 Frontend와 Backend를 모두 Javascript로 만들고 싶을 때
- 빠르게 시작해야하며 거의 모든 것을 customize할 수 있는 경우
  - 상대적으로 기본이 갖춰진 있고 필요한 것들이 포함된 것을 원한다면 PHP-Laravel, Python-Django를 선택하는 것이 좋음
  - Python-Django는 많은 것이 들어있어 사용법을 배워야 함
  - Nodejs는 아무 것도 들어있지 않은 상태에서 시작하여 모든 것을 붙여나감
- 많은 데이터를 다루는 경우
  - Nodajs는 데이터를 다루는 성능이 아주 좋음(not Data Science)
  - DB생성및 삭제, 데이터 전송, 메세지 전송, 알람, 실시간처리 등
  - 채팅 기능을 만든다면 Python은 비동기 언어가 아니기 떄문에 실시간 처리를 할 element가 없어 nodejs가 필요
  - 실시간으로 위치를 업데이트하고 서버의 Scale를 다루어야 한다면 nodejs가 유리

## Nodejs를 사용하면 안되는 경우

- Javascript는 메모리나 램같은 하드웨어에 접근할수 없어 하드웨어파워를 사용하는 경우에는 적합하지 않음
  - DataScience
  - 이미지 압축, filter적용 및 저장
  - 비디오 인코딩, 디코딩
  - 바이트 단위의 작업

### Nodejs란?

- Javascript는 브라우저에 내장되어 있음
- Nodejs는 javascript를 브라우저 밖으로 가지고 나와 유저의 컴퓨터에서 사용할 수 있게 함
- 브라우저에 종속되어 있지 않아 Server, File System 등 다양한 작업이 가능

### Nodejs 설치 방법

- [Nodejs 홈페이지](https://nodejs.org/ko/)에서 설치
