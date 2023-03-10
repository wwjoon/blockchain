# โ๏ธ Blockchain

## โก Technical Skills

<div>
    <img src="https://img.shields.io/badge/Node.js-339933?style=flat&logo=Node.js&logoColor=white"/>
    <img src="https://img.shields.io/badge/TypeScript-007acc?style=flat&logo=typescript&logoColor=white"/>
</div>

## ๐ Table of Contents

- [๐ tsconfig.json](#tsconfig)
- [๐งพ Declaration Files](#declaration-file)
- [๐ JSDoc](#jsdoc)
- [๐ฌ ts-node](#tsnode)
- [๐ซ DefinitelyTyped](#definitely-typed)
- [๐ Typescript Handbook](#typescript-handbook)
- [๐ญ Reference](#reference)

---

## <a name="tsconfig"></a>๐ tsconfig.json

[tsconfig ๊ณต์๋ฌธ์ ๐](https://www.typescriptlang.org/tsconfig)

```json
{
  "include": ["src"], // typescript ์์ค๊ฐ ์์ฑ๋๋ ๊ฒฝ๋ก
  "compilerOptions": {
    "outDir": "build", // build ๋๋ ๊ฒฐ๊ณผ๋ฌผ์ด ๋ด๊ธธ ํด๋
    "target": "ES6", // build ๋๋ Javascript์ ๋ฒ์ 
    "lib": ["ES6", "DOM"], // Javascript ์ฝ๋๊ฐ ์ด๋ค ํ๊ฒฝ์์ ๋์๋ ์ง ์ ์
    "strict": true,
    "allowJs": true // Javascript์ ์ฌ์ฉ์ ํ์ฉ
  }
}
```

lib ์ Javascript ์ฝ๋๊ฐ ์ด๋ค ํ๊ฒฝ์์ ๋์๋ ์ง๋ฅผ ์ ์ํ๋ค.

๋ง์ฝ `DOM`์ ๋ฃ์ด์ฃผ๊ฒ๋๋ฉด typescript๋ DOM ํ๊ฒฝ์์ ์ ๊ณต๋๋ `document.`, `window.` ๋๋ `localStorage.`๋ฑ์ ์๋ ฅํ์์ ๋ ๋ธ๋ผ์ฐ์  ํ๊ฒฝ์์ ์ง์๋๋ ์๋์์ฑ ๋ชฉ๋ก์ ์ ๊ณตํด์ค๋ค.

---

## <a name="declaration-file"></a>๐งพ Declaration Files

npm์ผ๋ก ์ค์นํ node_modules์ ์กด์ฌํ๋ Javascript ํ์ผ์ ๋ํ type ์ ์ ๋ฐฉ๋ฒ

### myPackage.js

```js
export function init(config) {
  return true;
}
export function exit(code) {
  return code + 1;
}
```

js๋ก ์์ฑ๋ ๊ฐ๋จํ ํ์ผ

### index.ts

```ts
import { init, exit } from "myPackage";

init({ url: "true" });

exit(1);
```

myPackage๋ฅผ importํ๊ฒ๋๋ฉด myPackage์ ๋ํ type์ ์ฐพ์ ์ ์๋ค๋ฉฐ ์๋ฌ๊ฐ ํ์๋๋ค.

### myPackage.d.ts

```ts
interface Config {
  url: string;
}

declare module "myPackage" {
  function init(config: Config): boolean;
  function exit(code: number): number;
}
```

`{ํจํค์ง๋ช}.d.ts` ํ์ผ์ ์์ฑํ ํ js ํ์ผ์ ์๋ ํจ์๋ค์ ํ์์ ์ ์ํด์ค๋ค๋ฉด ์๋ฌ๊ฐ ์ฌ๋ผ์ง๋ฉฐ ์๋์์ฑ ๊ธฐ๋ฅ์ ์ ๊ณตํ๋ค.

---

## <a name="jsdoc"></a>๐ JSDoc

JSDoc์ ๊ธฐ์กด ํ๋ก์ ํธ์ ์กด์ฌํ๋ Javascript ํ์ผ๋ค๊ณผ Typescript๋ฅผ ๊ฒฐํฉํ๊ธฐ ์ํด ์ด์ฉํ๋ค.

### tsconfig.json

```json
{
  "include": ["src"], // typescript ์์ค๊ฐ ์์ฑ๋๋ ๊ฒฝ๋ก
  "compilerOptions": {
    "outDir": "build", // build ๋๋ ๊ฒฐ๊ณผ๋ฌผ์ด ๋ด๊ธธ ํด๋
    "target": "ES6", // build ๋๋ Javascript์ ๋ฒ์ 
    "lib": ["ES6", "DOM"], // Javascript ์ฝ๋๊ฐ ์ด๋ค ํ๊ฒฝ์์ ๋์๋ ์ง ์ ์
    "strict": true,
    "allowJs": true
  }
}
```

๋จผ์  tsconfig.json์ compilerOptions์ allowJs๋ฅผ `true`๋ก ์ค์ ํด์ค๋ค.

### index.ts

```ts
import { init, exit } from "./myPackage";

init({ url: "hi", debug: false });
exit(1);
```

index.ts ์์๋ myPackage ๋ผ๋ ์ด๋ฆ์ js ํ์ผ์ import ํด์ค๋ค.

### myPackage.js

```js
// @ts-check
/**
 * Initializes the project
 * @param {object} config
 * @param {boolean} config.debug
 * @param {string} config.url
 * @returns {boolean}
 */
export function init(config) {
  return true;
}

/**
 * Exits the program
 * @param {number} code
 * @returns {number}
 */
export function exit(code) {
  return code + 1;
}
```

myPackage.js ํ์ผ์๋ ํจ์ ์๋จ์ `// @ts-check`๋ผ๊ณ  ํ์ํด์ฃผ๊ณ  ์ฃผ์์ ์์ฑํ๋ค.

`/**` ์ฌ๊ธฐ๊น์ง๋ง ์์ฑํด๋ vscode์์ ์๋์์ฑ์ผ๋ก ๋๋จธ์ง ์ฝ๋๋ค์ ์์ฑํด์ค๋ค.

param์์ ํจ์์ ๋งค๊ฐ๋ณ์๋ฅผ returns์์ return ํ์์ ์ค์ ํด์ค๋ค.

์ด๋ ๊ฒ ์ค์ ์ ํด์ฃผ๋ฉด index.ts ํ์ผ์๋ init๊ณผ exit ํจ์์ ํ์์ jsํ์ผ์ ๋ณ๊ฒฝ ์์ด ์๋์์ฑ์ด ๋จ๊ฒ๋๋ค.

---

## <a name="tsnode"></a>๐ฌ ts-node

[npm ts-node](https://www.npmjs.com/package/ts-node)

typescript๋ก ์์ฑ๋ ํ์ผ์ ์คํํ๋ ค๋ฉด js๋ก build๋ฅผ ํ ํ `node index.js`์ ๊ฐ์ด ์คํ์์ผ์ผ ํ์คํธ๋ฅผ ํ  ์ ์๋ค.

๊ทธ๋ฌ๋ ts-node ๋ผ์ด๋ธ๋ฌ๋ฆฌ๋ฅผ ์ฌ์ฉํ๋ฉด build๋ฅผ ํ์ง ์๊ณ  ์ง์  TypeScript๋ฅผ ์คํ์์ผ์ฃผ๋ ์ญํ ์ ํ๋ค.

`ts-node index.ts` ์ด๋ฐ์์ผ๋ก ๋ฐ๋ก typescript ํ์ผ์ ์คํํ  ์ ์๋ค.

ts-node๋ typescript ์ฝ๋๋ฅผ buildํ๊ณ  startํ  ํ์ ์์ด ์คํ์์ผ์ค๋ค.

---

## <a name="definitely-typed"></a>๐ซ DefinitelyTyped

[DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped)

Typescript ์ ํ ์ ์๋ฅผ ์ํ ์ ์ฅ์์ด๋ค.

`npm install --save-dev @types/node` ๋ฅผ ์ด์ฉํด typescript ํ์์ ๋ถ๋ฌ ์ฌ ๋ ์ด ์ ์ฅ์์์ ๋ถ๋ฌ์ค๊ฒ ๋๋ค.

type์ด ์ ์๋์ง ์์ ํจํค์ง์ type ์ ์๋ฅผ ๊ธฐ์ฌํ๊ณ  ์ถ๋ค๋ฉด ์ด ์ ์ฅ์์ Pull Request๋ฅผ ํ์ฌ ๊ธฐ์ฌํ  ์ ์๋ค.

---

## <a name="typescript-handbook"></a>๐ Typescript Handbook

Typescript์ ๋ํด ๋ ๋ฐฐ์ฐ๊ณ  ์ถ๋ค๋ฉด [Typescript Handbook๐](https://www.typescriptlang.org/docs/handbook/intro.html)

---

## <a name="reference"></a>๐ญ Reference

https://nomadcoders.co/typescript-for-beginners

https://github.com/Lecture-Summary/typechain
