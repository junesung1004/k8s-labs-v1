# Step 1: Build jar file
FROM gradle:8.3-jdk17 AS builder

WORKDIR /app

# 종속성 캐싱을 위해 먼저 설정 파일만 복사
COPY build.gradle settings.gradle /app/
RUN gradle build --no-daemon || true

# 전체 소스 복사 후 빌드
COPY . /app
RUN gradle clean bootJar --no-daemon



# Step 2: 실행 이미지
FROM openjdk:17-jdk-slim

WORKDIR /app

COPY --from=builder /app/build/libs/*.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]