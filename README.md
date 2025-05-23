# CVE-2017-7529
[당승표(@portfolio10)](https://github.com/portfolio10/nginx)

## 요약
 - 본 실습은 Nginx 서버의 Range 요청 처리 과정에서 발생하는 캐시 취약점(CVE-2017-7529)을 재현하고, 취약점의 실제 동작
 - 취약점: Nginx Range 헤더 처리 오류로 인해 캐시된 데이터 노출 가능
 - 영향: 서버 캐시 파일의 민감 데이터 유출

## 환경 구성 및 실행
 - OS : Windows 10
 - Docker, Python
 1. 특정 디렉터리에 폴더 생성 
 2. Dockerfile, poc.py, docker-compose.yml 파일 생성
 3. 'docker compose up -d' 실행
 4. http://127.0.0.1:8080 에 접속하여 Nginx 실행 확인
 5. 'pip install requests' 를 통해 필요 라이브러리 설치
 6. 'python poc.py http://127.0.0.1:8080' 실행하여 결과 값 확인.

## 결과
![PoC 실행 결과](./result.png)

## 결론
 - CVE-2017-7529는 Nginx 서버가 Range 요청을 잘못 처리하여 발생하는 심각한 캐시 노출 취약점이다.
 - 공격자는 특정 Offset을 사용하여 민감 데이터를 유출할 수 있다.
 - 안전한 운영을 위해서는 Nginx 버전 업데이트, 캐시 관련 설정 강화, Range 요청에 대한 필터링 적용하는 것이 중요하다.[