# 谷歌 Objective-C 风格指南

例子省略

github地址：

https://github.com/google/styleguide/blob/gh-pages/objcguide.md

中文翻译地址：

http://zh-google-styleguide.readthedocs.io/en/latest/google-objc-styleguide/spacing/

## 空格和格式

### 空格 VS 制表符

只使用空格，一次只用2个空格。在代码里使用空格代替制表符。

将你的文本编辑器设置成自动将制表符替换成空格。

### 行宽

Objective-C最大行宽是100列。

你可以通过在Xcode里设置 *Preferences > Text Editing >
Page guide at column: 100* 更容易发现越界。(默认是80)

### 方法声明与定义

在`-`和`+`之间以及返回类型使用一个空格，参数列表中只有参数之间可以有空格。

方法应该像这样：

```objective-c
- (void)doSomethingWithString:(NSString *)theString {
  ...
}
```

星号前的空格是可选的。当写新的代码时，要与先前代码保持一致。

如果一行有非常多的参数，更好的方式是将每个参数单独拆成一行。如果使用多行，将每个参数前的冒号对齐。

```objective-c
- (void)doSomethingWith:(GTMFoo *)theFoo
                   rect:(NSRect)theRect
               interval:(float)theInterval {
  ...
}
```

当第一个关键字比其它的短时，保证下一行至少有 4 个空格的缩进。这样可以使关键字垂直对齐，而不是使用冒号对齐：

```objective-c
- (void)short:(GTMFoo *)theFoo
    longKeyword:(NSRect)theRect
    evenLongerKeyword:(float)theInterval {
  ...
}
```

### 条件句

在`if` , `while` , `for` 和 `switch` 以及比较运算符的后面加一个空格

```objective-c
// GOOD:

for (int i = 0; i < 5; ++i) {
}

while (test) {};
```
当循环体或条件语句适合于单行时，括号可以省略

```objective-c
// GOOD:

if (hasSillyName) LaughOutLoud();

for (int i = 0; i < 10; i++) {
  BlowTheHorn();
}
```

```objective-c
// AVOID:

if (hasSillyName)
  LaughOutLoud();               // AVOID.

for (int i = 0; i < 10; i++)
  BlowTheHorn();                // AVOID.
```

如果一个 ` if `有一个 ` else `句子，两个句子都需要括号

```objective-c
//GOOD:

if (hasBaz) {
  foo();
} else {
  bar();
}
```

```objective-c
// AVOID:

if (hasBaz) foo();
else bar();        // AVOID.

if (hasBaz) {
  foo();
} else bar();      // AVOID.
```

 使用switch时，除非下一个case没有代码，否则要加注释来记录。

```objective-c
// GOOD:

switch (i) {
  case 1:
    ...
    break;
  case 2:
    j++;
    // Falls through.
  case 3: {
    int k;
    ...
    break;
  }
  case 4:
  case 5:
  case 6: break;
}
```

### 表达式



