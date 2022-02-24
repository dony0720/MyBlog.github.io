```python
var http = require('http');
var fs = require('fs');
var url = require('url');
var qs = require('querystring');

function templateHTML(title, list, body, control){
  return `
  <!doctype html>
  <html>
  <head>
    <title>WEB1 - ${title}</title>
    <meta charset="utf-8">
  </head>
  <body>
    <h1><a href="/">WEB</a></h1>
    ${list}
    ${control}
    ${body}
  </body>
  </html>
  `;
}


var app = http.createServer(function(request,response){
    var _url = request.url;
    var queryData = url.parse(_url, true).query;
    var pathname = url.parse(_url, true).pathname;
    if(pathname === '/'){
      if(queryData.id === undefined){
        fs.readdir('./data', function(error, filelist){
          var title = 'Welcome';
          var description = 'Hello, Node.js';
          var list = templateList(filelist);
          var template = templateHTML(title, list,
            `<h2>${title}</h2>${description}`,
            `<a href="/create">create</a>`
          );
          response.writeHead(200);
          response.end(template);
        });
      } else {
        fs.readdir('./data', function(error, filelist){
          fs.readFile(`data/${queryData.id}`, 'utf8', function(err, description){
            var title = queryData.id;
            var list = templateList(filelist);
            var template = templateHTML(title, list,
              `<h2>${title}</h2>${description}`,
              `<a href="/create">create</a> <a href="/update?id=${title}">update</a>
              <form action="delete_process" method="post">
                  <input type="hidden" name="id" value="${title}">
                  <input type="submit" value="delete">
                </form>`
            );
            response.writeHead(200);
            response.end(template);
          });
        });
      }
    } else if(pathname === '/create'){
      fs.readdir('./data', function(error, filelist){
        var title = 'WEB - create';
        var list = templateList(filelist);
        var template = templateHTML(title, list, `
          <form action="/create_process" method="post">`
          `<p><input type="text" name="title" placeholder="title"></p>
            <p>
              <textarea name="description" placeholder="description"></textarea>
            </p>
            <p>
              <input type="submit">
            </p>
          </form>
        `, '');
        response.writeHead(200);
        response.end(template);
      });
    } else if(pathname === '/create_process'){
      var body = '';
      request.on('data', function(data){
          body = body + data;
      });
      request.on('end', function(){
          var post = qs.parse(body); 
          var title = post.title;
          var description = post.description;
          fs.writeFile(`data/${title}`, description, 'utf8', function(err){ 
            response.writeHead(302, {Location: `/?id=${title}`});
            response.end(); 
          })
      });
    } else if(pathname === '/update'){
      fs.readdir('./data', function(error, filelist){
        fs.readFile(`data/${queryData.id}`, 'utf8', function(err, description){
          var title = queryData.id;
          var list = templateList(filelist);
          var template = templateHTML(title, list,
            `
            <form action="/update_process" method="post">
              <input type="hidden" name="id" value="${title}">
              <p><input type="text" name="title" placeholder="title" value="${title}"></p>
              <p>
                <textarea name="description" placeholder="description">${description}</textarea>
              </p>
              <p>
                <input type="submit">
              </p>
            </form>
            `,
            `<a href="/create">create</a> <a href="/update?id=${title}">update</a>`
          ); 
          response.writeHead(200);
          response.end(template);
        });
      });
    } else if (pathname === '/update_process'){
      var body = '';
      request.on('data', function(data){
          body = body + data; 
      });
      request.on('end', function(){
          var post = qs.parse(body);
          var id = post.id;
          var title = post.title;
          var description = post.description;
          fs.rename(`data/${id}`, `data/${title}`, function(error){ 
            fs.writeFile(`data/${title}`, description, 'utf8', function(err){
              response.writeHead(302, {Location: `/?id=${title}`});
              response.end();
            })
          });
      });
    }
    else if(pathname === '/delete_process'){
      var body = '';
      request.on('data', function(data){
          body = body + data;
      });
      request.on('end', function(){
          var post = qs.parse(body);
          var id = post.id;
          fs.unlink(`data/${id}`, function(error){ 
            response.writeHead(302, {Location: `/`});
            response.end();
          })
      });
    }
    else {
      response.writeHead(404);
      response.end('Not found');
    }
});
app.listen(3000);

```


