# 베이스 이미지로 Java 17을 포함한 Tomcat 9.0을 선택합니다.
FROM tomcat:9.0-jdk17-temurin

# 빌드 컨텍스트(프로젝트 루트)를 기준으로 WAR 파일 경로를 지정합니다.
COPY metadata-service/war/build/libs/war.war /usr/local/tomcat/webapps/ROOT.war

# Tomcat 서버가 사용하는 8080 포트를 외부에 노출합니다.
EXPOSE 8080
