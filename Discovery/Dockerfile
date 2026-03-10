# 1. 경량화된 OpenJDK 17 (또는 21) Alpine 이미지 사용
FROM eclipse-temurin:21-jre-alpine

# 2. 작업 디렉토리 설정
WORKDIR /app

# 3. 컨테이너 내부 시간을 한국 시간(KST)으로 동기화
RUN apk add --no-cache tzdata && \
    cp /usr/share/zoneinfo/Asia/Seoul /etc/localtime && \
    echo "Asia/Seoul" > /etc/timezone

# 4. Gradle 빌드 결과물인 jar 파일을 컨테이너의 app.jar로 복사
# 주의: GitHub Actions에서 빌드 후 생성된 jar 파일을 복사합니다.
ARG JAR_FILE=build/libs/*-SNAPSHOT.jar
COPY ${JAR_FILE} app.jar

# 5. Spring Boot 실행 명령어 (설정 파일 주입 및 메모리 최적화 옵션 추가 가능)
ENTRYPOINT ["java", "-Djava.security.egd=file:/dev/./urandom", "-jar", "/app/app.jar"]