---
title:  "[Node.js] passport.js 사용법"
excerpt: "Express에서 사용자 인증을 위한 passport npm"

categories:
  - Javascript
  - Node.js

last_modified_at: 2020-10-06T18:00:00
---

### passport.js
- strategy에 따른 요청에 인증하기 위한 목적
- strategy:
  -  Local Strategy(passport-local)
  -  Social Authentication (passport-kakao, passport-twitter 등) 방식이 존재
- routes, DB 등을 mount하지 않고 application-level에서 결정할 수 있어 유연함
- API 동작 : 사용자가 passport에 인증 요청 -> passport는 인증 성공/실패시 어떤 제어를 할지 결정

### install
- `npm install passport passport-local express-session`

### structure
- passport 폴더를 만들어 index, strategy 작성
  - index : serialize, deserialize 작성, strategy 호출
  - strategy : local 및 외부 인증 전략 작성
- login check middleware 
  - login을 했는지에 대한 체크 미들웨어
  - isLoggedIn, isNotLoggedIn
- app에 passport 등록
  - `app.use(passport.initialize());`
  - `app.use(passport.session());`
  - passport 폴더의 index 호출 `passportConfig();`
- login route에 passport.authenticate 작성

## Example source code

#### localStrategy.js (/passport)

```js
const passport = require('passport');
const LocalStrategy = require('passport-local').Strategy;
const bcrypt = require('bcrypt');

const User = require('../models/user');

module.exports = () => {
  passport.use(new LocalStrategy({
    usernameField: 'email',
    passwordField: 'password',
    // session: true, // 세션에 저장 여부
    // passReqToCallback: false,
  }, async (email, password, done) => {
    try {
      const exUser = await User.findOne({ where: { email } });
      if (exUser) {
        const result = await bcrypt.compare(password, exUser.password);
        if (result) {
          done(null, exUser);
        } else {
          done(null, false, { message: '비밀번호가 일치하지 않습니다.' });
        }
      } else {
        done(null, false, { message: '가입되지 않은 회원입니다.' });
      }
    } catch (error) {
      console.error(error);
      done(error);
    }
  }));
};
```
- LocalStrategy
  - local 로그인을 위한 전략
  - usernameField/passwordField : 폼 필드 내 input의 name 태그
  - session: 세션 저장여부
  - passReqToCallback: express의 req 객체에 접근 가능 여부  
  true일 때, 뒤의 callback 함수에서 req 인자가 더 붙음  
  `(req, email, password, done) => {}`
  - id, pw가 전송되면, 콜백함수 실행
  - DB에서 비교하여 done 함수를 이용해 user 객체 전송, 또는 에러 리턴
  - done : verify callback
    - 첫 번째 인자: DB조회시 발생하는 서버 에러. 무조건 실패하는 경우에만 사용
    - 두 번째 인자: 성공했을 때 return할 값
    - 세 번째 인자: 사용자가 임의로 실패를 만들고 싶을 때 사용  
    ex) 위에서 비밀번호가 틀렸다는 에러

#### index.js (/passport)

```js
const passport = require('passport');
const local = require('./localStrategy');
const User = require('../models/user');

module.exports = () => {
  passport.serializeUser((user, done) => {
    done(null, user.id);
  });

  passport.deserializeUser((id, done) => {
    User.findOne({
      where: { id },
      include: [{
        model: User,
        attributes: ['id', 'nick'],
        as: 'Followers',
      }, {
        model: User,
        attributes: ['id', 'nick'],
        as: 'Followings',
      }],
    })
      .then(user => done(null, user))
      .catch(err => done(err));
  });

  local();
};

```
- serializeUser
  - strategy에서 로그인 성공시 호출하는 `done(null, user)` 함수의 두 번째 인자 user를 전달 받아 세션(req.session.passport.user)에 저장
  - 보통 세션의 무게를 줄이기 위해, user의 id만 세션에 저장
- deserializeUser
  - 서버로 들어오는 요청마다 세션정보를 실제 DB와 비교
  - 해당 유저 정보가 있으면 done을 통해 req.user에 저장
  - serializeUser에서 done으로 넘겨주는 user가 deserializeUser의 첫 번째 매개변수로 전달되기 때문에 둘의 타입은 항상 일치 필요

#### app.js (/)

```js
const passport = require('passport');

...

const passportConfig = require('./passport');

const app = express();
passportConfig(); // 패스포트 설정

...

app.use(cookieParser(process.env.COOKIE_SECRET));
app.use(session({
  resave: false,
  saveUninitialized: false,
  secret: process.env.COOKIE_SECRET,
  cookie: {
    httpOnly: true,
    secure: false,
  },
}));
app.use(passport.initialize());
app.use(passport.session()); // session 미들웨어 코드 뒤에 적용
```
- passport를 app에 등록
- passport 미들웨어는 세션 설정 후 등록 (initialize, session)

#### login check middleware (/routes/middleware.js)

```js
exports.isLoggedIn = (req, res, next) => {
  if (req.isAuthenticated()) {
    next();
  } else {
    res.status(403).send('로그인 필요');
  }
};

exports.isNotLoggedIn = (req, res, next) => {
  if (!req.isAuthenticated()) {
    next();
  } else {
    const message = encodeURIComponent('로그인한 상태입니다.');
    res.redirect(`/?error=${message}`);
  }
};
```
- 로그인을 꼭 해야되는 페이지와, 하지 않아도 되는 페이지 구분하는 미들웨어 작성
- [req.isAuthenticated](https://github.com/jaredhanson/passport/blob/a892b9dc54dce34b7170ad5d73d8ccfba87f4fcf/lib/passport/http/request.js#L74) 함수를 이용하여 요청에 인증여부 확인

#### login route (/routes/auth.js)

```js
router.post('/login', isNotLoggedIn, (req, res, next) => {
  passport.authenticate('local', (authError, user, info) => {
    if (authError) {
      console.error(authError);
      return next(authError);
    }
    if (!user) {
      return res.redirect(`/?loginError=${info.message}`);
    }
    return req.login(user, (loginError) => {
      if (loginError) {
        console.error(loginError);
        return next(loginError);
      }
      return res.redirect('/');
    });
  })(req, res, next); // 미들웨어 내의 미들웨어에는 (req, res, next)를 붙입니다.
});
```
- passport.authenticate()
  - strategy 설정하고, 인증 절차에 대한 콜백 작성
  - 인증 에러/실패 및 성공시 처리하는 부분 작성


----
**ref :**  
[인프런. Node.js 교과서](https://www.inflearn.com/course/node-js-%EA%B5%90%EA%B3%BC%EC%84%9C/dashboard)  
[passport](http://www.passportjs.org/)  
[Passport로 회원가입 및 로그인하기](https://www.zerocho.com/category/NodeJS/post/57b7101ecfbef617003bf457)
