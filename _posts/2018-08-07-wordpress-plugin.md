---
layout: post
title:  "워드프레스 영화정보 플러그인 만들기"
date:   2018-08-07 15:25:16 +0900
categories: wordpress, plugin, OSS
---
# 워드프레스 영화정보 플러그인 만들기

ScriptonBasestar의 첫 공개 프로젝트~

옛날부터 그냥 쓰던 블로그가 있는데 영화정보 등록하는 간단한 플러그인을 만들어 쓰고 있었는데...

생각 난 김에 만들기도 하고 만드는 방법 정리도 하려고 한다.

https://github.com/ScriptonBasestar/sb-wp-review_infobox

## 디렉토리 구조

표준으로 정해진 것은 없는 것 같지만 개인적으로 이 구조가 맘에 들었다.

```text
.
├── classes
├── css
├── images
├── inc
├── javascript
├── test
│   ├── mysql
│   │   ├── conf
│   │   └── init
│   └── wp
│       └── init
├── view
└── sb-review-infobox.php
```

디렉토리 루트에 프로젝트명과 같은 php파일이 들어가는게 관례(인 것 같다)

## 실행 순서

1. activation(플러그인 활성화)\
  `register_activation_hook(__FILE__, 'sb_review_infobox_activate');`
2. run(실행시 코드들)
3. deactivation(플러그인 비활성화)\
  `register_deactivation_hook(__FILE__, 'sb_review_infobox_deactivate');`

구조는 PHP답게 자유롭고 간단하다.
클래스 내에 선언한 것은 이렇게 호출을 하던데.. PHP를 잘 몰라서 패스\
`register_activation_hook(__FILE__, array($this, 'plugin_activation'));`

전역변수를 남발해도 되지만 나중에 오류가능성이 있으니 주의는 해야한다.

어차피 PHP 레거시 프로젝트는 전역이 남발되어 있는게 보통이니 편하게 돌아만 가면 되지 않을까

## 테스트

완전 자동화된 테스트를 원했지만... 하나하나 셋팅하기 귀찮아서 설치까지만 자동화를 하고 테스트는 수동으로 처리한다.

```txt
docker-compose
wp-cli
```

참고 사이트\
  https://www.lesstif.com/pages/viewpage.action?pageId=22643947
  https://make.wordpress.org/cli/handbook/quick-start/
  https://developer.wordpress.org/cli/commands/core/

## 기능

tinymce에 버튼을 클릭하면 영화정보를 검색하고 화면에 출력된다.

tinymce 추가기능 참고: https://github.com/ScriptonBasestar-Study/tinymce-advanced

