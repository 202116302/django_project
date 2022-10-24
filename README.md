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