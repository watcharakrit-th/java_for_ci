mvn clean install -U
mvn clean verify sonar:sonar
curl -u admin:admin -X POST "http://localhost:9000/api/user_tokens/generate?name=maven-scan"


mvn clean verify sonar:sonar \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.token=squ_4584aa57a777d793f92ad20ebbf68a5b6a034bf9







docker run -d --name sonarqube -p 9000:9000 sonarqube:community
export SONAR_TOKEN=$(curl -s -u admin:admin -X POST "http://localhost:9000/api/user_tokens/generate?name=maven-scan-2" | jq -r '.token')
echo $SONAR_TOKEN
docker run -d --name jenkins   -p 8080:8080 -p 50000:50000   -v jenkins_home:/var/jenkins_home   jenkins/jenkins:lts


docker compose build --no-cache jenkins