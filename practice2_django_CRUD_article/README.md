## Django_Articles_flow_Practice

#### 처음 장고 시작전에 준비 단계

1. 폴더 생성
2. vscode 켜기
3. git init (지금 여기 practice에선 이미 되어있으므로 할 필요 없음)
4. python -m venv venv (가상환경 생성)
5. source venv/Scripts/activate(깃배쉬에서만 적용) (혹은 5번 걍 안해도 깃배쉬창 지웠다가 다시키면 가상환경 적용되긴 함)
6. ctrl + shift + p를 통해 Interpreter 들어가서 가상환경 전체 적용
7. .gitignore생성해주기 venv에 양이 너무 많아서 이건 깃 애드커밋 할 필요 없도록 해주기 위함. 그외에도 상황따라 다를 수 있음. 현재는 gitignore.io 들어가서 입력해주는데 윈도우, 파이썬, 장고, 비쥬얼스튜디오 복붙해줬음 (저장하면 venv에 초록불 꺼짐 vsc에서도 왼쪽바에 나타나는 커밋부분 1k에서 1개로 바뀜)
8. requirement.txt 가져오기 pip list 해서 확인해보면 가상환경이어서 뭐 설치된게 없음
9. pip install -r requirements.txt 를 통해 requirement 전부 설치해주기 ( `pip install django==3.2.12` 현재는 requirements.txt에 이게 있으므로 따로 안해줬지만 장고를 시작하려면 우선 가상환경 생성하고 활성화 후 장고를 설치 해줘야 한다.)

> 어떤 무언갈 추가로 따로 설치했으면 `pip freeze > requirements.txt`해줘서 requirements.txt에 추가해줘야 함 
>
> 위에 코드는 pip list를 requirements.txt로 만들어주는 거임. 
>
> 다른 협업하는 사람과 같은 가상환경을 만들기 위해 이용함.

----

#### 장고 프로젝트 생성부터 시작!

1. `django-admin startproject crud .` 여기서 crud 프로젝트 뒤에 점찍는 이유는 현재 위치에 생성하도록 하기 위해서임. 점 없으면 안에 폴더 또 만들어지고 그안에 생성됨.

2. `python manage.py startapp articles` 앱 생성 (앱은 일반적으로 복수형으로 작성함)

3. 세팅에서 앱 등록 해주기 & LANGUAGE_CODE ='en-us' 를 한글로 바꿀려면 'ko-kr' 로 바꾸고 TIME_ZONE ='UTC'를 한국시간으로 바꿀려면 'Asia/Seoul' 로 바꿔주기 (지금 practice에서는 앱등록하고 시간만 바꿔줬음)

4. models.py 작성

5. `python manage.py makemigrations` 마이그레이션 해주기 (설계도느낌으로 새롭게 설계도 만들때 사용)

6. `python manage.py migrate` 까지 해주면 됨 (설계도를 실제 DB에 반영되는 거) 

7. 이후에도 models.py 변경 되면 다시 마이그레이션 해주면 됨 그러면 기존 행 어떻게 할 건지 1,2 선택지 나오는데 1번해서 디폴트 값 주는 거 하면 엔터만하면 타임존 나우 디폴트값 적용할 수 있다고 알려줌

8. 그리고 마지막으로 다시 마이그레이트 하면 됨

   > `git log` 를 통해 잘 커밋해 오고 있는지 볼 수 있으며 나가고 싶으면 q 누르면 됨
   >
   > 서버확인을 위해서는 `python manage.py runserver` 로 확인해주며 ctrl + c로 끌 수 있음

9. 어드민 계정 만들기 `python manage.py createsuperuser` 하고 이름, 이메일, 비번 작성해주기 (간단해도 ㄱㅊ해? 질문에 y누르면 됨)

10. 서버에서 어드민 추가해서 봐도 아직 안됨. admin.py 가서 추가해줘야 함

11. 가장 상위에서 templates를 만들어 base.html 을 넣어준다. 그리고 `! + tab` 을 해줘서 기본 형태를 잡고 부트스트랩 넣어주고 타이틀 작성해주고 `block content`해준다

12. settings.py 가서 TEMPLATES 가서 DIR 부분 안에 BASE_DIR / 'templates' 넣어서 이곳을 확인할 수 있도록 해주기

----

#### 본격적으로 url , view, template 순으로 작업시작

1. articles 안에 urls.py 만들기

