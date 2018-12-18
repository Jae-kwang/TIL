# path
* path.sep : 경로 구분자
* path.delimiter : 환경변수 구분자
* path.dirname(__filename) : 파일 경로
* path.extname(__filename) : 파일 확장자 
* path.basename(__filename) : 파일명
* path.parse(__filename) : 위의 3개를 한번에 가져옴
* path.format() : .parse()로 나온 결과 object 와 동일하 구조를 하나로 합쳐줌
* path.normalize(경로) : 정상적인 path로 바꿔줌
* path.isAbsolute(경로) : 절대경로 여부 판단
* path.relative(경로A, 경로B) : 첫변째 경로에서 두번째 경로로 가는 상대경로를 보여줌
* path.join(경로A, 경로B, ...) : 절대 경로를 무시하고 합침
  * 조각난 경로를 하나로 합침
* path.resolve(경로A, 경로B, ...) : 절대 경로를 고려하고 합칩
  * '/'있으면 그냥 절대경로로 생각함
* 절대 경로를 절대경로로 인식하고자 한다면 Resolve를 그게 아니라면 join을 쓴다.