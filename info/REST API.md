# `REST API란?`

`REST`란 어떤 자원에 대해 CRUD(Create, Read, Update, Delete) 연산을 수행하기 위해 URI(Resource)로 요청을 보내는 것으로, Get, Post 등의 방식(Method)을 사용하여 요청을 보내며, 요청을 위한 자원은 특정한 형태(Representation of Resource)으로 표현됩니다. 그리고 이러한 REST 기반의 API를 웹으로 구현한 것이 RESTful API입니다. </br>

REST란 어떤 자원에 대해 CRUD 연산에 대한 요청을 할 때, 요청을 위한 Resource(자원, URI)와 이에 대한 Method(행위, POST) 그리고 Representation of Resource(자원의 형태, JSON)을 사용하면 표현이 명확해지므로 이를 REST라 하며, 이러한 규칙을 지켜서 설계된 API를 Rest API 또는 Restful한 API라고 합니다. 그리고 위에서 살짝 언급하였듯이, 이러한 Rest API는 Resource(자원), Method(행위), Representation of Resource(자원의 형태)로 구성됩니다. </br>

GET은 CRUD중에서 READ, POST는 CREATE, DELETE는 DELETE, PUT과 PATCH는 둘다 UPDATE에 관련된 메서드이지만, PUT은 수정하지 않을 내용도 같이 보내주어야합니다. 그렇지않으면 null혹은 default 값 처리가 된다. PATCH는 원하는 내용만 수정이 가능합니다. OPTIONS 는 리소스의 사용가능한 인터낵션을 기술한 메타데이터를 가져오는데 사용합니다.
