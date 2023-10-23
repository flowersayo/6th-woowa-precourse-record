본 규칙은 [AngularJS commit conventions](https://docs.google.com/document/d/1QrDFcIiPjSLDn3EL15IJygNPiHORgU1_OOAqWjiDU5Y/edit#heading=h.uyo6cb12dt6w)
을 참고하여 작성되었습니다.


# 깃 커밋 메시지 컨벤션이란?

깃(Git) 커밋 메시지 컨벤션은 일관된 형식을 사용하여 커밋 메시지를 작성하도록 하는 규칙이나 가이드라인을 의미합니다. 
이러한 컨벤션은 개발자들이 프로젝트의 변경 사항(History)을 이해하고 추적하기 쉽도록 도와줍니다.



# 커밋 메시지 형식 (Format of the commit message)

```
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

- 커밋 메시지는 100자를 넘을 수 없습니다.
- 하나의 커밋 메시지는 헤더, 바디, 푸터로 구성되어 있습니다.

**예시**

```
fix($compile): couple of unit tests for IE9

Older IEs serialize html uppercased, but IE9 does not...
Would be better to expect case insensitive, unfortunately jasmine does
not allow to user regexps for throw expectations.

Closes #392
```

# 메시지 헤더(Message header)

> `<type>(<scope>): <subject>`

한줄의 간결한 설명으로 해당 커밋을 요약합니다.


## `<type>`  

해당 커밋이 제공하는 **변경사항의 종류**를 나타냅니다.

- feat: 새로운 기능 추가
- fix: 버그 수정
- docs: 문서 변경
- style: 코드 의미에 영향을 주지 않는 변경 (화이트스페이스, 포맷팅, 세미콜론 누락 등)
- refactor: 버그를 수정하거나 기능을 추가하지 않는 코드 변경
- perf: 성능 향상을 위한 코드 변경
- test: 누락된 테스트 추가
- chore: 빌드 프로세스나 보조 도구 및 라이브러리에 대한 변경 (문서 생성 등)

## `<scope>` (optional)
 
해당 커밋에서 **변경이 일어난 부분**이나 모듈, 파일 등을 가리키는 것으로 사용됩니다. 
`<scope>` 를 명시적으로 지정함으로서 다른 팀원들이 커밋의 영향을 빠르게 이해할 수 있게 됩니다.
적합한 스코프가 없다면 * 을 사용할 수 있습니다. 

## `<subject>`

변경사항에 대한 **아주 짧은(very short)** 설명입니다. **명령형이고 현재형**으로 작성합니다. 
대문자로 시작하지 않고 끝에 `.` 을 붙이지 않습니다.


# 메시지 바디(Message body)

이 변경사항 대한 동기, 이전 동작과 대조하는 것을 포함해야합니다.  **명령형이고 현재형**으로 작성합니다. 



# 메시지 푸터(Message footer)

`Breaking changes` 나 해당 커밋으로 `해결된 이슈목록`을 참조하는데 사용됩니다. 

## Breaking changes

소프트웨어의 새 버전이 이전 버전과 호환되지 않는 변경 사항을 의미합니다.

ex) API 변경, 기존 기능의 제거, 데이터 형식 변경 또는 구조 변경 등 

## Referencing issues

`Closes` 키워드로 시작하여 다음과 같이 해당 해당 커밋이 해결한 이슈를 닫습니다.

```
Closes #123, #245, #992
```


# 예시

```
feat($compile): simplify isolate scope bindings

Changed the isolate scope binding options to:
  - @attr - attribute binding (including interpolation)
  - =model - by-directional model binding
  - &expr - expression execution binding

This change simplifies the terminology as well as
number of choices available to the developer. It
also supports local name aliasing from the parent.

BREAKING CHANGE: isolate scope bindings definition has changed and
the inject option for the directive controller injection was removed.

To migrate the code follow the example below:

Before:

scope: {
  myAttr: 'attribute',
  myBind: 'bind',
  myExpression: 'expression',
  myEval: 'evaluate',
  myAccessor: 'accessor'
}

After:

scope: {
  myAttr: '@',
  myBind: '@',
  myExpression: '&',
  // myEval - usually not useful, but in cases where the expression is assignable, you can use '='
  myAccessor: '=' // in directive's template change myAccessor() to myAccessor
}

The removed `inject` wasn't generaly useful for directives so there should be no code using it.
```




```
style($location): add couple of missing semi colons
```
