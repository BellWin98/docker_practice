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

# .dockerignore에 불필요 파일 추가
COPY . .

# /app/build/libs/*.jar 파일을 아래 명령어를 통해 생성
RUN ./gradlew bootJar

# 새로운 work stage 시작, 기존 스테이지는 자동으로 사라진다.
FROM openjdk:11

WORKDIR /app

# 왼쪽이 stage1, 오른쪽이 도커 두번째 stage
COPY --from=stage1 /app/build/libs/*.jar app.jar

# docker run -d -p 8080:8080 ordering:v1 -v C:/Users/Playdata/tmp:/tmp
# volume을 잡아준다: 전체 host의 특정 경로와 매핑을 시킴
VOLUME /tmp

# CMD 또는 ENTRYPOINT를 통해 컨테이너 실행
ENTRYPOINT [ "java", "-jar", "app.jar" ]

# docker 실행 시 db정보를 환경변수로 주입
# application.yml db 정보에 평소에는 localhost로 실행했다가 도커 실행하면 아래 주소로 덮어쓰기 되게함
# docker run -d -p 8080:8080 -e SPRING_DATASOURCE_URL=jdbc:mariadb://host.docker.internal:3306/spring_order -v C:/Users/Playdata/tmp:/tmp ordering:v1