---
title: Jekyll Chripy 테마로 Github Blog 만들기
description: Jekyll 테마를 이용하여 Github Blog 만들기
author: jiwon
date: 2024-11-06 11:33:00 +0900
categories: [Blogging]
tags: [typography]
pin: false
math: true
mermaid: true
# image:
#   path: /commons/devices-mockup.png
#   lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
#   alt: Responsive rendering of Chirpy theme on multiple devices.
---


### 서론
---
대학생 때 사용하던 티스토리 대신 조금 더 개발자스러운 블로그를 만들고 싶었습니다. 벨로그와 깃허브 블로그 중 고민하다가 조금더 저만의 스타일을 보여줄 수 있는 깃허브 블로그로 결정했습니다!<br/> Markdown으로 포스팅하는 법도 익힐겸, 만들면서 겪었던 문제와 어떻게 해결했는지를 다루는 포스팅해보려고 합니다. 깃허브 블로그 만드는데 3시간 정도 걸렸고, 크게 어려운 부분은 없기 때문에 본인이 개발자라면 한 번쯤 만들어보는 것도 추천합니다!


### 개발 과정
---


#### 1. Git 레포지토리 생성
---
본인의 깃허브 계정에 레포지토리를 생성합니다. 여기서 레포지토리 명은 "username.github.io"로 작성합니다. 본인의 username 대신 다른 걸로 지정해도 되지만, 조금더 설정할 것이 늘어난다고 하니 이왕이면 본인 username으로 지정하면 좋겠습니다.


레포지토리 Settings > Pages에 들어가서 설정을 해줘야합니다.

Build and deployment에서 Source > Deploy from a branch으로 수정해줍니다!
![Desktop View](/assets/img/posts/241106/github_pages.png){: width="972" height="589" }


#### 2. Git 프로젝트 Clone
---
이제 로컬 환경에서 글을 쓸 수 있어야하기 때문에 project를 clone 해줍니다.
```bash
$ git clone https://github.com/devjiwon/devjiwon.github.io.git
```
참고로 저는 이번에 노트북을 새로 장만했기 때문에, 처음부터 설정해야 할 것들이 있었습니다.


#### 3. Brew, ruby 설치
---
jekyll로 깃허브 블로그를 만들기 위해선 ruby 설치가 필수입니다. ruby와의 7년전 추억을 뒤로하고, 설치를 해봅니다..

ruby를 설치하기 전에 brew를 설치해야 합니다.
[Homebrew 홈페이지](https://brew.sh/)에 들어가서 brew를 설치하기 위한 명령어를 복사해줍니다.
![Desktop View](/assets/img/posts/241106/homebrew.png){: width="972" height="589" }

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

설치가 완료되면, 아래 명령어를 입력해주세요.
```bash
% (echo; echo 'eval "$(/opt/homebrew/bin/brew shellenv)"') >> /Users/jim      /.zprofile
% eval "$(/opt/homebrew/bin/brew shellenv)"
```

brew를 통해 ruby를 설치해봅시니다.

```bash
brew update
brew install rbenv ruby-build

# 설치 확인
rbenv versions

# 아래의 형태로 나오면 system ruby 사용중
* system (set by /Users/...

# 해당 명령어를 통해 설치가능한 ruby 버전 확인
rbenv install -l

# 버전을 입력하여 루비 설치
rbenv install {version}
```

루비를 설치했다면, 루비의 경로를 설정해줍니다. 저는 이 부분을 놓쳐서 배포할 때 에러를 만났습니다.
```bash
vi ~/.zshrc

[[ -d ~/.rbenv  ]] && \
  export PATH=${HOME}/.rbenv/bin:${PATH} && \
  eval "$(rbenv init -)"

# 저장 후 적용
source ~/.zshrc
```


#### 4. Jekelly 템플릿 다운
---
맘에 드는 지킬 테마를 찾아주세요! 다양한 지킬 테마는 여기서 확인할 수 있습니다. 

<http://jekyllthemes.org/>


저는 그 중 [Chirpy 테마](https://github.com/cotes2020/jekyll-theme-chirpy)가 제일 맘에 들었습니다.

마음에 드는 깃허브에 들어가서 **소스코드를 다운로드** 해주세요.
![Desktop View](/assets/img/posts/241106/chirpy_download.png){: width="972" height="589" }


압출을 풀어서 프로젝트 전체를 본인의 레포지토리에 복사붙여넣기를 해주세요.

그럼 이제 한 번 실행시켜볼까요?

아래 명령어를 통해 jekyll 서버를 실행시키면, <http://127.0.0.1:4000/> 에서 확인이 가능합니다!
```bash
jekyll serve
```

#### 5. 배포
---
깃에 푸시하기 전에 로컬에서 정상적으로 확인이 되는지 먼저 확인해보면, 예상치 못한 오류를 줄일 수 있으니 로컬에서 한 번 실행시켜보세요!

자, 이제 배포할 준비가 끝났다면, push 해주세요.
배포 상황은 Actions 탭에서 확인이 가능합니다. 만약 정상적으로 초록색 표시가 뜨지 않고, 빨간색으로 오류가 발생했다면 detail을 들어가서 오류 메세지를 확인하세요.
![Desktop View](/assets/img/posts/241106/git_actions.png){: width="972" height="589" }

제가 직면한 첫번째 문제는 위에서 설치한 ruby의 경로를 global로 설정하지 않아 발생한 문제였습니다. global로 수정해주니 바로 해결!
![Desktop View](/assets/img/posts/241106/git_deployment_error.png){: width="972" height="589" }


문제가 없다면 5~10분 정도 시간이 지난 후, 본인의 블로그가 잘 배포된 걸 확인할 수 있습니다.
<https://devjiwon.github.io/>


### 마무리
---
혹시라도 깃 블로그를 만들면서 어려운 부분이 있다면, 댓글 남겨주시면 도움드리겠습니다.