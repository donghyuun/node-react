# NodeReact
<회원가입>

회원가입 페이지에서 post 로 보낸 회원가입 정보를 받으면, 미리 생성한 유저 모델을 이용해 받은 정보로 
새로운 유저 인스턴스를 생성한다. 생성된 유저 인스턴스를 db에 저장하기 전에 bcrypt 패키지를 이용하여 
비밀번호를 암호화하여 db 에 저장한다;

<로그인>

로그인 페이지에서 post 로 보낸 로그인 정보를 받으면 db에 같은 이메일을 가진 객체가 있는지 확인하고 있다면 가져온다.
가져온 객체의 비밀번호와 받은 로그인 정보의 비밀번호가 같은지 확인하고 맞다면 해당 객체의 _id 와 jwt 패키지를 
이용해 토큰을 암호화하여 생성하고, db 의 해당 객체에 추가한 후 저장한다. 추가로 클라이언트 쿠키에도 토큰을 저장해준다.

<권한확인>

권한확인 페이지에 get 했을 경우 서버의 권한확인 미들웨어가 실행된다. 
(미들웨어에서는)
미들웨어에서는 해당 유저가 로그인 했는지 하지 않았는지 확인한다. 확인하는 방법으로
클라이언트 쿠키에서 토큰을 가져온 뒤 복호화를 하여 _id 를 확인한 뒤, db 에서 해당 _id 를 가진 객체를 찾고,
그 객체가 가진 토큰과 클라이언트 쿠키의 토큰이 동일한지 비교한다. 동일하다면 req 에 해당하는 객체의 정보를 입력한다.

<로그아웃>

db 에서 req 에 들어있는 _id 와 동일한 객체를 찾은 뒤, 해당 객체의 토큰을 삭제해준다. 
