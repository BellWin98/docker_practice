FROM openjdk:11 as stage1

WORKDIR /app

# gradle 빌드 시에 필요한 파일들을 workdir로 copy
# 폴더는 폴더 이름 그대로 도커 workdir에 copy
# /app/gradlew 파일, gradle 폴더, build.gradle 파일 ...
# COPY gradlew .
# COPY gradle gradle
# COPY build.gradle .
# COPY settings.gradle .
# COPY src src
COPY . .

# /app/build/libs/*.jar 파일을 아래 명령어를 통해 생성
RUN ./gradlew bootJar

# 새로운 work stage 시작, 기존 스테이지는 자동으로 사라진다.
FROM openjdk:11

WORKDIR /app

# 왼쪽이 stage1, 오른쪽이 도커 두번째 stage
COPY --from=stage1 /app/build/libs/*.jar app.jar

# CMD 또는 ENTRYPOINT를 통해 컨테이너 실행
ENTRYPOINT [ "java", "-jar", "app.jar" ]