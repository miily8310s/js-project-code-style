# JavaScript Style Guide MEMO

## 参照ページ:
- [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)
- [ESLint rules](https://eslint.org/docs/rules/)

## 変数の参照
- すべての参照は`const`を使用し、`var`は使用しない

  ESLint: [prefer-const](https://eslint.org/docs/rules/prefer-const.html), [no-const-assign](https://eslint.org/docs/rules/no-const-assign.html)

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
