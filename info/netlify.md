# netlify

netlify에 React 프로젝트를 배포하였을 때, 다른 페이지에서 새로고침을 하면 http 에러가 난다.

그럴때는 두가지 방법이 있다.
첫번째로는 public폴더에 \_redirect라는 아무 확장자가 없는 파일을 만들고,

```
/* /index.html 200
```

라고 적어준다.

netlify.toml이란 파일과 내용물로는

```
[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200
```

을 넣어준다.

둘다 새로고침이나, 메인페이지의 도메인이 아닌 다른곳으로 접속하려했을때 index.html의 루트부터 거치고 오게 해주는 것이다.
