strict - next.js의 기본 eslint 구성과 더욱 엄격한 cor

import 및 모듈의 절대 경로 별칭 설정

next.js에는 tsconfig.json 파일의 "paths" 및 b

자동 셍성되는 항목
package.json 파일에 scripts 자동 추가 / public 디렉토리
TypeScript 사용(선택) : tsconfig.json 파일 생성
Eslint 설정 (선택) : eslintrc.json 대신 eslint.config.mjs 파일 생성
Tailwind CSS 사용 (선택)
src 디렉토리 사용 (선택)
App Router(선택), app/layout.tsx 파일 및 app/page.tsx
Turbopack 사용 (선택)
import alias 사용 (선택) : tsconfig.json에 "paths" 자동 생성.
수동으로 프로젝트를 생성할 때 추가적으로 해야 하는 작업을 자동으로 처리해 줍니다.

Core web Vitals

LCP (Largest Contentful Paint) : 뷰포트 내에서 가장 큰 페이지 요소 (큰 텍스트 블록, 이미지 또는 비디오)를 표시하는데 걸리는 시간. \*뷰포트 : 웹페이지 사용자가 별도의 스크롤 동작 없이 볼 수 있는 영역

FID(First Input Delay) : 사용자가 웹페에지와 상호작용을 시도하는 첫 번째 순간부터 웹페이지가 응답하는 시간.

CLS(Cumulative Layout Shift) : 방문자에게 콘텐츠가 얼마나 불안정한 지 측정한 값입니다. 페이지에서 갑자기 발생하는 레이아웃의 변경이 얼마나 일어나는지 측정합니다.
즉, 레이아웃 이동 ( layout shift) 빈도를 측정합닞다.

#실습에 사용할 프로젝트를 생성합니다.

공식 문서에는 기본 패키지 관리자를 pnpm을 사용합니다.
원하는 패키지 관리자 탭을 클릭하면 명령을 확인할 수 있습니다. (npx create-next-app@latest)
pnpm과 관련한 내용을 뒤에서 설명합니다.
다음 명령으로 프로젝트를 생성합니다.

명령을 실행하면 당므과 같은 8개의 선택 항목이 나옵니다.

1. 포로젝트 이름을 입력합니다.
   2~4 TypeScript, ESLint, Tailwind를 사용할지 선택합니다.
   5.src/디렉토리를
   구분/ /src 디렉토리 사용 (추천) /src 디렉토리 미사용
   구조/ 모든 코드가 src/폴더 안에 들어감 // 코드가 프로젝트 루트에 바로 위치함
   예/ src/app, src/components, src/lib 등 // app, components, lib등
   목적/ 코드와 설정 파일을 분리 / 전체가 섞여 있음

#.eslintrc.json vs eslint.config.mjs

json은 주석, 변수, 조건문 등을 쓸 수 없기 때문에 복잡한 설정이 어렵습니다.
(JavaScript Object Notation)
mjs 는 ESLint가 새롭게 도입한 방식으로, ESM(ECMAScript 모듈) 형식입니다.
확장자 .mjs는 "module JavaScript" 를 의미합니다.
ESLint v9 이상에서 공식 권장 방식입니다.
조건문, 변수 동적 로딩 등 코드처럼 유연한 설정이 가능합니다.
다른 설정 파일을 import 해서 재사용을 할 수 있습니다.
프로젝트 규모가 커질수록 유지보수에 유리합니다.
포멧 / JSON 형식 // JavaScript 모듈
실행방식/ 정적인 설정파일 // 동적인 설정도 가능 (함수, 변수, 사용 등)
호환성/ 구버전 ESLint와 호환 // ESLint v9 부터 공식 권장
특징/ 간단하고 직관적 // 더 유연하고 모듈화 가능
사용 여부 / 여전히 사용 가능 // 최신 Next.js에서 가능

Next.js와 eslint.config.mjs

Next.js14 이후로는 ESLint 9 와의 호환성을 고려해 최신 권장 방식인 eslint.config.mjs를 사용하는 쪽으로 전환되고 있습니다.

.eslintrc.json도 여전히 지원되므로, 필요한 경우 수동으로 만들거나 마이그레이션해서 사용할 수 있습니다.

마이그레이션 도구는 아직 공식적으로 제공되지는 않지만, 직접 욺기려면 다음처럼 하면 됩니다.

json

// .eslintrc.json{
"extends" : " next",
"rules": {
"no-console": "warn"
}
}

js

// eslint.config.mjs
import next from 'eslint-config-next';
export default [
next(),{
rules:{
'no console':'warn',
}
}
]

pnpm은 Performant(효율적인) NPM의 약자로 고성능 Node 패키지 매니저입니다,.

npm, yarn과 같은 목적의 패키지 관리자이지만, 디스크 공간 낭비, 복잡한 의존성 관리, 느린 설치 속도 문제 개선을 위해 개발되었습니다.
대표적인 특징은 다음과 같습니다.

1.  하드 링크(Hard Link) 기반의 효율적인 저장 공간 사용
    : 패키지를 한 번만 설치하여 글로벌 저장소에 저장하고, 각 프로젝트의 node_modules 디렉토리에는 설치된 패키지에 대한 하드 링크 (또는 심볼릭 링크) 가 생성됩니다.

2.  빠른 패키지 설치 속도 (Performant) :이미 설치된 패키지는 다시 다운로드 하지 않고 재사용하므로, 초기 설치뿐만 아니라 종속성 설치 및 업데이트 할 때도 더 바른 설치가 가능합니다.

$ pnpm intall
$ pnpm add
$ pnpm remove
$ pnpm update

$ pnpm create next-app@latest

-npm의 npx 대신 pnpm create을 사용합니다.,
next-app 명령이 실제로 실행되는 것은 create-next-app 입니다.
블로그 드 ㅇ에서 pnpm도 create-next-app 이라고 소개하는 경우가 있지만 추천하지는 않습니다.
$ cd my-app
서버 실행 : $ pnpm start

Hard link vs symbolic link(soft link)

#pnpm의 특징 중에 하드 링크를 사용해서 디스크 공간을 효율적으로 사용할 수 이 ㅆ다고 합니다. 탐색기에서 npm과 pnpm프로젝트의 node.module의 용량을 확인해 보세요. #왜 효율적이라 한 것일까요 ?

원본과 하드링크는 같은 것 입니다.

soft 공유하지 않고 경로 문자열을 저장해두는 특수 파일입니다.(바로가기초롬) 따라서 심볼릭 링크를 열면 내부에 적힌 "경로"를 따라가서 원본 파일을 찾습니다.
원본이 삭제되면 심볼릭 링크는 끊어진 경로가 되므로 더 이상 사용할 수 없습니다.
