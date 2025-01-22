---
title: "ECMAScript 2023 (ES14) 新特性"
description: "ECMAScript 2023 (ES14) 新特性详解"
pubDate: "Jul 08 2023"
heroImage: "/blog-placeholder-5.jpg"
---

### ECMAScript 2023 (ES14) 新特性详解

ECMAScript（简称 ES）是 JavaScript 的标准规范，每年都会发布一个新的版本，逐步扩展和改进语言特性。2023 年，ES14（ECMAScript 2023）如期而至，带来了几个非常有用的新特性和优化，进一步提升了开发者编写高效、可维护代码的体验。本文将详细介绍 ECMAScript 2023 中的关键更新和它们的实际应用场景。

---

### 1. **Array.prototype.findLast 和 Array.prototype.findLastIndex**

在 JavaScript 数组操作中，我们通常使用 `find()` 和 `findIndex()` 来查找符合条件的元素及其索引，但这些方法从数组的起始位置开始查找，有时候我们希望从数组的末尾开始查找。ECMAScript 2023 为此引入了 `findLast()` 和 `findLastIndex()`。

- **`findLast(callback)`**：从数组末尾向前遍历，返回满足条件的第一个元素。
- **`findLastIndex(callback)`**：从数组末尾向前遍历，返回满足条件的第一个元素的索引。

**示例：**

```javascript
const arr = [1, 2, 3, 4, 5, 6];

// findLast: 找到最后一个偶数
const lastEven = arr.findLast((x) => x % 2 === 0);
console.log(lastEven); // 输出 6

// findLastIndex: 找到最后一个偶数的索引
const lastEvenIndex = arr.findLastIndex((x) => x % 2 === 0);
console.log(lastEvenIndex); // 输出 5
```

这两个方法使我们在处理从末尾开始的数组查询时更加简洁和高效。

---

### 2. **Symbol.prototype.description**

在过去，`Symbol` 是 JavaScript 中一种独特的基本类型，用于创建唯一的标识符。但在获取 `Symbol` 描述时，我们通常需要通过显式转换为字符串才能查看。这次更新简化了这一过程，`Symbol.prototype.description` 提供了一种更直接的方式来访问符号的描述。

**示例：**

```javascript
const sym = Symbol("example");
console.log(sym.description); // 输出 "example"
```

这使得 `Symbol` 的调试和描述更加直观，提升了可读性。

---

### 3. **Change Array by Copy: `toReversed`, `toSorted`, `toSpliced`, `with`**

为了改进数组操作的不可变性，ECMAScript 2023 引入了几种“通过拷贝修改”的方法。这些方法不会修改原始数组，而是返回一个经过变更的新数组。

- **`toReversed()`**：返回一个倒序的新数组。
- **`toSorted(compareFn)`**：返回一个经过排序的新数组。
- **`toSpliced(start, deleteCount, ...items)`**：返回一个移除或替换部分元素的新数组。
- **`with(index, value)`**：返回一个特定索引处被替换的新数组。

**示例：**

```javascript
const arr = [1, 2, 3];

// toReversed
const reversedArr = arr.toReversed();
console.log(reversedArr); // 输出 [3, 2, 1]

// toSorted
const sortedArr = [3, 1, 2].toSorted();
console.log(sortedArr); // 输出 [1, 2, 3]

// toSpliced
const splicedArr = arr.toSpliced(1, 1);
console.log(splicedArr); // 输出 [1, 3]

// with
const newArr = arr.with(1, 5);
console.log(newArr); // 输出 [1, 5, 3]
```

这些方法提供了更加简洁的操作方式，同时保留了原数组的不可变性，特别适用于函数式编程风格。

---

### 4. **Hashbang（#!）支持**

ECMAScript 2023 增加了对哈希邦（`#!`）的支持，通常用于在类 Unix 环境下的脚本文件中指定解释器路径。这在开发 Node.js 脚本时尤其有用。现在，JavaScript 引擎会自动忽略以 `#!` 开头的内容。

**示例：**

```javascript
#!/usr/bin/env node
console.log("Hello from Node.js script");
```

上面的例子告诉操作系统使用 Node 程序来运行脚本。

现在，你可以使用 `./fileName.js` 来运行 JavaScript 代码，而不是 `node fileName.js`。

`#!` 也被称为 sharp-exclamation、hashbang、pound-bang 或 hash-pling。

这项更新使得 JavaScript 脚本的跨平台执行更加方便，不再需要额外的工具来处理哈希邦注释。

---

### 5. **Improved Error Cause (错误原因改善)**

ES14 改进了`Error`对象，现在可以通过`cause`属性来传递和查看导致当前错误的原因。这对于在复杂的错误处理场景下，保留和传递错误上下文信息非常有帮助。

**示例：**

```javascript
try {
	throw new Error("Initial error", { cause: "Database connection failed" });
} catch (e) {
	console.log(e.message); // 输出 "Initial error"
	console.log(e.cause); // 输出 "Database connection failed"
}
```

通过 `cause` 属性，我们可以更详细地记录和追踪错误来源，提升调试和日志记录的效率。

---

### 6. **WeakRef 和 FinalizationRegistry 的加强**

虽然 `WeakRef` 和 `FinalizationRegistry` 在之前的版本中已被引入，2023 年对它们进行了性能优化和行为改善，提升了内存回收的效率。尽管这些特性使用较少，但它们在特定的内存敏感型应用中非常重要。

---

### 7. **Symbols as WeakMap keys**

**示例：**

```javascript
const weak = new WeakMap();
const key = Symbol("ref");

weak.set(key, "Hello, ES2023!");

console.log(weak.get(key)); // Output: Hello, ES2023!
```

这允许使用独特的 Symbol 作为键。目前，WeakMap 仅限于允许对象作为键。对象被用作 WeakMap 的键，是因为它们具有相同的身份特性。

Symbol 是 ECMAScript 中唯一允许唯一值的原始类型，因此使用 Symbol 作为键，而不是为 WeakMap 创建一个新的对象。

---

###

### 总结

ECMAScript 2023 带来的这些改进，进一步增强了 JavaScript 的可用性和开发者体验。无论是更灵活的数组操作、更清晰的错误处理，还是为不可变数据结构提供的新方法，这些特性都能帮助开发者编写更加高效、清晰和可维护的代码。随着 JavaScript 生态的不断演进，我们可以期待这些特性在未来的项目中发挥越来越重要的作用。

开发者可以开始在项目中尝试这些新特性，结合现代的开发工具和构建环境，将这些新功能纳入日常开发实践中，提升开发效率和代码质量。

**参考资源：**

- [ECMAScript 2023 提案](https://github.com/tc39/proposals)
- [MDN Web Docs - ECMAScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

---
