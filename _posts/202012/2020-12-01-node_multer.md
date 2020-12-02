---
title:  "[Node.js] multer"
excerpt: "파일 업로드 모듈 multer 사용법"

categories:
  - Javascript
  - Node.js

last_modified_at: 2020-12-01T18:00:00
---

- 웹 클라이언트에서 `multipart/form-data`로 인코딩하는 form을 통해 서버로 파일을 업로드
- Multer는 파일 업로드가 필요할 때, `multipart/form-data`를 쉽게 다룰 수 있는 express, node.js를 위한 미들웨어

## API
### File information 
- `fieldname` : form의 field name
- `originalname` : 클라이언트 로컬에서 업로드한 파일의 이름
- `encoding` : 파일의 encoding type
- `mimetype` : 파일의 Mime type
  - ex) `image/jpeg`, `image/png` 등
- 그외 `size`, `destination`등이 존재

### multer(opts)
- multer는 options object를 가질 수 있음
- 가장 기본적인 것이 어디에 업로드를 할지 경로를 정하는 `dest` property
- option object가 없으면 disk가 아닌 memory에 저장됨
- `dest` or `storage` : 파일을 저장할 경로
- `fileFilter` : 어떤 파일을 허가할지 제어하는 필터
- `limits` : 업로드되는 데이터의 용량 제한
- `preservePath` : 파일의 단순 이름 대신 full path를 유지

### .single(fieldname)
- 하나의 파일만 받아들이는 설정
- `req.file`에 저장

### .array(fieldname[, maxCount])
- 여러 개의 파일을 받아들이는 설정
- maxCount로 개수 제한
- `req.files`에 저장

### .none()
- 순수 text만 받아들이는 설정

----

### storage - DiskStorage
- 디스크에 파일을 저장하기 위한 컨트롤
- `destinaion` / `filename` 두 가지 옵션 사용

```js
var storage = multer.diskStorage({
  destination: function (req, file, cb) {
    cb(null, '/tmp/my-uploads')
  },
  filename: function (req, file, cb) {
    const uniqueSuffix = Date.now() + '-' + Math.round(Math.random() * 1E9)
    cb(null, file.fieldname + '-' + uniqueSuffix)
  }
})

var upload = multer({ storage: storage })
```

### fileFilter
- 어떤 파일이 들어오면 스킵할지, 패스할지 필터링하는 역할

```js
function fileFilter (req, file, cb) {

  // The function should call `cb` with a boolean
  // to indicate if the file should be accepted

  // To reject this file pass `false`, like so:
  cb(null, false)

  // To accept the file pass `true`, like so:
  cb(null, true)

  // You can always pass an error if something goes wrong:
  cb(new Error('I don\'t have a clue!'))

}
```

----


## Example (based on express)

- multer 모듈 인스톨

```
npm install multer
```

- 모듈 불러오기
- storage, filter 정의

```js
const multer  = require('multer');

// 파일을 업로드할 폴더를 미리 만들기,
// 또는 아래와 같이 dest 옵션으로 폴더 생성
const upload = multer({dest : 'uploads/'});

...

const storage = multer.diskStorage({
    destination: (req, file, cb) => {
        cb(null, 'uploads');
    },
    filename: (req, file, cb) => {
        console.log(file);
        cb(null, Date.now() + path.extname(file.originalname));
    }
});
const fileFilter = (req, file, cb) => {
    // mime type 체크하여 이미지만 필터링
    if (file.mimetype == 'image/jpeg' || file.mimetype == 'image/png') {
        cb(null, true);
    } else {
        cb(null, false);
    }
}
upload = multer({ storage: storage, fileFilter: fileFilter });
```

- post 라우터에 upload를 미들웨어로 삽입

```js
//Upload route
app.post('/upload', upload.single('image'), (req, res, next) => {
    try {
        return res.status(201).json({
            message: 'File uploded successfully'
        });
    } catch (error) {
        console.error(error);
    }
});
```

- 클라이언트에서는 아래의 form을 이용하여 파일 업로드

```html
<form method="POST" action="/upload" enctype="multipart/form-data">
    <div> 
        <label>Select your profile picture:</label>
        <input type="file" name="image" />
    </div>
    <div> 
        <input type="submit" name="btn_upload_profile_pic" value="Upload" /> 
    </div>
</form>
```
----
**ref :**  
[Multer](https://github.com/expressjs/multer)  
[Uploading Files using Multer on Server in Node.js and Express.js](https://pprathameshmore.medium.com/uploading-files-using-multer-on-server-in-nodejs-and-expressjs-5f4e621ccc67)  