2. crud 의 urls.py 가서 articles/ 들어오면 articles 안에 있는 urls.py에 맡기도록 작성해주기 주석처리로 include 하는 방법 나와있음 그대로 따라하면 됨

3. articles의 urls.py로 가서 작성할 때 path안의 name 적어주는 이유는 html 에서 a태그해서 이동할 때를 위함이며 앱 네임 써주는 이뉴는 앱이 여러개 일 때 다른 앱에서도 같은 name이 있는 경우를 해결하기 위해서 이다.

4. views.py 에서 index 함수 만들어 주고 articles안에다가 templates만들고 그 안에 articles만들고 그안에 index.html 만들기 (전체 게시글 조회)  view에서 'articles' key로 넘겨주고 index.html에서 for를 사용해서 보여줄 article을 p태그로 사용해서 만들기

5. 이후 서버 열면 글목록엔 아무것도 없음 그 이유는 글 작성을 안해서임. admin가서 글 작성하면 p태그 작성한 거 뜸

   ----

6. 다시 url 가서 new 페이지 만들준비

7. view 가서 new함수 만들고

8. new.html 만들고

9. new.html 에서 form 작성하고

10. index.html 에서 글 작성 a태그 만들어주기

    ----

11. 다시 url 가서 create 페이지 만들준비

12. view 가서 create함수 만들고

13. create.html 만들고

14. new의 form에서 action 부분 수정하기 (url 추가해주기. create로 가는)

15. crerate에서 글목록으로 가는 url 만들어 주기

16. 글 내용들 최신순을 위로 올리기 위해 views.py 에서 index 함수에서 articles 뒤에 `.all()[::-1]` 또는 `.order_by('-pk')`를 이용해주기 (여기서 all은 전부 가져오는거고 get은 하나 가져오는거고 일부분만 갖고 오고싶으면 filter를 이용해서 order_by 하면 됨. filter없이 그냥 order_by는 전부 적용 됨) (이런 정보들은 전부 공식문서에 있으니 꼭 공식문서와 친해지기!)

17. new.html에서 method POST로 바꿔주고 csrf 토큰 추가해줌

18. view에서도create함수에서 불러오는거 GET을 POST로 바꿔주기

19. 그리고 create함수에서 render를 하고 index템플릿으로 가게되면 글을 작성 후에도 게시글 조회가 되지 않음 URL은 여전히 create에 머물러 있게됨. 즉 단순히 인덱스 페이지만 render되었을 뿐 그렇기에 redirect를 해줘야 함. create함수에서 render를 redirect로 바꾸고 index.html로 가도록 해주기

20. 그러면 이제 create에서 생성후 바로 articles:index로 이동하므로 create.html에서 성공적으로 글이 작성되었다는 템플릿은 필요가 없음. 템플릿에서 create.html 삭제해주면 됨

----

#### DETAIL, DELETE, EDIT

1. 개별 게시글 상세 페이지를 위해 url에서 `'<int:pk>/'`로 경로를 지정해줌 view에서 detail 함수에서 get(pk=pk) 를 통해 우측 pk는 variable routing을 통해 받은 pk이며 왼쪽 pk는 DB에 저장된 레코드의 pk(id)임

2. detail.html 작성해 페이지 만들어 주고 index.html에 detail 링크작성

3. create 메소드에서 변경해서 글 작성이후 글목록으로 안가고 detail로 이동하도록 작성하기. redirect에서 인덱스를 디테일로 바꾸고 pk가져가도록 하기

   > 여기까지가 CRUD에서 CR임!!!!
   >
   > 이제 밑으로 UD 계속해서 진행하기!

4. Delete진행하기. 먼저 url 만들고 view에서 메소드 만들고 detail.html에서 글삭제 할 수 있도록 해주는 버튼 만들기. 여기서 a태그쓰면 GET방식으로 주소창에서 지울수 있게 되므로 form으로 작성해야하고 POST방식으로 하고 csrf토큰도 사용해야함!

5. view에서 delete에서 if문을 사용해서 post만 삭제 요청되도록 하기

6. 마찬가지로 url에 edit만들어 주고 view에 edit함수 만들어주고 템플릿에 edit.html만들어주기. new에 있는 form 복사해서 가져옴. value 추가해줌

7. detail 페이지에 EDIT페이지로 갈 수 있는 링크 작성

8. 마찬가지로 url에 update만들어주고 view에 작성해주고 create와 마찬가지로 별도의 수정되었다는 메시지를 출력하는 template은 필요없으며 edit.html에서 form action에 링크를 추가하면 됨.
