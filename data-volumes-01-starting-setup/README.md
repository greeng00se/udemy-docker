### 1. 볼륨을 사용하지 않아 컨테이너에서 저장된 파일이 영구 저장이 되지 않음

- docker run -p 3000:80 -d --name feedback-app --rm feedback-node

### 2. 볼륨 추가(오류)

- Dockerfile에 다음과 같이 설정하고 실행 -> 오류 발생
- 익명 볼륨을 사용했기 때문

# VOLUME 컨테이너 내부 위치
VOLUME ["/app/feedback"]