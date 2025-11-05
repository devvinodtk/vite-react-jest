# React + TypeScript + Vite + Jest + RTLnp

Install dependencies for Jest + RTL

```
npm install --save-dev jest @types/jest ts-jest @testing-library/react @testing-library/jest-dom @testing-library/user-event \
jest-environment-jsdom ts-node
```

Root tsconfig.json modify as below

```
 "references": [
  ...,
  { "path": "./tsconfig.test.json" }
 ]

```

Create Root tsconfig.test.json

```
{
  "extends": "./tsconfig.app.json",
  "compilerOptions": {
    "noEmit": false,
    "allowImportingTsExtensions": false,
    "types": ["jest", "node"],
    "verbatimModuleSyntax": false,
    "esModuleInterop": true,
  },
  "include": ["src/**/*.test.ts", "src/**/*.test.tsx", "src/setupTests.ts", "src/global.d.ts"]
}
```

Update jest.config.ts

```
transform: {
  '^.+\\.(ts|tsx)$': ['ts-jest', { tsconfig: 'tsconfig.test.json' }],
},
```

package.json add 'test' under scripts

```
"test": "jest"
```

Create src/setupTests.ts

```
import '@testing-library/jest-dom';
```

Add a global CSS module type declaration as src/global.d.ts

```
declare module '*.css';
declare module '*.scss';
declare module '*.sass';
declare module '*.less';
```

Include the global types file in tsconfig.test.json

```
"include": [
  ...,
  "src/global.d.ts"
]
```
 
Ensure identity-obj-proxy is installed

```
npm install --save-dev identity-obj-proxy
```

Mock static assets (so image imports also work)

Create file src/__mocks__/fileMock.ts

```
export default 'test-file-stub';
```