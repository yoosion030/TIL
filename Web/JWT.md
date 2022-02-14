# JWT( Json Web Token )란?

## 로그인은 어떻게 이루어지나??

1. 세션 `id`를 이용하는 방식
   ![](https://media.vlpt.us/images/yaytomato/post/0a2cbabb-4ba8-4325-91e1-e0efc992dfd2/%E1%84%89%E1%85%A6%E1%84%89%E1%85%A7%E1%86%AB%20%E1%84%8B%E1%85%B2%E1%84%8C%E1%85%A5%20%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC.png)

   **동작 과정**

   1. 유저가 로그인 시도를 한다.
   2. 서버에서는 세션을 생성한다.
   3. 그 세션의 `id`를 클라이언트에 보낸다.
   4. 클라이언트는 서버에서 온 `id`를 클라이언트에 저장해둔다.
   5. 인증이 필요한 데이터를 가져올 때 서버에 `id`값을 보낸다.
   6. 서버는 그 `id`를 통해 세션을 불러와 유효한지 확인한다.

2. `JWT`를 이용하는 방식

**accessToken**
**refreshToken**  
accessToken은 유효기간이 짧기때문에 로그인을 자주해야되고 계속 새로은 token을 발급받아야 하므로 매우 부편합니다. 그러나 유효기간을 늘린다고 하면, 토큰을 탈취당했을 때 보안에 더 취약해지게 됩니다. "그러면 유효기간을 짧게하면서 좋은 방법이 있지 않을까?"라는 질문의 답이 바로 **refreshToken**입니다.

refreshToken은 accessToken과 똑같은 형태의 JWT입니다. 처음에 로그인을 완료했을 때 accessToken과 동시에 발급되는 refreshToken은 긴 유효기간을 가지면서, accessToken이 만료되었을 떼 새로 발급해주는 열쇠가 됩니다. 

refreshToken의 유효기간은 2주, accessToken의 유효기간은 1시간이라 하겠습니다. 사용자는 API 요청을 신나게 하다가 1시간이 지나게 되면, 가지고 있는 Access Token은 만료됩니다. **그러면 Refresh Token의 유효기간 전까지는 Access Token을 새롭게 발급받을 수 있습니다.**  (2주 후에는 다시 로그인을 하요 새로운 token을 발급해야한다는 소리)

 

   ![](https://media.vlpt.us/images/yaytomato/post/94ff189f-46fb-4901-bb7f-06d7b2154834/JWT%20%E1%84%8B%E1%85%B2%E1%84%8C%E1%85%A5%20%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC.png)

**동작 과정**

   1. 유저가 로그인을 시도한다.
   2. 서버가 인증 정보를 보내주는데, 암호화나 시그니처 추가가 가능한 데이터 패키지안에 인증정보를 담아 보내준다. ( 이 패키지가 JSON Web Token 즉 JWT 이다 )
   3. 담기는 정보 중 `accessToken`과 `refreshToken`이 있는데 이 정보들을 클라이언트에 저장해둔다.
   4. 이 accessToken을 유저에게만 보여줄 수 있는 정보에 접근할 때 서버에 보낸다.
   5. 서버는 그 토큰이 유효한지 확인한다.

   ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F99DB8C475B5CA1C936)

**자세한 과정**

    1.유저가 로그인을 시도한다.  
    2.서버에서는 회원DB에서 값을 비교한다.  
    3~4. 로그인이 완료가 되면 `accessToken`, `refreshToken`을 발급한다. 일반적으로 회원DB에 `refreshToken`을 저장해둔다.  
    5.사용자는 `refreshToken`을 안전한 저장소에 저장 후 `accessToken`을 헤더에 실어 요정을 보낸다.  
    6~7.`accessToken`을 검증하여 이에 맞는 데이터를 보낸다.  
    8.`accessToken` 토큰이 만료가 되었다.  
    9.사용자는 이전과 동일하게 `accessToken`을 헤더에 실어 요청을 보낸다.  
    10~11.서버는 `accessToken`이 만료됨을 확인한다.  

    **Access Token 만료가 될 때마다 계속 과정 9~11을 거칠 필요는 없습니다.  

    사용자(프론트엔드)에서 Access Token의 Payload를 통해 유효기간을 알 수 있습니다. 따라서 프론트엔드 단에서 API 요청 전에 토큰이 만료됐다면 바로 재발급 요청을 할 수도 있습니다.**  

    12.사용자는 `refreshToken`과 `accessToken`을 함께 서버로 보낸다.    
    13.**서버는 받은 `accessToken`이 조작되지 않았는지 확인한 후, `refreshToken`과 사용자의 DB에 저장되어 있던 `refreshToken`을 비교합니다. token이 동일하고 유효기간도 지나지 않았다면 새로은 `accessToken`을 발급해준다.**  
    14.서버는 새로는 `accessToken`을 헤더에 실어 다시 API요청을 진행합니다.  


## 단점
1. 구현이 복잡하다. 클라이언트, 서버 모두
2. accessToken이 만료될 때마다 새롭게 발급하는 과정에서 생기는 HTTP요청 횟수가 많다.

## 장점
1. 기존의 Access Token만 있을 때보다 보안상 안전하다.