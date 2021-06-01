# HTTP VS HTTPS

### HTTP

- **개념**
  - **H**yper**T**ext **T**ransfer **P**rotocol
  - w3 상에서 정보를 주고받을 수 있는 프로토콜
- **특징**
  - 클라이언트 서버 구조
    - Request Response 구조
    - 클라이언트는 서버에 요청을 보내고, 응답을 대기
    - 서버가 요청에 대한 결과를 만들어서 응답
  - 무상태 프로토콜(Stateless)
    - 서버가 클라이언트의 상태를 보존X
  - 비연결성(connectionsless)
    - HTTP는 기본이 연결을 유지하지 않는 모델
      - HTTP 지속 연결(Persistent Connections)로 문제 해결
- **약점**
  - 평문이기 때문에 도청 가능
    - HTTP를 사용한 리퀘스트나 리스폰스 통신 내용은 HTTP 자신을 암호화하는 기능은 없기 때문에 통신 전체가 암호화 되지는 않는다.
    - 평문(암호화되지 않은 메시지)으로 HTTP 메시지를 보내게 된다.
  - 통신 상대를 확인하지 않기 때문에 위장 가능
    - HTTP를 사용한 리퀘스트나 리스폰스에서는 통신 상대를 확인하지 않는다.
    - 리퀘스트를 보낸 서버가 정말로 URI에서 지정된 호스트인지 아닌지, 리스폰스를 반환한 클라이언트가 정말로 리퀘스트를 출력한 클라이언트인지 아닌지를 모른다.
  - 완전성을 증명할 수 없기 때문에 변조 가능
    - 정보가 정확한지 아닌지를 확인할 수 없다.
    - HTTP가 완전성을 증명할 수 없다는 뜻은 만약 리퀘스트나 리스폰스가 발신된 후에 상대가 수신할 때까지의 사이에 변조되었다고 하더라도 이 사실을 알 수 없다.

---

### HTTPS

- **개념**

  - **HTTP S**ecure
  - HTTP에 암호화나 인증 등의 구조를 더한 것을 HTTPS라고 부른다.

  - HTTPS는 HTTP 통신을 하는 소켄 부분을 SSL(Secure Socket Layer)이나 TLS(Transport Layer Security)이라는 프로토콜로 대체한다.
    - HTTP는 직접 TCP와 통신하지만 SSL을 사용한 경우에는 HTTP는 SSL와 통신하고 SSL이 TCP와 통신하게 된다.
    - SSL을 사용함으로써 HTTP는 HTTPS로서 암호화와 증명서와 안전성 보호를 이용할 수 있게 된다.

- **구조**

  - ![HTTPS](https://user-images.githubusercontent.com/66261552/120269680-3b1c3080-c2e3-11eb-991f-55a3c862a7dd.jpeg)
    1. 클라이언트가 Client Hello 메시지를 송신하면서 SSL 통신을 시작한다.
       - 메시지에 SSL 버전을 지정, 암호 스위트(Cipher Suite)로 불리는 리스트(사용하는 암호화의 알고리즘이나 키 사이즈 등) 등이 포함
    2. 서버가 SSL 통신이 가능한 경우에는 Sever Hello 메시지로 응답한다.
       - SSL 버전과 암호 스위트를 포함
    3. 서버가 Certificate 메시지를 송신한다.
       - 메시지에 공개키 증명서가 포함
    4. 서버가 Server Hello Done 메시지를 송신하여 초최의 SSL 네고시에이션 부분이 끝났음을 통지
    5. SSL의 최초 네고시에이션이 종료되면 클라이언트가 Client Key Exchange 메시지로 응답
       - 메시지에 통신을 암호화하는데 사용하는 Pre-Master secret 포함
    6. 클라이언트는 Change Cipher Spec 메시지를 송신한다.
       - 이 메시지는 이 메시지 이후의 통신은 암호키를 사용해서 진행한다는 것을 나타낸다.
    7. 클라이언트는 Finished 메시지를 송신한다.
       - 이 메시지는 접속 전체의 체크 값을 포함하고 있다.
    8. 서버에서도 Change Cipher Spec 메시지를 송신한다.
    9. 서버에서도 Finished 메시지를 송신한다.
    10. 서버와 클라이언트의 Finished 메시지 교환이 완료되면 SSL에 의해서 접속은 확립된다.
        - 이제부터는 HTTP 리퀘스트를 송신한다.
    11. 애플리케이션 계층의 프로토콜에 의한 통신
        - HTTP 리스폰스를 송신한다.
    12. 클라이언트가 접속을 끊는다. 접속을 끊을 경우에 close_notify 메시지를 송신한다. 그 후에 TCP FIN 메시지를 보내 TCP 통신을 종료한다.

---

### 참고자료

그림으로 배우는 Http & Network Basic