```python
var http = require('http');
var fs = require('fs');
var url = require('url');
var qs = require('querystring');
```

외부 모듈을 가져오기 위해 require을 사용함 


```python
function templateHTML(title, list, body, control){
  return `
  <!doctype html>
  <html>
  <head>
    <title>WEB1 - ${title}</title>
    <meta charset="utf-8">
  </head>
  <body>
    <h1><a href="/">WEB</a></h1>
    ${list}
    ${control}
    ${body}
  </body>
  </html>
  `;
```

templateHTML이란 함수를 만듬 <br>
함수를 호출하게 되면 return 아래의 있는 코드를 실행한다 


```python
function templateList(filelist){
  var list = '<ul>';
  var i = 0;
  while(i < filelist.length){
    list = list + `<li><a href="/?id=${filelist[i]}">${filelist[i]}</a></li>`;
    i = i + 1;
  }
  list = list+'</ul>';
  return list;
}
```

filelist는 배열의 형식으로 되어있음 <br> 
list는 반복문을 사용해 filelist의 크기만큼 반복한다<br>
그러면 HTML,CSS,JavaScript 이렇게 각각의 리스트에 url이 생성된다.


```python
var app = http.createServer(function(request,response){
    var _url = request.url;
    var queryData = url.parse(_url, true).query;
    var pathname = url.parse(_url, true).pathname;
    if(pathname === '/'){
      if(queryData.id === undefined){
        fs.readdir('./data', function(error, filelist){
          var title = 'Welcome';
          var description = 'Hello, Node.js';
          var list = templateList(filelist);
          var template = templateHTML(title, list,
            `<h2>${title}</h2>${description}`,
            `<a href="/create">create</a>`
          );
          response.writeHead(200);
          response.end(template);
```

