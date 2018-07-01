


worker_process
worker_process는 워커 프로세스를 몇개 생성할 것인지를 지정하는 지시어다. 이 값이 1이라면 모든 요청을 하나의 프로세스로 실행하겠다는 의미인데, 여러개의 CPU 코어가 여러개 있는 시스템에서 이 값이 1이면 하나의 코어만으로 요청을 처리하게 되는 셈이다. 따라서 여러개의 코어가 있는 시스템이라면 이 값은 코어의 숫자만큼 지정하는 것이 바람직하다.


client_max_body_size
이 값은 업로드 할 수 있는 용량의 크기를 지정한다. 이 지시자의 기본값은 1MB인데, 더 많은 파일의 업로드를 허용하려면 이 값을 늘려줘야 한다. 아래의 설정은 10MB까지 업로드를 허용한다.


가상호스트를 지정하기 위해서는 nginx.conf 파일에 server 블록을 사용하면 된다. 하나의 호스트에서 하나의 웹서비스만을 운영한다면 이런 방식도 좋지만, 만약 하나의 호스트에서 복수의 서비스를 운영한다면 본 토픽의 말미에서 설명하는 include 방식을 이용할 것을 권장한다. 서버블록에 올 수 있는 주요 지시자는 아래와 같다.


server_name
server_name 지시어에는 (주로 도메인인) 호스트 명이 온다. server_name이 속해있는 server 블록이 해당 호스트명에 대한 설정이라는 것을 의미한다. 호스트명으로 올 수 값은 아래와 같다.




Upstream
Upstream 서버는 다른 말로 Origin 서버라고도 한다. 즉 여러대의 컴퓨터가 순차적으로 어떤 일을 처리 할 때 어떤 서비스를 받는 서버를 의미한다. 위의 그림에서 업스트림 서버는 PHP-FPM이 설치된 서버이고, 이 맥락에서 NGINX는 Downstream 서버라고 할 수 있다.

upstream 이름 {
    [ip_hash;]
    server host 주소:포트 [옵션];
    .....
}

옵션
옵션으로 올 수 있는 값은 아래와 같다.

ip_hash : 같은 방문자로부터 도착한 요청은 항상 같은 업스트림 서버가 처리 할 수 있게 한다.
weight=n : 업스트림 서버의 비중을 나타낸다. 이 값을 2로 설정하면 그렇지 않은 서버에 비해 두배 더 자주 선택된다.
max_fails=n : n으로 지정한 횟수만큼 실패가 일어나면 서버가 죽은 것으로 간주한다.
fail_timeout=n : max_fails가 지정된 상태에서 이 값이 설정만큼 서버가 응답하지 않으면 죽은 것으로 간주한다.
down : 해당 서버를 사용하지 않게 지정한다. ip_hash; 지시어가 설정된 상태에서만 유효하다.
backup : 모든 서버가 동작하지 않을 때 backup으로 표시된 서버가 사용되고 그 전까지는 사용되지 않는다.

Nginx가 제공하는 로드밸런싱 메서드
1. 라운드로빈(Round-robin)은 기본으로 사용하는 메서드로 모든 서버에 동등하게 요청을 분산한다.
upstream test_proxy {
    server web-01;
    server web-02;
}

2. least_conn은 연결이 가장 작은 서버로 요청을 보낸다.
upstream test_proxy {
    least_conn;
    
    server web-01;
    server web-02;
}

3. ip_hash는 클라이언트 IP주소를 기준으로 요청을 분배한다. IP주소가 같다면, 동일한 서버로 요청을 전송한다.
upstream test_proxy {
    ip_hash; 

    server web-01;
    server web-02;
}

location / {
    proxy_pass http://test_proxy;
}




nginx를 proxy서버로 사용할때 목적지서버의 404나 403 등의 에러응답코드를 다른것으로 변조하고 싶은경우가 있다.

이럴경우 아래의 코드를 삽입해서 proxy서버에서 직접 콘트롤 가능하게 할 수 있다.
proxy서버에서 특정페이지로 redirect 하게 하거나 여러가지 일을 할 수 있다.

***proxy_intercept_errors on;***

...

rewrite ^ /v1/AUTH_toastcam/$camera/thumbnail/$camera.jpg break;
proxy_pass http://swift_backend;
error_page 401 /was_updateToken;
error_page 404 =200 /resources/images/img_clip_make_err.png



internal
internal은 특정 location이 nginx 내부 요청에서만 유효하고 외부 요청에서는 404로 응답하도록 한다. 에러 페이지 등에 사용하면 좋다.


error_page 404 /404.html;
location  /404.html {
  internal;
}


auth_request /was_auth;
auth_request_set $X_Auth_Token $upstream_http_X_Auth_Token;
proxy_set_header X-Auth-Token $X_Auth_Token;
 
rewrite ^/(.*)$ /v1/AUTH_toastcam/$1 break;
proxy_pass http://swift_backend;


http://whatisthenext.tistory.com/123
https://extrememanual.net/nginx