<h1> Access / Refresh Token 재발급 원리 </h1>
 
<h3> 1. 기본적으로 로그인 같은 과정을 하면 Access Token과 Refresh Token을 모두 발급한다.</h3> 

- 이때, Refresh Token만 서버측의 DB에 저장하며, Refresh Token과 Access Token을 쿠키 혹은 웹스토리지에 저장한다.

<h3> 2. 사용자가 인증이 필요한 API에 접근하고자 하면, 가장 먼저 토큰을 검사한다.</h3> 

- 이때, 토큰을 검사함과 동시에 각 경우에 대해서 토큰의 유효기간을 확인하여 재발급 여부를 결정한다.

```
case1 : access token과 refresh token 모두가 만료된 경우 → 에러 발생 (재 로그인하여 둘다 새로 발급)
case2 : access token은 만료됐지만, refresh token은 유효한 경우 →  refresh token을 검증하여 access token 재발급
case3 : access token은 유효하지만, refresh token은 만료된 경우 →  access token을 검증하여 refresh token 재발급
case4 : accesss token과 refresh token 모두가 유효한 경우 → 정상 처리
```

<h3> Tip 😃 </h3>

```
[refresh token을 검증하여 access token 재발급]
- 클라이언트(쿠키, 웹스토리지)에 저장되어있는 refresh token과 서버 DB에 저장되어있는 refresh token 일치성을 확인한 뒤 access token 재발급한다.
[access token을 검증하여 refresh token 재발급]
- access token이 유효하다라는 것은 이미 인증된 것과 마찬가지니 바로 refresh token 재발급한다. 
```
<h3> 3. 로그아웃을 하면 Access Token과 Refresh Token을 모두 만료시킨다.</h3> 

<h3> Refresh Token 인증 과정 ✨ </h3>

![image](https://user-images.githubusercontent.com/74536458/204080266-0d23bf73-9501-407a-82a8-35ed908c0206.png)

<h5> 
  
  1. 사용자가 ID , PW를 통해 로그인.

  2. 서버에서는 회원 DB에서 값을 비교

  3~4. 로그인이 완료되면 Access Token, Refresh Token을 발급한다. 이때 회원DB에도 Refresh Token을 저장해둔다.

  5. 사용자는 Refresh Token은 안전한 저장소에 저장 후, Access Token을 헤더에 실어 요청을 보낸다.

  6~7. Access Token을 검증하여 이에 맞는 데이터를 보낸다.

  8. 시간이 지나 Access Token이 만료됐다.

  9. 사용자는 이전과 동일하게 Access Token을 헤더에 실어 요청을 보낸다.

  10~11. 서버는 Access Token이 만료됨을 확인하고 권한없음을 신호로 보낸다.
</h5>
<h3> Tip 😃 </h3>

```
Access Token 만료가 될 때마다 계속 과정 9~11을 거칠 필요는 없다.
사용자(프론트엔드)에서 Access Token의 Payload를 통해 유효기간을 알 수 있다.
따라서 프론트엔드 단에서 API 요청 전에 토큰이 만료됐다면 곧바로 재발급 요청을 할 수도 있다.
```
<h5>
  
  12. 사용자는 Refresh Token과 Access Token을 함께 서버로 보낸다.

  13. 서버는 받은 Access Token이 조작되지 않았는지 확인한후, Refresh Token과 사용자의 DB에 저장되어 있던 Refresh Token을 비교한다. Token이 동일하고 유효기간도 지나지 않았다면 새로운 Access Token을 발급해준다.

  14. 서버는 새로운 Access Token을 헤더에 실어 다시 API 요청 응답을 진행한다. 
</h5>

<h3> 📭 nestjs 기준 RefreshToken 인증 </h3>

``` javascript
    try {
      const verify = this.jwtService.verify(token.refreshToken, {
        secret: this.config.get('JWT_SECRET'),
      });
      if (verify) {
        const userData = await this.agencyMemberRepository.findOne({
          where: { uid: verify.uid, userPwd: verify.secretString },
        });

        const payload = { uid: userData.uid, secretString: userData.userPwd };
        const accessToken = await this.jwtService.sign(payload, {
          expiresIn: this.config.get('JWT_PUBLISH'),
          secret: this.config.get('JWT_SECRET'),
        });
        return {
          accessToken: accessToken,
          refreshToken: token.refreshToken,
        };
      }
    } catch (e) {
      switch (e.message) {
        // 토큰에 대한 오류를 판단합니다.
        case 'invalid signature':
          throw new HttpException(
            {
              errCode: 'xxx',
              errMsg: '유효하지 않은 토큰입니다.',
            },
            401,
          );

        case 'jwt expired':
          throw new HttpException(
            {
              errCode: 'xxx',
              errMsg: '토큰이 만료되었습니다.',
            },
            410,
          );
        default:
          throw new HttpException(
            {
              errCode: 'xxx',
              errMsg: '서버 에러입니다.',
            },
            500,
          );
      }
    }
```

출처 : https://inpa.tistory.com/entry/WEB-%F0%9F%93%9A-Access-Token-Refresh-Token-%EC%9B%90%EB%A6%AC-feat-JWT
