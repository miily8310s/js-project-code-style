# JavaScript Style Guide MEMO

## 参照ページ:
- [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)
- [ESLint rules](https://eslint.org/docs/rules/)

## よく出てくるもの
  ### 変数の参照
  - すべての参照は`const`を使用し、`var`は使用しない
  
    ESLint: [prefer-const](https://eslint.org/docs/rules/  prefer-const.html), [no-const-assign](https://eslint.org/docs/  rules/no-const-assign.html)
  
    ```js
    // ダメな例
    var a = 1;
    var b = 2;
    
    // 良い例
    const a = 1;
    const b = 2;
    ```
  
  - 参照を再割当てする場合は`var`の代わりに`let`を使用する
  
    ESLint: [no-var](https://eslint.org/docs/rules/no-var.html)
  
    ```js
    // ダメな例
    var count = 1;
    if (true) {
      count += 1;
    }
    
    // 良い例
    let count = 1;
    if (true) {
      count += 1;
    }
    ```
  
  ### オブジェクト
  - オブジェクトを作成する際は、リテラル構文を使用する
  
    ESLint: [no-new-object](https://eslint.org/docs/rules/no-new-object.html)
  
    ```js
    // ダメな例
    const item = new Object();
    
    // 良い例
    const item = {};
    ```
  - メソッド/プロパティの短縮構文（Shorthand）を使用する

    ESLint: [object-shorthand](https://eslint.org/docs/rules/object-shorthand.html)

    ```js
    const lukeSkywalker = 'Luke Skywalker';
    // ダメな例
    const atom = {
      value: 1,
    
      addValue: function (value) {
        return atom.value + value;
      },
    };

    const obj = {
      lukeSkywalker: lukeSkywalker,
    };

    
    // 良い例
    const atom = {
      value: 1,
    
      addValue(value) {
        return atom.value + value;
      },
    };

    const obj = {
      lukeSkywalker,
    };
    ```
  ### 配列
  - 配列を作成する際は、リテラル構文を使用する
  
    ESLint: [no-array-constructor](https://eslint.org/docs/rules/no-array-constructor.html)

    ```js
    // ダメな例
    const items = new Array();
    
    // 良い例
    const items = [];
    ```
  - 直接配列に項目を代入せず、Array.pushを使用する

    ```js
    const someStack = [];
    // ダメな例
    someStack[someStack.length] = 'abracadabra';
    
    // 良い例
    someStack.push('abracadabra');
    ```
  - 配列をコピーする場合は、配列の拡張演算子`...`を使用する

    ```js
    // ダメな例
    const len = items.length;
    const itemsCopy = [];
    let i;
    
    for (i = 0; i < len; i++) {
      itemsCopy[i] = items[i];
    }

    
    // 良い例
    const itemsCopy = [...items];
    ```
  - 配列が複数行ある場合、配列の開始の括弧の後と、最後の括弧の前に改行を入れる

    ```js
    // ダメな例
    const arr = [
      [0, 1], [2, 3], [4, 5],
    ];
    
    const objectInArray = [{
      id: 1,
    }, {
      id: 2,
    }];
    
    const numberInArray = [
      1, 2,
    ];

    
    // 良い例
    const arr = [[0, 1], [2, 3], [4, 5]];

    const objectInArray = [
      {
        id: 1,
      },
      {
        id: 2,
      },
    ];
    
    const numberInArray = [
      1,
      2,
    ];
    ```
  ### 構造化
  - 複数のプロパティからなるオブジェクトにアクセスする際は、オブジェクト構造化代入を使用する
  
    ESLint: [prefer-destructuring](https://eslint.org/docs/rules/prefer-destructuring)

    ```js
    // ダメな例
    function getFullName(user) {
      const firstName = user.firstName;
      const lastName = user.lastName;
    
      return `${firstName} ${lastName}`;
    }
    
    // 良い例
    function getFullName(obj) {
      const { firstName, lastName } = obj;
      return `${firstName} ${lastName}`;
    }
    
    // 最高な例
    function getFullName({ firstName, lastName }) {
      return `${firstName} ${lastName}`;
    }
    ```
  - 配列の構造化代入を使用する
  
    ESLint: [prefer-destructuring](https://eslint.org/docs/rules/prefer-destructuring)

    ```js
    const arr = [1, 2, 3, 4];

    // ダメな例
    const first = arr[0];
    const second = arr[1];
    
    // 良い例
    const [first, second] = arr;
    ```

  ### 文字列
  - プログラムで文字列を生成する場合は、文字列連結ではなく、テンプレート文字列を使用する
  
    ESLint: [prefer-destructuring](https://eslint.org/docs/rules/prefer-template.html) [prefer-destructuring](https://eslint.org/docs/rules/template-curly-spacing)

    ```js
    // ダメな例
    function sayHi(name) {
      return 'How are you, ' + name + '?';
    }
    
    function sayHi(name) {
      return ['How are you, ', name, '?'].join();
    }
    
    function sayHi(name) {
      return `How are you, ${ name }?`;
    }
    
    // 良い例
    function sayHi(name) {
      return `How are you, ${name}?`;
    }
    ```
  ### 関数
  - 関数宣言ではなく名前付き関数式を使用する
  
    ESLint: [func-style](https://eslint.org/docs/rules/func-style) 

    ```js
    // ダメな例
    function foo() {
      // ...
    };
    
    const foo = function () {
      // ...
    };
    
    // 良い例
    const short = function longUniqueMoreDescriptiveLexical () {
      // ...
    };
    ```

  - 関数構文の中にスペースを入れる
  
    ESLint: [func-style](https://eslint.org/docs/rules/func-style) 

    ```js
    // ダメな例
    const f = function(){};
    const g = function (){};
    const h = function() {};
    
    // 良い例
    const x = function () {};
    const y = function a() {};
    ```

  ### アロー関数
  - 無名関数を使用する必要がある場合は、アロー関数表記を使用する
  
    ESLint: [prefer-arrow-callback](https://eslint.org/docs/rules/prefer-arrow-callback.html),[arrow-spacing](https://eslint.org/docs/rules/arrow-spacing.html)

    ```js
    // ダメな例
    [1, 2, 3].map(function (x) {
      const y = x + 1;
      return x * y;
    });
    
    // 良い例
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });
    ```

  ### モジュール
  - 非標準モジュールシステム上では常にモジュール（`import`/`export`）を使用する

    ```js
    // ダメな例
    const StyleGuide = require('./StyleGuide');
    module.exports = StyleGuide.es6;
    
    // 良い例
    import StyleGuide from './StyleGuide';
    export default StyleGuide.es6;

    // 最高な例
    import { es6 } from './StyleGuide';
    export default es6;
    ```

  - すべてのimportをimport文以外の上に置く

    ESLint: [import/first](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/first.md)

    ```js
    // ダメな例
    import foo from 'foo';
    import { named1, named2 } from 'foo';
    
    // 良い例
    import foo, { named1, named2 } from 'foo';
    
    import foo, {
      named1,
      named2,
    } from 'foo';
    ```

  - パスからは一箇所のみでインポートする

    ```js
    // ダメな例
    import foo from 'foo';
    foo.init();
    
    import bar from 'bar';
    
    // 良い例
    import foo from 'foo';
    import bar from 'bar';
    
    foo.init();
    ```


  - 複数行のインポートは、複数行の配列リテラルおよびオブジェクトリテラルと同じようにインデントする

    ```js
    // ダメな例
    import {longNameA, longNameB, longNameC, longNameD, longNameE} from 'path';
    
    // 良い例
    import {
      longNameA,
      longNameB,
      longNameC,
      longNameD,
      longNameE,
    } from 'path';
    ```