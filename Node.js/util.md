# Util

## util.deprecate(fn, msg[, code])
```javascript
const util = require('util')

// deprecate는 지원이 조만간 중단될 메서드임을 알려줄 때 사용합니다.
const dontuseme = util.deprecate((x, y) => {
    console.log(x + y) 
}, 'message')

dontuseme(1, 2) // DeprecationWarning 발생
```

## util.promiseify(original)
```javascript
const util = require('util')
const crypto = rquire('crypto')

// 중첩된 콜백 함수 
crypto.randomBytes(64, (err, buf) => {
    const salt = buf.toString('base64')
    crypto.pbkdf2('비밀번호', salt, 12345, 64, 'sha512', (err, key) => {
        key.toString('base64')
    })
})

const randomBytesPromise = util.promiseify(crypto.randomBytes)
const pbkdf2Promise = util.promiseify(crypto.pbkdf2)
 
randomBytesPromise(64)
    .then((buf) => {
        const salt = buf.toString('base64')
        return pbkdf2Promise('비밀번호', salt, 12345, 64, 'sha512')
    })
    .then((key) => {

    })
    .catch((err) => {
        console.log(err)
    })

(async () => {
    const buf = await randomBytesPromise(64)
    const salt = buf.toString('base64')
    const key = await pbkdf2Promise('비밀번호', salt, 12345, 64, 'sha512')
    console.log('password', key.toString('base64'))
})() 

// util.callbackify(original) : promise된 것을 다시 callback으로 바꿔준다.
```
