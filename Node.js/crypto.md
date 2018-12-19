# crypto 단방향 암호화(해시)
* 다양한 방식의 암호화를 돕는 모듈
* 비밀번호는 hash방식으로 암호화 해 복호화되지 않는 문자열을 만듭니다.
``` javascript
const crypto = require('crypto')
crypto.createHash('sha512') // sha512방식으로 hash를 만든다.
      .update('비밀번호')     // 암호화하고 싶은 비밀번호 추가
      .digest('base64')     // 출력
```
* 비밀번호를 복호화 할 필요 없다.
* 암호문(해시)을 저장한 후 사용자의 입력 비밀번호를 암호화한 것과 비교합니다.
* 우연의 경우로 동일한 암호문이 나오는 "비밀번호 충돌"이 발생할 수 있다.
* 그래서 Node에서는 좀 더 복잡한 방식을 제공한다.
```javascript

crypto.randomBytes(64, (err, buf) => {
    // buffer에 randomBytes가 들어있다.
    const salt = buf.toString('base64') // randomBytes base64 문자열로 만든다.
    // base64: buf를 문자열로 만드는 알고리즘 중 하나이다.
    // 해시 충돌 공격을 어렵게 하기위해 salt라는 문자열을 원래비밀번호에 추가하고 iteration 횟수를 높입니다.
    // salt는 암호화된 비밀번호와 같이 저장하시고, iteration은 1초가 걸릴때까지 올려주면 좋다.
    crypto.pbkdf2('비밀번호', salt, 12345, 64, 'sha512', (err, key) => {
        key.toString('base64')
        // key : 암호화된 key
    })
})
```

* 실무에서는 bcrypt, scrypt 등을 많이 사용한다.
---

# crypto 양방향 암호화
* 복호화 가능한 알고리즘 
```javascript
// 1. 암호화
const cipher = crypto.createCipher('aes-256-cbc', '열쇠') // 열쇠를 알아야 암호화, 복호화가 가능하다.
let result = cipher.update('비밀번호', 'utf8', 'base64') // 비밀번호, 인코딩, 결과 === utf8 비밀번호 문자열을 'base64'로 바꿔라
result += cipher.final('base64') // 암호화 마무리
 
 // 2. 복호화
const decipher = crypto.createDecipher('aes-256-cbc', '열쇠') // 똑같은 알고리즘 및 열쇠를 써야한다.
let result2 = decipher.update(result, 'base64', 'utf8') // 암호문, base64를 utf8로 바꿔라.
result2 += decipher.final('utf8')
```