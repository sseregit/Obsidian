`
`keytool -genkeypair -alias localhost -keyalg RSA -keysize 2048 -storetype PKCS12 -keystore edge.p12 -validity 3650`

적어도 책에서 제공한 인증서 만드는법과

```yaml
server.ssl:  
  key-store-type: PKCS12  
  key-store: classpath:keystore/edge.p12  
  key-store-password: wkddustlr  
  key-alias: localhost
```
을 설정하면 자체 서명된 인증서로 만들수 있지만 브라우저나 다른 클라이언트는 신뢰하지 않아 경고창이 뜬다.

알아두는것이 유익할듯!