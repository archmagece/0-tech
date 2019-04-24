# elixir pheonix

요기서 썼음
https://docs.daybit.com/kr#price-history-interval
https://daybit.com/reward/btc-reward

https://elixirschool.com/ko/
https://elixirschool.com/ko/lessons/basics/basics/

## directory structure
https://pragdave.me/blog/2018/06/02/project-structure.html
```
Elixir
my_app
├── config
├── lib
├── mix.exs
├── README.md
└── test

Ruby
my_app/
├── bin
├── Gemfile
├── lib
├── my_app.gemspec
├── Rakefile
└── README.md

NodeJS
├── dist
├── node_modules
├── src
├── gulpfile.js
├── package.json
└── README

GO
project-layout/
├── api
├── assets
├── build
├── cmd
├── configs
├── deployments
├── docs
├── examples
├── githooks
├── init
├── internal
├── LICENSE.md
├── Makefile
├── pkg
├── README.md
├── scripts
├── test
├── third_party
├── tools
├── vendor
└── web
```

## 특징
안정성 뛰어남
네트워크관련에는 좋음

https://medium.com/@justdevelop/erlang-%EC%82%AC%EC%9A%A9%ED%95%98%EC%97%AC-%EC%84%9C%EB%B2%84-%EA%B0%9C%EB%B0%9C%ED%95%B4-%EB%B3%B4%EB%A9%B0-a84ba20ba4c5
CPU연산량이 많으면 쓰지마
1. 외부에 공개된 서버이면서 바이너리 레벨로 프로토콜을 구성하는 경우 좋아
1. 고성능보다 안정성
1. Hot swapping 기능이 필요한 경우(docker로 하지않나...)
1. 많은 수의 사용자 세션을 다뤄야 하는 경우(stateless라면..)

http://kydonia.net/blog/elixir/2017/02/25/elixir-design-goals-ko/
모든 코어를 다 쓴다(컨테이너보다 한개 하드웨어 통짜로 쓰는게 유리? 핫스왑도 그렇고)
elixir는 macro 있음

## mac에서 테스트

brew install erlang
brew install elixir

고민없이 선택한 프레임워크
https://github.com/phoenixframework/phoenix

## 먼저 pheonix 설치부터
```
mix archive.uninstall phx_new
mix archive.install https://github.com/phoenixframework/archives/raw/master/phx_new.ez
```

## 추가 라이브러리
rebar3: 빌드 버전관리
lager: logging library
cowboy: http server
gproc: pub-sub 기능
jiffy, jsx: json 라이브러리
OTP: 표준라이브러리

## 프로젝트 생성
mix phx.new

하면 이런 메시지가 친절하게 나옴
We are almost there! The following steps are missing:

    $ cd hello
    $ mix deps.get
    $ cd assets && npm install && node node_modules/brunch/bin/brunch build

Then configure your database in config/dev.exs and run:

    $ mix ecto.create

Start your Phoenix app with:

    $ mix phx.server

You can also run your app inside IEx (Interactive Elixir) as:

    $ iex -S mix phx.server


