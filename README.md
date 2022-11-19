# django_project


### 1. 장고 설치, 환경설정 하기 
~~~~~
- 새 프로젝트 생성 뒤, 가상환경 interpreter 설정 
  (Virtualenv Environment)

- 인터프리터 설정에서 django 설치 (pip install django)
  3.2.1 버전 

- 장고 프로젝트 생성 터미널에 
  django-admin startproject (프로젝트이름) 입력
  그 뒤, django 프로젝트 폴더 생성 
  
- 터미널에 python manage.py runserver 입력 후
  django 실행 확인 
~~~~~~~~~~ 

---------------------------------

### 2. blog 앱과 single_page 앱 만들기 

~~~~~
- 터미널에 python manage.py startapp blog 
         (       똑같이             )single_pages 입력 

  1. 모델 만들기-블로그 글 저장 위한 Post 모델 
  
  2. 데이터베이스에 Post 모델 반영
     - 터미널에 python manage.py makemigrations 입력 
       (앞으로 모델 수정시 필수 입력...) 
     'No changes detected' 가 뜨면 OK
     
  3. setting.py에 blog 앱과 single_page 앱 등록하기 
     INSTALLED_APPS 에 추가! 
     
  4. 터미널에 python manage.py makemigrations (모델반영) 


 - 관리자 모드에서 글 작성하기 
    * 관리자 계정 생성 python manage.py createsuperuser

  1. blog/admin.py에 Post 모델 추가 
     관리자 페이지에 Post 모델 등록 
  
  2. 포스트 제목 ,번호 출력, 작성 시간 고치기 

** 모델 수정 후에는 makemigration -> migrate !

~~~~~~

### 3. 장고로 웹페이지 만들기 

~~~~~~~
- URL 설정하기
  1. django_project(프로젝트 이름)/urls.py 에서 
     어떤 페이지로 연결 할지 정함 
     블로그 url 만듦

  2. blog/urls.py 생성 

- FBV(Function based view) 페이지 만들기 
 
  1. blog/urls.py 에 내용 추가하기 
          urlpatterns = [
            path('', views.index),
        ]
     -blog에서 views의 인덱스를 보여주는? 

  2. blog/views.py에서 index() 함수 정의 

  3. 템플릿 파일 만들기 
     blog/templates/blog 폴더 생성 아래 index.html 생성 

  4. 블로그 페이지에 포스트 목록 나열하기 
     model.py의 Post 모델 임포트, index() 함수
     blog/views.py에 입력 

  5. index.html 에 포스트 목록 나열 
      -최신 포스트 보여주기 

  6. 상세 페이지 만들기 
      - 포스트 상세 패이지 URL 정의 하기 (blog/url.py)
      - blog/views.py에서 함수 설정 
      - 상세 페이지 템플릿 만들기 
      - blog/model.py 에서 상세페이지 링크로 가는 모델 설정 
     
- single_pages 앱 만들기 
  
  1. single_pasge 앱 url 정의 (프로젝트 파일/urls.py) (대문페이지?)
  
  2. 대문 페이지, 자기소개 페이지 URL 정의하기  
     -도메인 뒤에 뭐가 있는지에 따라 views.py 파일에 어떤 함수를 실행 시킬지?
     
  3. single_pages/views.py에 함수 정의 하기 
  
  4. 템플릿 파일 만들기  
  
~~~~~~~~~~~~~~~~~~~~~~~~  

### 4.정적파일 처리하기 

~~~~~~~~~~~~~
- FBV -> CBV 변환 

  1. blog/views.py 수정
     함수에서 클래스 모델로 변경
     
  2. blog/urls.py 수정 
     기존에 views.py에서 정의 했던 함수를 
     클래스 모델로 변경 
  
  3. 모델에 맞게 템플릿 지정
     -직접 지정 : blog/views.py PostList 클래스 모델에서 
       template_name을 직접 지정 
      
     - 관례 : 파일명을 post_list.html로 수정 
    
  4. 상세페이지도 위가 같은 방법..
     - post_list.html 에서 기존에 posts 라고 쓰여 있는 부분을 
       post_list로 수정! (Post 모델을 사용해서 바꿔준거임!) 

- 정적파일 처리하기 
  
  1. 각 앱 폴더 안에 static 폴더 만들고 css파일 넣기
       각 앱 폴더(blog, single_pages) 

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

### 장고 쉘 플러스 사용하기 

~~~~~~~~~~~~~~~~~~~~~~~~~~

  파이썬 콘솔? 터미널? 환경에서 장고 홈페이지 정보? 확인가능 
  
  터미널에 입력 
  - pip install django_extensions ipython
  - python manege.py shell_plus 입력 

  Post.objects.count() = 개수 출력 
  Post.objects.all() = 목록 모두 출력 

  for 문 사용하여 포스트 글 목록 확인 가능 

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
 
### 템플릿 모듈화
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
  모듈화할 템플릿 파일을 복사하여, base.html로 수정
   
  base.html에서 공통영역만 남기고 삭제 
  ( ex 포스트 올라가는 부분만 삭제) 
  삭제한 부분에 {% block main_area %}
               {% endblock %} 작성 
  
  원본 템플릿 파일에서 앞에서 삭제한 부분만 남기고 다 삭제 
  맨 앞에 {% extends 'blog/base.html' %}와 
       {% block main_area %} 작성 
  맨 뒤에 {% endblock %} 작성
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

### TTD 사용 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
  생성한 앱 폴더에 test.py에 테스트 코드 작성후 
  터미널에 python manage.py test 실행 
  
  post_list.html 모듈화 후 
  python manege.py test blog.tests.TestView.test_post_list 실행으로 결과확인

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~