```json
//tsconfig.json
"compilerOptions": {
	// js 파일의 사용 허용 옵션, 프로젝트가 js에서 ts로 마이그레이션 중일 때 사용한다.
	// allowJS: true,

	// 모듈을 import, 또는 require할 시, 절대 경로를 사용을 위한 rootDir 설정 옵션
	// ex)
	// baseUrl
	// ├── ex.ts
	// ├── hello
	// │   └── world.ts
	// └── tsconfig.json
	//
	// in ex.ts
	// import { helloWorld } from "hello/world";
	//
	"baseUrl": "./",

	// d.ts 파일 생성 관련 옵션
	// d.ts 파일은 변수 및 커스텀 생성한 Type 등에 대한 명세를 보여준다.
	"declaration": true,

	// 모듈 호출시, ES호환성 관련 옵션
	// TS에서, 아래의 두 줄의 ES6 코드는 모듈시스템 내부 동작에 의해 모듈이 호출 방식이 같지 않다.
	// import moment from 'moment';      (=== const moment = require("moment"))
	// import * as moment from 'moment'; (=== const moment = require("moment").default)
	//
	// 공식적인 호출 방식은 두번째 방법이며,
	// 따라서 첫번째 방식으로 호출 할 경우 에러가 발생한다.
	//
	// esModuleInterop 옵션 활성화 시, importHelpers 옵션이 활성화되며,
	// 첫번째 방식으로도 모듈을 호출 할 수 있게 된다.
	"esModuleInterop": true,

	// ts 데코레이터 관련 옵션, relect-metadata 모듈을 기반으로 하는 메타데이터의 사용 설정 옵션이다.
	// 데코레이터 사용시, true
	"emitDecoratorMetadata": true,

	// ts 데코레이터 관련 옵션, 데코레이터 실험적 사용 설정 옵션이다.
	// 실험적 사용이라는 표현이 사용되는 이유는 데코레이터는 아직 JS 공식 승인 언어 기능이 아니기 때문이다.
	// 데코레이터 사용시, true
	"experimentalDecorators": true,

	// JS파일 안의 Jsx 구성을 어떻게 할지 제어하는 설정
	// .tsx로 시작한 JS파일의 결과에만 영향이 있다.
	// 올 수 있는 값과 예시는 아래와 같다.
	//
	// // sample code
	// export const helloWorld = () => <h1>Hello world</h1>
	//
	// "react" (default)
	// import React from 'react';
	// export const helloWorld = () => React.createElement("h1", null, "Hello world");
	//
	// "preserve"
	// import React from 'react';
	// export const helloWorld = () => <h1>Hello world</h1>;
	//
	// "react-native"
	// import React from 'react';
	// export const helloWorld = () => <h1>Hello world</h1>;
	//
	// "react-jsx"
	// import { jsx as _jsx } from "react/jsx-runtime";
	// import React from 'react';
	// export const helloWorld = () => _jsx("h1", { children: "Hello world" }, void 0);
	//
	// "react-jsxdev"
	// import { jsxDEV as _jsxDEV } from "react/jsx-dev-runtime";
	//	const _jsxFileName = "/home/runner/work/TypeScript-Website/TypeScript-Website/index.tsx";
	// import React from 'react';
	// export const helloWorld = () => _jsxDEV(
	// 		"h1", { children: "Hello world" }, void 0, false, {
	//			fileName: _jsxFileName, lineNumber: 9, 	columnNumber: 32
	//      },
	//      this);
	"jsx": "preserve"

	// ts에는 내장 js API (Math 등)에 대한 기본 유형 정의 및 브라우저 환경의 유형 정의 등이 포함되어 있다.
	// 이러한 유형 정의 set을 어떤 버전으로 이용할 것인지에 대한 설정 옵션
	//
	// Option 종류
	// ES5 / ES2015(ES6) / ES2016(ES7) / ES2017 / ES2018
	// ES2019 / ES2020 / ES2021 / ESNext / DOM / WebWorker / ScriptHost
	// 각 버전 별로 추가되는 유형 정의가 있다 (자세한 내용은 하단에 이미지 참고)
	//
	// ts로 최신 문법 작성시 에러가 발생한다면, 해당 문법의 유형 정의를 가지고 있는 버전을 lib 옵션에 추가해야한다.
	// (ES6를 추가할 시, ES2020과 ES2019를 같이 넣어주는 것이 좋다)
	"lib": ["DOM", "ES5", "ES2015"],

	// 빌드된 결과물이 어떤 런타임 환경에서 실행 가능한지에 대한 설정
	// default는 es3 이지만, 권장은 ES6이다.
	// 해당 값을 변경하면, lib 값도 같이 변경된다.
	"target": "ES6",

	// 빌드될 프로젝트의 루트 디렉토리를 지정
	// 해당 디렉토리를 기준으로 빌드가 이뤄짐
	"rootDir": "./src",

	// 빌드된 결과물이 저장될 디렉토리를 지정
	"outDir": "./dist",

	// type definition파일(*.d.ts)을 어디에서 불러올지 설정하는 옵션
	// defalut 경로: node_modules/@types/PACKAGE_NAME/index.d.ts
	//
	// typeRoots와 types 옵션은 같이 사용하지 않는다.
	//
	// typeRoots는 배열 안의 경로에서만 type definition 파일을 불러온다.
	// tpyeRoots 배열은 인자로 경로 값을 가진다.
	//
	// types는 배열 안의 경로 또는 default 경로에서 PACKAGE_NAME을 찾아 파일을 불러온다.
	// types 배열은 인자로 패키지 이름 값을 가진다.
	"typeRoots": ["PATH"],
	"types": ["PACKAGE_NAME"],


	// Type을 엄격하게 검사할 것인지 설정하는 옵션 (true 권장)
	// strict: true라면, strict에 종속되는 옵션들은 전부 true 값을 가진다.
	"strict": true,

	// 현 프로그램을 위한 모듈 로더(loader)을 설정하는 옵션
	// 모듈 로더?
	// 모듈을 불러와서 실행시키는 프로그램
	// Options
	// CommonJS / UMD / AMD / System / ESNext / ES2020 / ES6
	"module": "MODULE_NAME",
}
```
