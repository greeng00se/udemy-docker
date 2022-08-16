# 이미지 사용
FROM node

# Working Directory
WORKDIR /app

# 첫 번째는 컨테이너 외부, 두 번째는 컨테이너 내부
COPY package.json /app

# 내부에서 명령어 실행
# 명령어는 보통 루트에서 실행됨 그래서 WORKDIR을 설정해야 함
RUN npm install

COPY . /app

# 포트
# Documentation
EXPOSE 80

# 서버 시작
CMD ["node", "server.js"]