## 1. Nextjs Project 新規作成
### 1-1. yarn install *インストールしていない場合
    npm install --global yarn
    yarn --version
### 1-2.  create-next-app
    npx create-next-app .
#### Node.js version 10.13以降が必要です。 -> ターミナル `node -v`でver確認出来ます。

### 1-4.  React-Testing-Library + MSW + next-page-tester のインストール
    yarn add -D jest @testing-library/react @testing-library/jest-dom @testing-library/dom babel-jest @babel/core @testing-library/user-event jest-css-modules
### 1-5.  Project folder 直下に".babelrc"ファイルを作成して下記設定を追加
    touch .babelrc
~~~
    {
        "presets": ["next/babel"]
    }
~~~
### 1-6.  package.json に jest の設定を追記
~~~
    "jest": {
        "testPathIgnorePatterns": [
            "<rootDir>/.next/",
            "<rootDir>/node_modules/"
        ],
        "moduleNameMapper": {
            "\\.(css)$": "<rootDir>/node_modules/jest-css-modules"
        }
    }
~~~
### 1-7.  package.jsonに test scriptを追記
~~~
    "scripts": {
        ...
        "test": "jest --env=jsdom --verbose"
    },
~~~
### 1-8.  prettierの設定 : settingsでRequire Config + Format On Saveにチェック
    touch .prettierrc
~~~
    {
        "singleQuote": true,
        "semi": false
    }
~~~  
## 2. Test動作確認
### 2-1. `__tests__`フォルダと`Home.test.tsx`ファイルの作成
~~~
import { render, screen } from '@testing-library/react'
import '@testing-library/jest-dom/extend-expect'
import Home from '../pages/index'

it('Should render title text', () => {
  render(<Home />)
  expect(screen.getByText('Next.js!')).toBeInTheDocument()
})
~~~
### 2-2. yarn test -> テストがPASSするか確認
~~~
 PASS  __tests__/Home.test.tsx
  ✓ Should render hello text (20 ms)

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        1.728 s, estimated 2 s
~~~