var queryData = url.parse(_url, true).query <br>
url 정보를 불러옴 ex) url.parse(_url, true).query = {id :'CSS'}<br>
<br>
var pathname = url.parse(_url, true).pathname; <br>
url 정보를 불러옴 ex) url.parse(_url, true).pathname = '/' <br>
단 path에는 쿼리스트링이 포함<br>
<br>
fs.readdir('./data', function(error, filelist){ <br>
파일 디렉토리 읽기 첫번째 인자로 파일 목록을 읽을 폴더('./data')를 가져온다<br>
콜백함수의 두번째 인자로 폴더의 파일목록(filelist)을 가져옴


```python
else {
        fs.readdir('./data', function(error, filelist){
          fs.readFile(`data/${queryData.id}`, 'utf8', function(err, description){
            var title = queryData.id;
            var list = templateList(filelist);
            var template = templateHTML(title, list,
              `<h2>${title}</h2>${description}`,
              `<a href="/create">create</a> <a href="/update?id=${title}">update</a>
              <form action="delete_process" method="post">
                  <input type="hidden" name="id" value="${title}">
                  <input type="submit" value="delete">
                </form>`
            );
            response.writeHead(200);
            response.end(template);
          });
        });
      }
```

fs.readFile('data/${queryData.id}', 'utf8', function(err, description){ <br>
data 디렉토리 안에 있는 queryData.id의 내용을 불러온다


```python
else if(pathname === '/create'){
      fs.readdir('./data', function(error, filelist){
        var title = 'WEB - create';
        var list = templateList(filelist);
        var template = templateHTML(title, list, `
          <form action="/create_process" method="post">`
          `<p><input type="text" name="title" placeholder="title"></p>
            <p>
              <textarea name="description" placeholder="description"></textarea>
            </p>
            <p>
              <input type="submit">
            </p>
          </form>
        `, '');
        response.writeHead(200);
        response.end(template);
      });
```

form action="/create_process" method="post"
post 방식 : 눈에 보이지 않는 방법으로 데이터를 전송 <br>
url에 정보가 담겨있을 수 있으므로 post 방식으로 데이터를 전송<br>
url에는 많은 데이터를 수용하지 않음 나중에 데이터가 잘릴 수가 있음 <br>
서버로부터 데이터를 가져올때는 GET 방식을 사용<br>
서버의 데이터 수정, 삭제, 생성을 할때는 반드시 post 방식<br>


```python
else if(pathname === '/create_process'){
      var body = '';
      request.on('data', function(data){
          body = body + data;
      });
      request.on('end', function(){
          var post = qs.parse(body);
          var title = post.title;
          var description = post.description;
          fs.writeFile(`data/${title}`, description, 'utf8', function(err){ 
            response.writeHead(302, {Location: `/?id=${title}`});
            response.end(); 
```

var post = qs.parse(body) -> body의 정보를 가져옴  ex) console.log(post) === title: ㅇㅇ , description : ㅇㅇ<br>
fs.writeFile(`data/${title}`, description, 'utf8', function(err) ->파일을 저장하는 방식<br>
response.writeHead(302, {Location: `/?id=${title}`})<br>
response.end() -> 리다이렉션 = 사용자를 다른 주소로 보내는것 


```python
else if(pathname === '/update'){
      fs.readdir('./data', function(error, filelist){
        fs.readFile(`data/${queryData.id}`, 'utf8', function(err, description){
          var title = queryData.id;
          var list = templateList(filelist);
          var template = templateHTML(title, list,
            `
            <form action="/update_process" method="post">
              <input type="hidden" name="id" value="${title}">
              <p><input type="text" name="title" placeholder="title" value="${title}"></p>
              <p>
                <textarea name="description" placeholder="description">${description}</textarea>
              </p>
              <p>
                <input type="submit">
              </p>
            </form>
            `,
            `<a href="/create">create</a> <a href="/update?id=${title}">update</a>`
          ); 
          response.writeHead(200);
          response.end(template);
        });
      });
```

<form action="/update_process" method="post"> <br>
input type="hidden" name="id" value="${title}" <br> 
<p><input type="text" name="title" placeholder="title" value="${title}"></p> <br>
사용자가 id의 값을 바꿀 수 있게 되면 파일을 찾을 수 없기 때문이다 . 즉 id의 값을 바꾸게 해서는 안된다<br>
id의 값은 수정할 수 없게 hidden으로 처리<br>
id의 값은 유지하면서 title은 바뀐 값이 전송되게 된다<br>


```python
else if (pathname === '/update_process'){
      var body = '';
      request.on('data', function(data){
          body = body + data; // 콜백이 될때마다 데이터를 추가
      });
      request.on('end', function(){
          var post = qs.parse(body);
          var id = post.id;
          var title = post.title;
          var description = post.description;fs.rename(`data/${id}`, `data/${title}`, function(error){ //id(이전의 파일이름)를  title로 바꾼다
          
            fs.writeFile(`data/${title}`, description, 'utf8', function(err){
              response.writeHead(302, {Location: `/?id=${title}`});
              response.end();
            })
          });
      });
    }
```

request.on('data', function(data){ <br>
body = body + data -> 콜백이 될때마다 데이터를 추가<br>
fs.rename(`data/${id}`, `data/${title}`, function(error){ -> id(이전의 파일이름)를  title로 바꾼다


```python
  else if(pathname === '/delete_process'){
      var body = '';
      request.on('data', function(data){
          body = body + data;
      });
      request.on('end', function(){
          var post = qs.parse(body);
          var id = post.id;
          fs.unlink(`data/${id}`, function(error){ 
            response.writeHead(302, {Location: `/`});
            response.end();
```

fs.unlink(`data/${id}`, function(error){ <br>
response.writeHead(302, {Location: `/`}); <br>
response.end(); -> data 디렉토리 아래에 있는 id 값의 파일을 삭제하고<br>
사용자를 홈으로 보낸다 
