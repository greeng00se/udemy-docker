### Build

- docker build -t feedback-node .

### 1. 볼륨을 사용하지 않아 컨테이너에서 저장된 파일이 영구 저장이 되지 않음

- docker run -p 3000:80 -d --name feedback-app --rm feedback-node

### 2. 볼륨 추가(오류)

- Dockerfile에 다음과 같이 설정하고 실행 -> 오류 발생
- 익명 볼륨을 사용했기 때문
- VOLUME 컨테이너 내부 위치
    - VOLUME ["/app/feedback"]

### 3. Named Volume

- docker run -p 3000:80 -d --name feedback-app -v feedback:/app/feedback --rm feedback-node 

### 4. 바인드 마운트(오류)

- docker run -p 3000:80 -d --name feedback-app -v feedback:/app/feedback -v "/Users/greeng00se/Documents/learn-docker/data-volumes-01-starting-setup:/app" --rm feedback-node  

### 5. 바인드 마운트
docker run -p 3000:80 -d --name feedback-app -v feedback:/app/feedback -v "/Users/greeng00se/Documents/learn-docker/data-volumes-01-starting-setup:/app" -v /app/node_modules --rm feedback-node

### 6. READONLY(오류 이렇게 설정한다면 내부 앱도 쓰기 불가)
docker run -p 3000:80 -d --name feedback-app -v feedback:/app/feedback -v $(pwd):/app:ro -v /app/node_modules --rm feedback-node

### 7. READONLY(내부 앱이 사용하는 폴더는 익명 볼륨을 이용하여 쓰기설정할 수 있게 함)
docker run -p 3000:80 -d --name feedback-app -v feedback:/app/feedback -v $(pwd):/app:ro -v /app/node_modules -v /app/temp --rm feedback-node

### 8. env --env or -e
docker run -p 3000:8000 -e PORT=8000 -d --name feedback-app -v feedback:/app/feedback -v $(pwd):/app -v /app/node_modules -v /app/temp --rm feedback-node

### 9. use .env
docker run -p 3000:8000 --env-file .env -d --name feedback-app -v feedback:/app/feedback -v $(pwd):/app:ro -v /app/node_modules -v /app/temp --rm feedback-node