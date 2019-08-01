Node.TypeScript
===============


## 프레임워크

* nest.js: 스프링과 비슷한 구조 제공
* express: 일반적으로 선호
* koa: express에서 세대교체중


## Starter
* https://github.com/microsoft/TypeScript-Node-Starter
* https://github.com/bitjson/typescript-starter


## 유닛테스트

### mocha + chai

### karma + jasmine


## 개발환경

#### nodemon: 재시작

```json
{
  "watch": ["src"],
  "ext": "json,ts",
  "ignore": ["src/**/*.spec.ts"],
  "exec": "ts-node -r tsconfig-paths/register src/main.ts"
}
```

```json
{
  "watch": ["src"],
  "ext": "ts",
  "ignore": ["src/**/*.spec.ts"],
  "exec": "node --inspect-brk -r ts-node/register -r tsconfig-paths/register src/main.ts"
}
```

#### prettierrc

코드포매팅

#### lint: 코드포매팅

```json
{
  "extends": [
    "tslint-config-standard",
    "tslint-config-prettier"
  ],
  "rules": {
    "class-name": true,
    "comment-format": [
      true,
      "check-space"
    ],
    "one-line": [
      true,
      "check-open-brace",
      "check-whitespace"
    ],
    "no-var-keyword": true,
    "semicolon": [
      true,
      "never"
    ],
    "quotemark": [true, "single"],
    "whitespace": [
      true,
      "check-branch",
      "check-decl",
      "check-operator",
      "check-module",
      "check-separator",
      "check-type"
    ],
    "typedef-whitespace": [
      true,
      {
        "call-signature": "nospace",
        "index-signature": "nospace",
        "parameter": "nospace",
        "property-declaration": "nospace",
        "variable-declaration": "nospace"
      },
      {
        "call-signature": "onespace",
        "index-signature": "onespace",
        "parameter": "onespace",
        "property-declaration": "onespace",
        "variable-declaration": "onespace"
      }
    ],
    "member-access": [
      false
    ],
    "no-internal-module": true,
    "no-trailing-whitespace": true,
    "no-null-keyword": true,
    "prefer-const": true,
    "jsdoc-format": true,
    "arrow-parens": false,
    "object-literal-sort-keys": false,
    "no-console": false
  }
}
```
