## 1. Nextjs Project 新規作成
### 1-1. yarn install *インストールしていない場合
    npm install --global yarn
    yarn --version
### 1-2.  create-next-app
    npx create-next-app@12.3.2 .
#### Node.js version 10.13以降が必要です。 -> ターミナル `node -v`でver確認出来ます。
### 1-2-1.  next.jsのversionを変更
    yarn add next@12.3.2
### 1-3.  React-Testing-Libraryのインストール
    yarn add -D jest jest-environment-jsdom @testing-library/react @testing-library/jest-dom jest-css-modules
### 1-4.  Project folder 直下に"jest.config.js"ファイルを作成して下記設定を追加
    touch jest.config.js
~~~
const nextJest = require('next/jest')
const createJestConfig = nextJest({
  dir: './',
})
const customJestConfig = {
  moduleDirectories: ['node_modules', '<rootDir>/'],
  testEnvironment: 'jest-environment-jsdom',
}
module.exports = createJestConfig(customJestConfig)
~~~
### ~~1-5.  package.json に jest の設定を追記~~
### 1-6.  package.jsonに test scriptを追記
~~~
    "scripts": {
        ...
        "test": "jest --watch"
    },
~~~
### 1-7.  prettierの設定 : settingsでRequire Config + Format On Saveにチェック
    touch .prettierrc
~~~
    {
        "singleQuote": true,
        "semi": false
    }
~~~  
## 2. Test動作確認
### 2-1. `__tests__`フォルダと`Home.test.jsx`ファイルの作成
~~~
import { render, screen } from '@testing-library/react'
import '@testing-library/jest-dom'
import Home from '../pages/index'

it('Should render title text', () => {
  render(<Home />)
  expect(screen.getByText('Next.js!')).toBeInTheDocument()
})
~~~
### 2-2. yarn test -> テストがPASSするか確認
~~~
 PASS  __tests__/Home.test.js
  ✓ Should render hello text (20 ms)

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        1.728 s, estimated 2 s
~~~
