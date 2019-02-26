# Flask

> Flask는 파이썬으로 활용할 수 있는 microframework이다.

## 1. 설치 및 Hello, world!

``` bash
$ pip install flask
```

``` python
#app.py
from flask import Flask

app = Flask(__name__)

@app.rout('/')
def index():
    return 'Hello, world'
```

* 서버 실행

  1. flask run

     ``` bash
     $ flask run
     ```

     * 기본 설정이 app.py 파일을 실행하는 것이다.

     * 만약, 파일 이름이 hello.py 라면, 아래와 같이 실행한다.

       ``` bash
       $ FLASK_APP=hello.py flask run
       ```

  2. python app.py

     * 스크립트 파일을 실행시키는 것과 동일한데, 이때는 app.py 파일에 아래와 같이 작성되어야 한다.

       ```python
       if __name__ == '__main__':
           app.run(debug=True)
           #c9에서는 아래와 같이 설정한다.
           app.run(host='0.0.0.0', port='8080', debug=True)
       ```

## 2. Variable routing

> Variable routing은 url의 특정 값을 변수로써 활용하는 것이다.

``` python
@app.route('/hi/<name>')
def hi():
    return f'{name}, 안녕!'

@app.route('/cube/<int:n>')
def cube(n):
    return str(n**3)
```

## 3. Template

>html 파일을 return 하며, jinja2를 활용하여 변수/반복문/조건문 등을 활용할 수 있다.

1. app.py 에서 `render_template` import

   ``` python
   from flask import Flask, render_template
   ```

2. app.py 에서 return

   ```python
   @app.route('/')
   def index():
       return render_template('index.html')
   ```

3. templates 폴더 내에 해당 html 파일 생성

   ```	html
   <! -- templates/index.html -->
   <h1>안녕</h1>
   ```

* 폴더구조

  ``` 
  .
  ├── app.py
  └── templates
      ├── base.html
      ├── dinner.html
      └── hello.html
  ```

  

## 4. Template  활용 - jinja2  문법

1. python에서 값 받아오기

   1. app.py

      ``` python
      name = '전홍준'
      return render_template('index.html', name=name)
      ```

   2. templates/index.html

      ```jinja2
      <h1>{{name}},안녕</h1>
      ```

2. 반목문 활용하기

   1. app.py

      ```python
      dinner = ['술','고기','소주']
      return render_template('index.html' , dinner=dinner)
      ```

   2. templates/index.html

      ``` jinja2
      <ol>
      {% for menu in dinner %}
      	{% if menu =='술' %}
      		<li>맥주</li>
      	{% else %}
      		<li>{{menu}}</hi>
      	{% endif %}
      {% endfor %}
      </ol>
      ```

   3. 주석 조심!!

      ```jinja2
      {# 이 주석! #}
      <!-- 은 주석이 아니다! -->
      ```

## 5. Template 상속

* `templates/base.html`

  ```jinja2
  <body>
  	{% block body %}
  	{% endblock %}
  </body>
  ```

* `templates/index.html`

  ```jinja2
  {% extends 'base.html' %}
  {% block body %}
  	<h1>안녕</h1>
  {% endblock %}
  ```

  