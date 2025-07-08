# @kjots/eslint-issue-no-implied-eval-exec-script

## ESLint issue: `no-implied-eval` with non-global `execScript()`

This project demonstrates an issue in ESLint with the [`no-implied-eval`](https://eslint.org/docs/latest/rules/no-implied-eval) rule where it will trigger a false positive for `execScript()` even when the code under test does not make use of the global `execScript()` function.

This issue has been raised on the [ESLint](https://github.com/eslint/eslint) project: https://github.com/eslint/eslint/issues/19923

```javascript
// eslint.config.js

module.exports = [
  {
    rules: {
      'no-implied-eval': 'error'
    }
  }
];
```

```javascript
// index.js

function execScript(string) {
  console.log("This is not your grandparent's execScript().");
}

execScript('wibble');
```

```
$ eslint .

/Users/kjots/Development/Git/github.com/kjots/eslint-issue-no-implied-eval-exec-script/index.js
  5:1  error  Implied eval. Consider passing a function instead of a string  no-implied-eval

✖ 1 problem (1 error, 0 warnings)

```
