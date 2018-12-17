# console 객체 
* console 객체에는 많이 흔히 쓰는 .log 말고도 다양한 기능들이 있다.
* console.time('시간') / console.timeEnd('시간') : 실행 시간을 체크
    ```javascript
    console.time('시간')
    for(var i=0; i<100; i++) {
        continue;
    }
    console.timeEnd('시간')
    > 시간: 0.01416015625ms
    ``` 
* console.dir(object) : object가 보기 좋은 console
* console.trace() : 실행된 함수를 추적할 수 있는 console
