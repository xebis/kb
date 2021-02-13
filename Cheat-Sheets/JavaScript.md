# JavaScript

**This** cheat sheet **is NOT complete!**

## Modules

### ES Modules

```javascript
export myConst; // named export: const, var, let, func, func*, obj
export { export, list }; // named export at the end of the module
export { export as newName, list }; // named export at the end of the module with renames
export default function () { ... } // default export: func, class; no semicolon
export default function myFunc () { ... } // default export: func, class; no semicolon
export default myExpression; // default export as an expression
export default (function () { ... }); // default export as an expression: func, class
export * from 'src/lib'; // namespace reexport
export { func as myFunc, otherFunc } from 'src/lib'; // named reexport
export { func as default } from 'src/lib'; // default reexport
```

- imports are: executed once, allowed only at the top level, relative and absolute paths allowed, .js might be ommited, hoisted

```javascript
import { named, list } from "mylib"; // named import
import { named as otherName, list as anotherName } from "mylib"; // named import with renames
import * from "src/mylib"; // namespace import
import myFunc from "./mylib"; // default import
import { default as myName } from "./mylib"; // renamed default import
import "mylib"; // empty import
import myDefault, * from "mylib"; // combined default and namespace import
import myDefault, { name1, name2 } from "mylib"; // combined default and name import
```

```html
<script type="module">
  <!-- by default strict mode, module scope, without this, asynchronous, with declarative and programmatic imports -->
</script>
```

## Sources

- [Dr. Axel Rauschmayer - Exploring ES6](https://exploringjs.com/es6/index.html)
