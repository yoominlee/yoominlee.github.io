---
layout: post
title: Github blog
subtitle: Generate github blog and customize
categories: gitblog
tags: [gitblog]
---

This note demonstrates some of what [Markdown][1] is capable of doing.

## 0. 시작하게 된 이유

메모장 처럼 네이버 블로그에 필기를 올렸던 적이 있었는데 나중에 보니 기록도 되고 보기도 편했다.

그래서 velog, tistory 등 다양한 기록 및 포폴용 블로그들을 찾아보게 되었고

시작 허들이 높지 않은 velog를 시도해 봤었었다.

하지만 자유도가 높지 않아 다른 블로그를 찾아보게 되었고,

깃허브 블로그가 내 웹사이트 형식으로 만들어질 수 있다는 부분이 좋았다. 

또한 추후에 포트폴리오를 만들 때 사용할 수 있을 것 같다는 생각도 들었다. 

무엇보다 재미있을 것 같았다.(학기 초 아니면 못할 것 같았다)

---

## 1. 레포지토리 만들기
![1][1]

#### ✅ Repository name
[ 사용자이름.github.io ]로 레포지토리 이름 설정한다.
나는 사용자명이 yoominlee여서 yoominlee.github.io 라고 설정했다.


#### ✅ 추가 설정
public으로 설정, README 파일 추가하는것 체크만 하면 완료!

​
## 2. Ruby 설치
![img2][2]

#### ✅설치파일 다운로드
[하단 링크](https://rubyinstaller.org/downloads/)로 들어가 64비트가 아닌 32비트 devkit으로 다운 받는다.

https://rubyinstaller.org/downloads/

​🤔* jekyll이 32비트기 때문에 64비트 파일로 설치하면 터미널에서 알아듣지 못한다고 한다.*

#### ✅설치파일 실행

다운받은 설치파일 실행한다.

처음에 Agree누르는 부분을 제외하고 다른것 안건드리고 다 Next 눌렀다.

⚠️마지막에 종료 누르기 전 터미널 여는것 체크 해주고 finish 누르기!

![img3][3]


#### ✅cmd 창

위의 이미지는 마지막에 체크 해준 후 Finish 누르면 자동적으로 뜨는 창이다.

1,2,3 다 설치하는건데 그냥 Enter 누르면 된다.

​
![img4][4]

#### ✅설치 확인

cmd 창을 연 후에 ruby -v 를 치면 다운받은 버전이 나온다.

## 3. jekyll

![img5][5]

#### ✅jekyll 설치

cmd 창에서 하단 내용을 입력(좌상단 이미지)

설치가 완료 되면 jekyll -v 를 입력해서 버전을 확인해준다.

버전이 확인되면 설치 잘 된것.


`$ gem install jekyll bundeler`


![img6][6]

#### ✅파일 정리

클론한 폴더에 파일 있다면 모두 지우고

cmd에서 클론한 폴더로 이동


#### ✅jekyll로 사이트 생성

`$ jekyll new ./`

이전 단계까지 완료 후 이동한 cmd에서 위의 명령어 입력


![img7][7]

bundle 설치하기 위해 마찬가지로 아래 내용 cmd에 입력

`$ bundle install`


![img8][8]

jkeyll을 로컬 서버에 띄우기 위해 다음을 입력

`$ bundle exec jekyll serve --trace`

🤔 *cannot load such file --brick 오류 뜨면*
`$ bundle add webrick` *명령어 입력 후 다시 $ bundle exec jekyll serve --trace 입력해서 서버를 띄우면 된다.*

잘 되었다면 아래 이미지 처럼 cmd 창 하단에 Server address가 보인다.


![img9][9]

그리고 그 IP로 된 url을 브라우저에 복붙 하면 아래와 같은 이미지가 뜨고, jekyll 설치가 성공한  것


![img10][10]


## 4. jekyll 테마 적용


![img11][11]

#### ✅jekyll 테마 선택

아래 [링크](https://jekyll-themes.com/)에서 원하는 테마를 고른다 (이외에도 사이트 다양하다)

https://jekyll-themes.com/

이후 Download 클릭.

#### ✅zip 압축풀기

로컬 git repository 위치에 다운받은 zip 파일의 압축을 해제한다.

나의 경우 하단 [docs](https://youssefraafatnasry.github.io/portfolYOU/docs/)에서 하라는 단계를 따랐다.​

https://youssefraafatnasry.github.io/portfolYOU/docs/

#### ✅내가 clone 한 디렉토리에 적용

아까 jekyll 확인 했던 것 처럼 로컬에서 사이트 확인

https://docs.github.com/ko/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll


![img12][12]

좌측 url을 입력 해 주면 우측과 같은 창이 뜬다!

## 5. 커스텀

[이전에 작업하던 템플릿의 docs](https://youssefraafatnasry.github.io/portfolYOU/docs/)를 참고하여 커스텀 한 것으로 다른 테마 사용 시 동일하게 적용되지 않을 수 있다

#### ✅favicon 적용

아래 [링크](https://favicon.io/)에서 내가 원하는 favicon 선택 후 favicon.ico 파일을 assets/favicon.ico 경로에 위치해 준다

https://favicon.io/

#### ✅업데이트

⚠️현재 계속해서 업데이트 중 ⚠️

수정 한 내용 저장 후 클론받은 디렉토리 위치의 cmd 창에서

$ bundle exec jekyll serve 

입력해서 나온 url 브라우저에 입력(반복하는 경우 새로고침만 해주기)하면서 업데이트 확인





[1]: https://github.com/yoominlee/img/blob/main/2023-03-14-01_github-blog/2023-03-14-01.png?raw=true
[2]: https://github.com/yoominlee/img/blob/main/2023-03-14-01_github-blog/2023-03-14-02.png?raw=true
[3]: https://github.com/yoominlee/img/blob/main/2023-03-14-01_github-blog/2023-03-14-03.png?raw=true
[4]: https://github.com/yoominlee/img/blob/main/2023-03-14-01_github-blog/2023-03-14-04.png?raw=true
[5]: https://github.com/yoominlee/img/blob/main/2023-03-14-01_github-blog/2023-03-14-05.png?raw=true
[6]: https://github.com/yoominlee/img/blob/main/2023-03-14-01_github-blog/2023-03-14-06.png?raw=true
[7]: https://github.com/yoominlee/img/blob/main/2023-03-14-01_github-blog/2023-03-14-07.png?raw=true
[8]: https://github.com/yoominlee/img/blob/main/2023-03-14-01_github-blog/2023-03-14-08.png?raw=true
[9]: https://github.com/yoominlee/img/blob/main/2023-03-14-01_github-blog/2023-03-14-09.png?raw=true
[10]: https://github.com/yoominlee/img/blob/main/2023-03-14-01_github-blog/2023-03-14-10.png?raw=true
[11]: https://github.com/yoominlee/img/blob/main/2023-03-14-01_github-blog/2023-03-14-11.png?raw=true
[12]: https://github.com/yoominlee/img/blob/main/2023-03-14-01_github-blog/2023-03-14-12.png?raw=true