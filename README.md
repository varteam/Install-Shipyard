# 사전 작업
우분투 설치 [https://github.com/varteam/Install-Ubuntu14.04]

도커 설치 [https://github.com/varteam/Install-Docker-On-Ubuntu]

# Install-Shipyard
shipyard 설치방법

도커 컨테이너로 바로 시작

    docker run --rm -v /var/run/docker.sock:/var/run/docker.sock shipyard/deploy start

<IP Address>:8080 접속시 화면이 나타남
초기 아이디/패스워드 = admin/shipyard

엔진을 추가해야 사용 가능함

# 엔진 추가
엔진을 추가 하기 위해서는 docker의 tcp 포트를 개방해야 함

    sudo vi /etc/default/docker

맨 아래에 추가

    DOCKER_OPTS="$DOCKER_OPTS -H tcp://0.0.0.0:2375 -H unix:///var/run/docker.sock"

docker 재실행

    sudo service docker restart

다시 <IP Address>:8080 접속 후 engines 에서 add
Docker 의 IP 와 이름 등등을 입력

완료

#아이디 및 패스워드 변경
docker run -it shipyard/shipyard-cli


    shipyard cli> shipyard login
    URL: http://<IP Address>:8080
    Username: admin
    Password: 
    # 로그인 하기
    
    shipyard cli> shipyard change-password
    Password: 
    Confirm: 
    # admin 비밀번호 변경
    
    shipyard cli> shipyard add-account -u *<계정 ID>* -p *<비밀번호>* -r admin
