# JavaScript Style Guide MEMO

## 参照ページ:
- [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)
- [ESLint rules](https://eslint.org/docs/rules/)
- [Google JavaScript Style Guide](https://google.github.io/styleguide/jsguide.html)
- [Google TypeScript Style Guide](https://google.github.io/styleguide/tsguide.html)

## よく出てくるもの
  ### 変数の参照
  - すべての参照は`const`を使用し、`var`は絶対に使用しない
  
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
    
      addValue: (value) => {
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

  - 直接配列に項目を代入せず、`Array.push`を使用する

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
    const getFullName = (user) => {
      const firstName = user.firstName;
      const lastName = user.lastName;
    
      return `${firstName} ${lastName}`;
    }
    
    // 良い例
    const getFullName = (obj) => {
      const { firstName, lastName } = obj;
      return `${firstName} ${lastName}`;
    }
    
    // 最高な例
    const getFullName = ({ firstName, lastName }) => {
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
    const sayHi = (name) => {
      return 'How are you, ' + name + '?';
    }
    
    const sayHi = (name) => {
      return ['How are you, ', name, '?'].join();
    }
    
    const sayHi = (name) => {
      return `How are you, ${ name }?`;
    }
    
    // 良い例
    const sayHi = (name) => {
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
    
    // 良い例
    const foo = () => {
      // ...
    };
    
    const short = function longUniqueMoreDescriptiveLexical () {
      // ...
    };
    ```

  - 関数構文の中にスペースを入れる
  
    ESLint: [func-style](https://eslint.org/docs/rules/func-style) 

    ```js
    // ダメな例
    const f = () => {};
    const g =  ()=>{};
    const h = () => {};
    
    // 良い例
    const x = () {};
    const y = function a() {};
    ```

  ### アロー関数
  - 無名関数を使用する必要がある場合は必ずアロー関数表記を使用する
  
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
  - 非標準モジュールシステム上では常にモジュール（`import`/`export`）を使用する。requireは使用しない。

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

  ### イテレータ
  - イテレータを使わない。`for-in`や`for-of`のようなループは使用しない。
    - 配列を反復処理するには `map()`/`every()`/ `filter()`/ `find()`/`findIndex()`/`reduce()`/`some()`などを使用する
    - `Object.keys()`/`Object.values()`/`Object.entries()`で配列を作成してオブジェクトを反復処理できるようにする

    ```js
    const numbers = [1, 2, 3, 4, 5];

    // ダメな例
    let sum = 0;
    for (let num of numbers) {
      sum += num;
    }
    sum === 15;
    
    const increasedByOne = [];
    for (let i = 0; i < numbers.length; i++) {
      increasedByOne.push(numbers[i] + 1);
    }
    
    // 良い例
    let sum = 0;
    numbers.forEach((num) => {
      sum += num;
    });
    sum === 15;
    
    const increasedByOne = [];
    numbers.forEach((num) => {
      increasedByOne.push(num + 1);
    });

    // 最高な例
    const sum = numbers.reduce((total, num) => total + num, 0);
    sum === 15;
    const increasedByOne = numbers.map(num => num + 1);
    ```

  ### プロパティ
  - プロパティにアクセスする場合はドット(`.`)を使用する

    ESLint: [dot-notation](https://eslint.org/docs/rules/dot-notation.html)

    ```js
    const numbers = [1, 2, 3, 4, 5];

    // ダメな例
    let sum = 0;
    for (let num of numbers) {
      sum += num;
    }
    sum === 15;
    
    const increasedByOne = [];
    for (let i = 0; i < numbers.length; i++) {
      increasedByOne.push(numbers[i] + 1);
    }
    
    // 良い例
    let sum = 0;
    numbers.forEach((num) => {
      sum += num;
    });
    sum === 15;
    
    const increasedByOne = [];
    numbers.forEach((num) => {
      increasedByOne.push(num + 1);
    });
    ```

  ### 変数
  - 変数を宣言する際は、常に`const`か`let`を使用する。使用しない場合はグローバル変数として宣言される。

    ESLint: [no-undef](https://eslint.org/docs/rules/no-undef), [prefer-const](https://eslint.org/docs/rules/prefer-const)

    ```js
    // ダメな例
    superPower = new SuperPower();
    
    // 良い例
    const superPower = new SuperPower();
    ```

  - インクリメント演算子(`++`)デクリメント演算子(`--`)を使わない
    - `num++`の代わりに`num += 1`のような構文で値を変更する方が良い

    ESLint: [no-plusplus](https://eslint.org/docs/rules/no-plusplus)

    ```js
    // ダメな例
    const array = [1, 2, 3];
    let num = 1;
    num++;
    --num;
    
    let sum = 0;
    let truthyCount = 0;
    for (let i = 0; i < array.length; i++) {
      let value = array[i];
      sum += value;
      if (value) {
        truthyCount++;
      }
    }
    
    // 良い例
    const array = [1, 2, 3];
    let num = 1;
    num += 1;
    num -= 1;
    
    const sum = array.reduce((a, b) => a + b, 0);
    const truthyCount = array.filter(Boolean).length;
    ```

  - 未使用の変数を許可しない

    ESLint: [no-unused-vars](https://eslint.org/docs/rules/no-unused-vars)

    ```js
    // ダメな例
    var some_unused_var = 42;

    // y=5の変数yは使用されているとは見なされない
    var y = 10;
    y = 5;
    
    // z = z + 1の変数zは使用済みとは見なされない
    var z = 0;
    z = z + 1;
    
    // xは未使用の関数の引数
    function getX(x, y) {
        return x;
    }
    
    // 良い例
    function getXPlusY(x, y) {
      return x + y;
    }
    
    var x = 1;
    var y = a + 2;
    
    alert(getXPlusY(x, y));
    ```

  ### 比較演算子と等価性

  - `==`や`!=`より`===`と`!==`を使用する

    ESLint: [eqeqeq](https://eslint.org/docs/rules/eqeqeq.html)

  - if文のような条件式はToBooleanメソッドによる強制型変換で評価され、以下のルールに常に従う

    ```
    - オブジェクトは`true`と評価
    - undefinedは`false`と評価
    - nullは`false`と評価
    - 真偽値は`boolean`型の値として評価
    - 数値は`true`と評価されます。しかし`0とNaN`の場合はfalse
    - 文字列は`true`と評価されます。しかし空文字`''`の場合はfalse
    ```

    ```js
    if ([0]) {
      // true
      // 配列はオブジェクトなのでtrueとして評価
    }
    ```

  - 不要な3項ステートメントを避ける

    ESLint: [no-unneeded-ternary](https://eslint.org/docs/rules/no-unneeded-ternary.html)

    ```js
    // ダメな例
    const foo = a ? a : b;
    const bar = c ? true : false;
    const baz = c ? false : true;
    
    // 良い例
    const foo = a || b;
    const bar = !!c;
    const baz = !c;
    ```

  ### ブロック
  - ifブロックが常にreturn文を実行するのであれば、それに続くelseブロックは不要

    ESLint: [no-else-return](https://eslint.org/docs/rules/no-else-return)

    ```js
    // ダメな例
    function foo() {
      if (x) {
        return x;
      } else {
        return y;
      }
    }

    // 良い例
    function foo() {
      if (x) {
        return x;
      }
    
      return y;
    }
    ```
  - ブロックのインデントは2スペースにすること

    ```js
    // ダメな例
    const hoge = () => {
        console.log('hoge');
    }

    // 良い例
    const hoge = () => {
      console.log('hoge');
    }
    ```

  ### タイプキャスティング＆コアーション
  - 文の先頭で型の強制を行う、newをつけての型変換はしない

    ESLint: [no-new-wrappers](https://eslint.org/docs/rules/no-new-wrappers),
    [radix](https://eslint.org/docs/rules/radix)

    ```js
    const age = 0;

    // ダメな例
    const totalScore = this.reviewScore.toString();
    const val = parseInt(inputValue);
    const hasAge = new Boolean(age);

    // 良い例
    // 文字列の場合はStringを使用する
    // 数字の場合はNumberを使用する、
    // parseIntを使用する場合は常に型変換のための基数を引数に渡す
    // 真偽値の場合はBooleanまたは!!を使用する
    const totalScore = String(this.reviewScore);
    const val = Number(inputValue);
    const val = parseInt(inputValue, 10);
    const hasAge = Boolean(age);
    const hasAge = !!age;
    ```

  ### 命名規則
  - メソッド名は`lowerCamelCase`で記述する

    ```js
    // ダメな例
    const ismethod = () => {
      // ...
    };

    // 良い例
    const isMethod = () => {
      // ...
    };
    ```

  - const変数であり、プログラマがそれを変更しないと信頼できる場合に限り、定数を大文字（`CONSTANT_CASE`）にする

    ESLint: [camelcase](https://eslint.org/docs/rules/camelcase.html)

    ```js
    const age = 0;

    // ダメな例
    export const apiKey = 'SOMEKEY';

    // 良い例
    export const API_KEY = 'SOMEKEY';
    ```
  - 変数名は、新しい読者にとって説明的で明確でなければいけない。プロジェクト外の読者にはあいまいまたはなじみのない略語は使用しない

