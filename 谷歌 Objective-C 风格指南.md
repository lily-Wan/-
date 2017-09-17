

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

### 条件语句

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

在二元运算符和赋值前后加一个空格，一元则省略空格，不要在小括号里添加空格。

```objective-c
// GOOD:

x = 0;
v = w * x + y / z;
v = -y * (x + z);
```

表达式内的因子可以省略空格

```objective-c
// GOOD:

v = w*x + y/z;
```

### 方法调用

方法调用的格式应该像方法声明。

在选择格式样式时，遵循已经在给定源文件中使用的约定。方法调用时，所有参数应该在同一行：

```objective-c
// GOOD:

[myObject doFooWith:arg1 name:arg2 error:arg3];
```

或者每行一个参数，以冒号对齐:

```objective-c
// GOOD:

[myObject doFooWith:arg1
               name:arg2
              error:arg3];
```

不要使用下面的缩进风格:

```objective-c
// AVOID:

[myObject doFooWith:arg1 name:arg2  // some lines with >1 arg
              error:arg3];

[myObject doFooWith:arg1
               name:arg2 error:arg3];

[myObject doFooWith:arg1
          name:arg2  // aligning keywords instead of colons
          error:arg3];
```

方法定义与方法声明一样，当关键字的长度不足以以冒号对齐时，下一行都要以四个空格进行缩进。

```objective-c
// GOOD:

[myObj short:arg1
          longKeyword:arg2
    evenLongerKeyword:arg3
                error:arg4];
```

总结:方法定义的格式与方法声明的格式非常相似。当格式的风格有多种选择时，新的代码要与已经存在的代码保持一致。

### 函数调用

函数调用应该包括在每行上的所有参数，除了需要更短的行来清晰或文档化参数。

函数参数的扩展行可以缩进与开括号对齐，或者一个四空格缩进。

```objective-c
// GOOD:

CFArrayRef array = CFArrayCreate(kCFAllocatorDefault, objects, numberOfObjects,
                                 &kCFTypeArrayCallBacks);

NSString *string = NSLocalizedStringWithDefaultValue(@"FEET", @"DistanceTable",
    resourceBundle,  @"%@ feet", @"Distance for multiple feet");

UpdateTally(scores[x] * y + bases[x],  // Score heuristic.
            x, y, z);

TransformImage(image,
               x1, x2, x3,
               y1, y2, y3,
               z1, z2, z3);
```

使用带有描述性名称的局部变量来缩短函数调用和减少调用的嵌套。

```objective-c
// GOOD:

double scoreHeuristic = scores[x] * y + bases[x];
UpdateTally(scoreHeuristic, x, y, z);
```

### 异常

在前一个`}` 的同一行有`@catch`和`finally`标签的格式异常，在`@`标签和左大括号`{`之间，还有在`@catch`和被捕捉到的异常对象的声明之间添加一个空格。

如果你决定使用 Objective-C 的异常，那么就按下面的格式。不过你最好先看看 避免抛出异常了解下为什么不要使用异常。

```objective-c
// GOOD:

@try {
  foo();
} @catch (NSException *ex) {
  bar(ex);
} @finally {
  baz();
}
```

### 函数长度

偏向使用短小精炼的函数。

长函数和方法有时是适当的，因此没有硬性限制在函数长度上。如果一个函数超过40行，考虑它是否可以在不损害程序结构的情况下被分解。

即使你的长函数现在运行得很好，但在几个月内修改它可能会增加新的行为。这可能会导致很难找到的错误。使您的函数短小简单，使其他人更容易阅读和修改您的代码。

在更新遗留代码时，也要考虑将长函数分解成更小更易于管理的部分。

### 垂直留白

有节制的使用垂直空格。

为了让更多的代码可以在屏幕上轻松浏览，避免在函数的括号内设置空白行。

在函数之间和逻辑组之间限制空白行。

##命名

在合理范围内，名称应该尽可能的描述详尽。遵循苹果命名规范 [Objective-C naming rules](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html)。

避免非标准的缩写。不要担心水平空间不够用，因为更重要的是让您的代码可以立即被新的读者理解。举例：

```objective-c
// GOOD:

// Good names.
int numberOfErrors = 0;
int completedConnectionsCount = 0;
tickets = [[NSMutableArray alloc] init];
userInfo = [someObject object];
port = [network port];
NSDate *gAppLaunchDate;
```

```objective-c
// AVOID:

// Names to avoid.
int w;
int nerr;
int nCompConns;
tix = [[NSMutableArray alloc] init];
obj = [someObject object];
p = [network port];
```

任何类、类别、方法、函数或变量名称都应该在名称中使用所有大写字母缩写和初始化。这遵循了苹果公司使用所有大写字母的标准，如URL、ID、TIFF和EXIF。

### 文件名

文件名应该反映类名实现以及包含的例子。

遵循你所参与项目的约定。文件的扩展名应该如下：

| Extension | Type                              |
| --------- | --------------------------------- |
| .h        | C/C++/Objective-C header file     |
| .m        | Objective-C implementation file   |
| .mm       | Objective-C++ implementation file |
| .cc       | Pure C++ implementation file      |
| .c        | C implementation file             |

包含在项目中共享或在大型项目中使用的代码的文件应该有一个非常独特的名称，通常包括项目或类前缀。

类别的文件名应该包含被扩展的类名，像`GTMNSString+Utils.h` 或`NSTextView+GTMAutocomplete.h`

### 类名

类名（以及类别、协议名）应首字母大写，并以驼峰格式分割单词。

当设计的代码在多个应用程序之间共享时，可接受和推荐前缀(例如`GTMSendMessage`)。还建议对依赖于外部库的大型应用程序的类进行前缀。

### 类别名

类别名应该有两三个字母的前缀以表示类别是项目的一部分或者该类别是通用的。类别名应该包含它所扩展的类的名字。

类别名称应该包含它所扩展的类的名称。举例，比如我们要基于 `NSString` 创建一个用于解析的类别，我们将把类别放在一个名为 `GTMNSString+Parsing.h` 的文件中。类别本身命名为 `GTMStringParsingAdditions` （是的，我们知道类别名和文件名不一样，但是这个文件中可能存在多个不同的与解析有关类别）。类别中的方法应该以 `gtm_myCategoryMethodOnAString:` 为前缀以避免命名冲突。

类名与包含类别名的括号之间，应该以一个空格分隔。

```objective-c
// GOOD:

// Using a category to extend a Foundation class.
@interface NSString (GTMNSStringParsingAdditions)
- (NSString *)gtm_parsedString;
@end
```

### Objective-C 方法名

方法名和参数名应该以小写字母开头，并混合驼峰格式。

可以适当的大写，包括在名字的开始。

```objective-c
// GOOD:

+ (NSURL *)URLWithString;
```

方法名应尽量读起来就像句子，这表示你应该选择与方法名连在一起读起来通顺的参数名。objective - c方法的名称往往很长，但这有一个好处，一个代码块几乎可以像散文一样阅读，从而使许多实现注释变得不必要。

只有在必要的地方阐明方法的含义或行为,才在第二个和后面的参数名中使用介词和连词，如`with`，`from`，和`to`。

```objective-c
// GOOD:

- (void)addTarget:(id)target action:(SEL)action;                          // GOOD; no conjunction needed
- (CGPoint)convertPoint:(CGPoint)point fromView:(UIView *)view;           // GOOD; conjunction clarifies parameter
- (void)replaceCharactersInRange:(NSRange)aRange
            withAttributedString:(NSAttributedString *)attributedString;  // GOOD.
```

返回对象的方法应该以名词开头,确定返回的对象:

```objective-c
// GOOD:

- (Sandwich *)sandwich;      // GOOD.
```

```objective-c
// AVOID:

- (Sandwich *)makeSandwich;  // AVOID.
```
访问器方法应该与他们 要获取的 成员变量的名字一样，但不应该以get作为前缀。例如:

```objective-c
// GOOD:

- (id)delegate;     // GOOD.
```

```objective-c
// AVOID:

- (id)getDelegate;  // AVOID.
```

返回布尔型形容词值的访问器的方法名称以is开头，但这些方法的属性名省略了is。

点表示法只使用属性名，而不是用方法名。

```objective-c
// GOOD:

@property(nonatomic, getter=isGlorious) BOOL glorious;
- (BOOL)isGlorious;

BOOL isGood = object.glorious;      // GOOD.
BOOL isGood = [object isGlorious];  // GOOD.
```

```objective-c
// AVOID:

BOOL isGood = object.isGlorious;    // AVOID.
```

```objective-c
// GOOD:

NSArray<Frog *> *frogs = [NSArray<Frog *> arrayWithObject:frog];
NSEnumerator *enumerator = [frogs reverseObjectEnumerator];  // GOOD.
```

```objective-c
// AVOID:

NSEnumerator *enumerator = frogs.reverseObjectEnumerator;    // AVOID.
```

观看苹果官方命名守则以获得更多Objective-C命名方面的细节。

这些规则仅适用于Objective-C方法。C++方法则继续遵循C++风格规范。

### 函数名

通常情况下函数是复杂的。

一般来说，函数应该从大写字母开始，每个新单词都有大写字母(又名`驼峰命名法`和`帕斯卡拼写法`)。

```objective-c
// GOOD:

static void AddTableEntry(NSString *tableEntry);
static BOOL DeleteFile(char *filename);
```

因为objective - c不提供命名空间，非静态函数应该有一个前缀，以最大程度减少冲突的机会。

```objective-c
// GOOD:

extern NSTimeZone *GTMGetDefaultTimeZone();
extern NSString *GTMGetURLScheme(NSURL *URL);
```

### 变量名

变量名应该以小写字母开头，并使用驼峰格式。

实例变量有突出显示。档案范围或全局变量有一个前缀`g`。比如，`myLocalVariable`, `_myInstanceVariable`, `gMyGlobalVariable`.

#### 普通变量名

读者应该能够根据名称推断出变量类型，但不要使用匈牙利命名法来表示语法属性，例如变量的静态类型(int或指针)。

文件范围或全局变量(相对于常量)在方法或函数的范围之外声明是很少见的，应该有前缀`g`。

```objective-c
// GOOD:

static int gGlobalCounter;
```

#### 实例变量

实例变量应该混合大小写，并以下划线作为前缀，如 `_usernameTextField`。

注意：谷歌之前的Objective-C实例变量规范提到的是后置下划线。现有的项目可能会选择继续使用新代码中的后置应该在每个类中维护前缀或后缀的一致性。下划线，以保持项目代码库中的一致性。

#### 常量

常量符号(const全局和静态变量和由# define创建的常量)应该使用驼峰格式分隔单词。

常量应该有一个适当的前缀。

```objective-c
// GOOD:

extern NSString *const GTLServiceErrorDomain;

typedef NS_ENUM(NSInteger, GTLServiceError) {
  GTLServiceErrorQueryResultMissing = -3000,
  GTLServiceErrorWaitTimedOut       = -3001,
};
```

因为objective - c不提供命名空间，所以外部链接的常量应该有一个前缀，可以将名称冲突的几率降到最低，通常是`ClassNameConstantName`或`ClassNameEnumName`。

由于Swift代码的互操作性，枚举值应该具有扩展typedef名称的名称:

```objective-c
// GOOD:

typedef NS_ENUM(NSInteger, DisplayTinge) {
  DisplayTingeGreen = 1,
  DisplayTingeBlue = 2,
};
```

常量名应该以小写字母 `k` 开头

```objective-c
// GOOD:

static const int kFileCount = 12;
static NSString *const kUserKey = @"kUserKey";
```

##类型和声明

### 局部变量

在最实用的范围内来命名变量，并接近他们的用途。在其声明中初始化变量。

```objective-c
// GOOD:

CLLocation *location = [self lastKnownLocation];
for (int meters = 1; meters < 10; meters++) {
  reportFrogsWithinRadius(location, meters);
}
```

偶尔，为了提高效率，在使用范围外声明一个变量更合适。这个示例声明了与初始化不同的`meter`，并不需要在每次循环中发送`lastKnownLocation`消息：

```objective-c
// AVOID:

int meters;                                         // AVOID.
for (meters = 1; meters < 10; meters++) {
  CLLocation *location = [self lastKnownLocation];  // AVOID.
  reportFrogsWithinRadius(location, meters);
}
```

在自动引用计数中，指向Objective-C对象的指针默认为`nil`，所以不需要对`nil`进行显式初始化

### 无符号整数

除了系统接口使用的匹配类型外，避免无符号整数。

在使用无符号整数进行数学计算或计算为零时，会出现一些细微的错误。当在系统接口中匹配NSUInteger时，仅使用依赖于数学表达式中的有符号整数。

```objective-c
// GOOD:

NSUInteger numberOfObjects = array.count;
for (NSInteger counter = numberOfObjects - 1; counter > 0; --counter)
```

```objective-c
// AVOID:

for (NSUInteger counter = numberOfObjects - 1; counter > 0; --counter)  // AVOID.
```

无符号整数可以用于标记和位掩码，不过通常`NS_OPTIONS`或`NS_ENUM`会更合适。

### 大小不一致的编码

由于32位和64位构建的大小不同，避免使用`long`、`NSInteger`、`NSUInteger`和`CGFloat`，除非匹配系统接口。

`long`、`NSInteger`、`NSUInteger`和`CGFloat`类型的大小在32 - 64位构建之间变化。在处理由系统接口公开的值时，使用这些类型是合适的，但是对于大多数其他计算都应该避免使用这些类型。

```objective-c
// GOOD:

int32_t scalar1 = proto.intValue;

int64_t scalar2 = proto.longValue;

NSUInteger numberOfObjects = array.count;

CGFloat offset = view.bounds.origin.x;
```

```objective-c
// AVOID:

NSInteger scalar2 = proto.longValue;  // AVOID.
```

文件和缓冲区大小通常超过32位限制，因此应该使用`int64_t`声明，而不是用`long`、`NSInteger`或`NSUInteger`。

## 注释

注释对于保持我们的代码可读非常重要。下面的规则给出了你应该做什么注释、在哪进行注释。记住：尽管注释很重要，但最好的代码应该自成文档。与其给类型及变量起一个晦涩难懂的名字，再为它写注释，不如直接起一个有意义的名字。

注意标点、拼写和语法。比起写得不好的注释，阅读有好的注释要容易得多。

注释应该像叙述文本一样可读，具有适当的大写和标点符号。在许多情况下，完整的句子比句子片段更具可读性。较短的注释，例如在一行代码末尾的注释，有时可以不那么正式，但是使用一致的样式。当你写注释时，为你的读者写:下一个需要理解你的代码的贡献者。慷慨一点——下一个可能就是你!

### 文件注释

每个文件的开头以文件内容的简要描述起始。每个文件可能包含以下事项:

- 必要的话，加上许可证样板。为项目选择一个合适的授权样板
- 如有必要，加上文件内容的简要描述

如果你对其他人的原始代码作出重大的修改，那么考虑删除作者行，因为修订历史已经提供了更详细和更准确的作者身份记录。

### 声明注释

每一个重要的接口，共有和私有的，都应该伴有一个注释来描述它的目的以及它如何适应更大的图景。

注释应该用于文档类、属性、实例变量、函数、类别、协议声明和枚举。

```objective-c
// GOOD:

/**
 * A delegate for NSApplication to handle notifications about app
 * launch and shutdown. Owned by the main app controller.
 */
@interface MyAppDelegate : NSObject {
  /**
   * The background task in progress, if any. This is initialized
   * to the value UIBackgroundTaskInvalid.
   */
  UIBackgroundTaskIdentifier _backgroundTaskID;
}

/** The factory that creates and manages fetchers for the app. */
@property(nonatomic) GTMSessionFetcherService *fetcherService;

@end
```

在使用Xcode解析格式化文档时，鼓励使用doxygenstyle风格注释接口。有各种各样的Doxygen命令;在项目中始终如一地使用它们。

如果你已经在文件头部详细描述了接口，可以直接说明 “完整的描述请参见文件头部”，但是一定要有这部分注释。

另外，每个方法都应该有注释来解释它的作用、参数、返回值、线程或队列假设以及其它影响。文档注释应该在公共方法的头文件中，或者在重要私有方法的前面。

在为方法和函数注释时，使用描述性形式(`Opens the file`)而不是命令形式(`Open the file`)。注释只是为了描述函数而不是告诉函数做什么。

为类的线程安全性，属性或方法作注释，如果有的话。如果一个类的实例可以被多个线程访问，那么要格外小心来记录多线程使用的规则和不变量。

属性和实例变量的任何标记值，如`NULL`或`- 1`，都应该在注释中记录。

 声明注释解释了如何使用方法或函数。注释解释如何实现方法或函数的注释应该与实现而不是声明。

### 实现注释

提供注释解释复杂的、微妙的或复杂的代码段。

```objective-c
// GOOD:

// Set the property to nil before invoking the completion handler to
// avoid the risk of reentrancy leading to the callback being
// invoked again.
CompletionHandler handler = self.completionHandler;
self.completionHandler = nil;
handler();
```

当有用的时候，也提供关于被考虑或放弃的实现方法的注释。

行尾注释应该与代码分开至少2个空格。如果您对后续行有几条注释，则通常可以更容易地将其对齐。

```objective-c
// GOOD:

[self doSomethingWithALongName];  // Two spaces before the comment.
[self doSomethingShort];          // More spacing to align the comment.
```

### 消除二义性符号

在需要避免歧义的地方，使用倒引号或竖线在注释中引用变量名和符号比使用引号或将在行内命名符号更好。

在Doxygen风格的注释中，偏向用一个单空间文本命令来划分符号，比如`@c`。

当一个符号是一个常见的词，它可能会使句子看起来像它的构造很差时，界定有助于使它清晰。一个常见的例子是符号`count`:

```objective-c
// GOOD:

// Sometimes `count` will be less than zero.
```

或者引用已经包含引号的内容时

```objective-c
// GOOD:

// Remember to call `StringWithoutSpaces("foo bar baz")`
```

当一个符号是自显形的时候，不需要倒引号或竖线。

```objective-c
// GOOD:

// This class serves as a delegate to GTMDepthCharge.
```

Doxygen格式也适用于识别符号。

```objective-c
// GOOD:

/** @param maximum The highest value for @c count. */
```

###对象所有权

对于没有被ARC管理的对象，当与 Objective-C 最常规的作法不同时，尽量使指针的所有权模型尽量明确。

#### 手动引用计数

继承自 `NSObject` 的对象的实例变量指针，通常被假定是强引用关系（retained），某些情况下也可以注释为弱引用（weak）或使用 `__weak` 生命周期限定符。

Mac软件中的一个例外是标记为`@IBOutlets`的实例变量，这些变量被假定为不被保留。

如果实例变量是指向`Core Foundation`、`c++`和其他非`objective - C`对象的指针，则应该始终用强而弱的注释声明它们，以指示哪些指针是，哪些不是保留的。核心基础和其他`非Objective-C`对象指针需要显式内存管理，即使在构建自动引用计数时也是如此。

强引用及弱引用声明的例子：

```objective-c
// GOOD:

@interface MyDelegate : NSObject

@property(nonatomic) NSString *doohickey;
@property(nonatomic, weak) NSString *parent;

@end


@implementation MyDelegate {
  IBOutlet NSButton *_okButton;  // Normal NSControl; implicitly weak on Mac only

  AnObjcObject *_doohickey;  // My doohickey
  __weak MyObjcParent *_parent;  // To send messages back (owns this instance)

  // non-NSObject pointers...
  CWackyCPPClass *_wacky;  // Strong, some cross-platform object
  CFDictionaryRef *_dict;  // Strong
}
@end
```

#### 自动引用计数

对象所有权和生命周期在使用ARC时是显式的，因此不需要额外的注释来自动保留对象。

## C 语言特性

### 宏

避免宏，特别是常量，枚举，XCode片段，或者C函数的地方。

宏使您看到的代码与编译器看到的代码不同。现代C使常量和实用函数的传统用法变得没有必要。宏只能在没有其他可用的解决方案时使用。

在需要宏的地方，使用一个惟一的名称来避免编译单元中符号碰撞的风险。如果实用，请保留在使用后未定义宏的范围。

宏名称应该使用`shouty_snake_case` ——所有大写字母在单词之间加上下划线。函数类宏可以使用C函数命名操作。不要定义似乎是C或objective - C关键字的宏。

```objective-c
// GOOD:

#define GTM_EXPERIMENTAL_BUILD ...      // GOOD

// Assert unless X > Y
#define GTM_ASSERT_GT(X, Y) ...         // GOOD, macro style.

// Assert unless X > Y
#define GTMAssertGreaterThan(X, Y) ...  // GOOD, function style.
```

```objective-c
// AVOID:

#define kIsExperimentalBuild ...        // AVOID

#define unless(X) if(!(X))              // AVOID
```

避免宏扩展到使C或objective - C结构不平衡。避免引入范围的宏，或者可能模糊代码块中值的捕获。

避免在header中生成类、属性或方法定义的宏作为公共API使用。这只会让代码难以理解，而语言已经有更好的方法来实现这一点。

避免生成方法实现的宏，或者生成在宏之外使用的变量声明。宏不应该通过隐藏在何处以及如何声明变量来让代码难以理解。

```objective-c
// AVOID:

#define ARRAY_ADDER(CLASS) \
  -(void)add ## CLASS ## :(CLASS *)obj toArray:(NSMutableArray *)array

ARRAY_ADDER(NSString) {
  if (array.count > 5) {              // AVOID -- where is 'array' defined?
    ...
  }
}
```

断言和调试日志宏可以接受使用宏，这些宏是根据构建设置有条件地编译的，通常都没有编译成发布版本。

### 非标准扩展

C/Objective-C 的非标准扩展除非指定否则可能不会被使用。

编译器支持不属于标准c语言的各种扩展，包括复合语句表达式 （例如: `foo = ({ int x; Bar(&x); x })` )和变长数组。

`__attribute__`是一个被认可的异常，因为它在objective-API规范中被使用。

条件运算符的二进制形式，`A ?: B`，是一个被认可的例外。

## Cocoa 和 Objective-C 特性

### 明确指定构造函数

清楚地标识你的指定的初始化器。

对于需要继承你的类的人来说，明确指定构造函数十分重要。这样他们就可以只重写一个构造函数（可能是几个）来保证他们的子类的构造函数会被调用。这也有助于将来别人调试你的类时，理解初始化代码的工作流程。使用注释或`NS_DESIGNATED_INITIALIZER` 宏来识别指定构造函数。如果你使用`NS_DESIGNATED_INITIALIZER`，用 `NS_UNAVAILABLE`来标记不支持的构造函数。

### 重载指定构造函数

当你写子类的时候，如果需要 `init…` 方法，确保重载父类的指定构造函数。

如果你没有重载父类的指定构造函数，你的构造函数有时可能不会被调用，这会导致非常隐秘而且难以解决的 bug。

### 重载 `NSObject` 的方法

在 `@implementation` 的顶部重载 `NSObject` 类的方法。

通常适用（但不局限）于 `init...`，`copyWithZone:`，以及 `dealloc` 方法。所有 `init...` 方法应该放在一起，其后是其他典型的 `NSObject`方法，比如`description` ，`isEqual:`，`hash`。

可能在NSObject方法之前创建实例的便利类工厂方法。

### 初始化

不要在 `init` 方法中，将成员变量初始化为 `0` 或者 `nil`；毫无必要。

刚分配的对象，默认值都是 0，除了 `isa` 指针。所以不要在初始化器里面写一堆将成员初始化为 `0` 或者 `nil` 的代码。

### 头文件中的成员变量应该是`@protected`或`@private`

成员变量通常应该在实现文件中声明，或者由属性自动生成。当在头文件中声明成员变量时，应该将其标记为`@protected`或`@private`。

```objective-c
// GOOD:

@interface MyClass : NSObject {
 @protected
  id _myInstanceVariable;
}
@end
```

### 避免 `+new`

不要调用 `NSObject` 类方法 `new`，也不要在子类中重载它。使用 `alloc` 和 `init`方法创建并初始化对象。

现代的 Ojbective-C 代码通过调用 `alloc` 和 `init` 方法来创建并 retain 一个对象。由于类方法 `new` 很少使用，这使得有关内存分配的代码审查更困难。

### 保持公共API尽量简单

保持类简单；避免 “厨房水槽（kitchen-sink）” 式的 API。如果一个函数压根没必要公开，就把它放在公共接口之外。

与 C++ 不同，Objective-C 没有方法来区分公共的方法和私有的方法；任何消息都会被发送到一个对象。因此，除非被类的用户使用，不要把这个方法放进公共 API 中。尽可能的避免了你你不希望被调用的方法却被调用到。这包括重载父类的方法。

再次说明，“私有的” 方法其实不是私有的。你有时可能不小心重载了父类的私有方法，因而制造出很难查找的 Bug。通常，私有的方法应该有一个相当特殊的名字以防止子类无意地重载它们。

### #import 和 #include 

`#import` Ojbective-C/Objective-C++ 头文件，`#include` C/C++ 头文件。

基于你所包括的头文件的编程语言，选择使用 `#import` 或是 `#include`。

当包含一个使用 Objective-C、Objective-C++ 的头文件时，使用 `#import` 。当包含一个使用标准 C、C++ 头文件时，使用 `#include`。头文件应该使用 `#define` 保护。

### includes的顺序

头包的标准顺序是相关的头文件、操作系统头文件、语言库头文件，以及其他依赖项的头组。

相关的头文件在其他的前面，以确保它没有隐藏的依赖项。对于实现文件，相关的头文件是头文件。对于测试文件，相关的头是包含测试接口的头文件。

空白行可以分隔包含标题的逻辑上不同的组。

使用项目源目录相关联的路径导入头文件。

```objective-c
// GOOD:

#import "ProjectX/BazViewController.h"

#import <Foundation/Foundation.h>

#include <unistd.h>
#include <vector>

#include "base/basictypes.h"
#include "base/integral_types.h"
#include "util/math/mathutil.h"

#import "ProjectX/BazModel.h"
#import "Shared/Util/Foo.h"
```

### 为系统框架使用Umbrella Headers

为系统框架和系统库导入 umbrella header ，而不是包含单独的文件。

当你试图从框架（如 Cocoa 或者 Foundation）中包含若干零散的系统头文件时，实际上包含顶层根框架的话，编译器要做的工作更少。根框架通常已经经过预编译，加载更快。另外记得使用 `#import` 而不是 `#include` 来包含 Objective-C 的框架。

```objective-c
// GOOD:

@import UIKit;     // GOOD.
#import <Foundation/Foundation.h>     // GOOD.
```

```objective-c
// AVOID:

#import <Foundation/NSArray.h>        // AVOID.
#import <Foundation/NSString.h>
...
```
### `init` 和 `dealloc` 内避免使用访问器

在 `init` 和 `dealloc` 方法执行的过程中，子类可能会处在一个不一致的状态，所以这些方法中的代码应避免调用 self 访问器。

子类尚未初始化，或在 `init` 和 `dealloc` 方法执行时已经被销毁，会使访问器方法很可能不可靠。实际上，应在这些方法中直接对实例变量进行赋值或释放操作。

```objective-c
// GOOD:

- (instancetype)init {
  self = [super init];
  if (self) {
    _bar = 23;  // GOOD.
  }
  return self;
}
```

```objective-c
// AVOID:

- (instancetype)init {
  self = [super init];
  if (self) {
    self.bar = 23;  // AVOID.
  }
  return self;
}
```

```objective-c

- (void)dealloc {
  [_notifier removeObserver:self];  // GOOD.
}
```

```objective-c
// AVOID:

- (void)dealloc {
  [self removeNotifications];  // AVOID.
}
```

### setter 应复制 NSStrings

使用`NSString`的setter应该总是复制它所接受的字符串。这通常也适用于`NSArray`和`NSDictionary`之类的集合。

不要仅仅保留字符串，因为它可能是一个`NSMutableString`。这就避免了调用者在您不知情的情况下更改它。

接收和保存集合对象的代码也应该考虑到传递的集合可能是可变的，因此集合可以更安全地作为原始副本的副本或可变副本被保存。

```objective-c
// GOOD:

@property(nonatomic, copy) NSString *name;

- (void)setZigfoos:(NSArray<Zigfoo *> *)zigfoos {
  // Ensure that we're holding an immutable collection.
  _zigfoos = [zigfoos copy];
}
```

### 使用轻量级泛型来记录包含的类型

所有在Xcode 7或更新版本上编译的项目都应该使用 Objective-C 轻量级泛型表示法来输入包含的对象。

每个`NSArray`、`NSDictionary`或`NSSet`引用都应该使用轻量级泛型进行声明，以改进类型安全性，并显式地记录使用情况。

```objective-c
// GOOD:

@property(nonatomic, copy) NSArray<Location *> *locations;
@property(nonatomic, copy, readonly) NSSet<NSString *> *identifiers;

NSMutableArray<MyLocation *> *mutableLocations = [otherObject.locations mutableCopy];
```

如果完全注释的类型变得复杂，请考虑使用类型定义来保持可读性。

```objective-c
// GOOD:

typedef NSSet<NSDictionary<NSString *, NSDate *> *> TimeZoneMappingSet;
TimeZoneMappingSet *timeZoneMappings = [TimeZoneMappingSet setWithObjects:...];
```

使用最具描述性的公共父类或协议。在最常见的情况下，当没有其他已知的情况时，将该集合声明为显式地使用id。

```objective-c
// GOOD:

@property(nonatomic, copy) NSArray<id> *unknowns;
```

### 避免抛异常

不要 `@throw` Objective-C 异常，同时也要时刻准备捕获从第三方或 OS 代码中抛出的异常。

以下是在[Apple's Introduction to Exception Programming Topics for Cocoa](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/Exceptions/Exceptions.html)时使用错误对象进行错误传递的建议。

我们的确允许 `-fobjc-exceptions` 编译开关（主要因为我们要用到 `@synchronized`），但我们不使用 `@throw`。为了合理使用第三方的代码，`@try`、`@catch` 和 `@finally` 是允许的。如果你确实使用了异常，请明确注释你期望什么方法抛出异常。

### `nil` 检查

`nil` 检查只用在逻辑流程中。

使用 `nil` 指针来检查应用程序的逻辑流程，而不是在发送消息时避免崩溃。将消息发送给 `nil` 确实返回作为一个指针，一个为0整数或浮点值，为 0 的结构体，`_Complex` 的值等于0 的`nil`。

注意，这适用于 `nil` 作为消息目标，而不是作为参数值。个别方法可能或不能安全地处理 `nil` 参数值。

注意，这和 C/C++ 中检查指针是否为 `NULL` 很不一样，C/C++ 运行时不做任何检查，从而导致应用程序崩溃。因此你仍然需要保证你不会使用一个 `NULL` 指针。

### BOOL 若干陷阱

将普通整形转换成 `BOOL` 时要小心。不要直接将 `BOOL` 值与 `YES` 进行比较。

在OS X和32位的iOS版本中把 `BOOL` 定义成无符号 `char ` ，这意味着 `BOOL` 类型的值远不止 `YES` (1)或 ``NO``(0)。不要直接把整形转换成 `BOOL`。

常见的错误包括将数组的大小、指针值及位运算的结果直接转换成 `BOOL` ，取决于整型结果的最后一个字节，很可能会产生一个 `NO` 值。当转换整形至 `BOOL` 时，使用三目操作符来返回 `YES` 或者 `NO`。

你可以安全地在 `BOOL`、`_Bool` 以及 `bool` 之间转换（参见 C++ Std 4.7.4, 4.12 以及 C99 Std 6.3.1.2）。但 Objective-C 的方法标识符中，只使用 `BOOL`。

对 `BOOL` 使用逻辑运算符（`&&`，`||` 和 `!`）是合法的，返回值也可以安全地转换成 `BOOL`，不需要使用三目操作符。

```objective-c
// AVOID:

- (BOOL)isBold {
  return [self fontTraits] & NSFontBoldTrait;  // AVOID.
}
- (BOOL)isValid {
  return [self stringValue];  // AVOID.
}
```

```objective-c
// GOOD:

- (BOOL)isBold {
  return ([self fontTraits] & NSFontBoldTrait) ? YES : NO;
}
- (BOOL)isValid {
  return [self stringValue] != nil;
}
- (BOOL)isEnabled {
  return [self isValid] && [self isBold];
}
```

同样，不要直接比较 `YES/NO` 和 `BOOL` 变量。在 C 中不仅仅因为影响可读性，更重要的是结果可能与你想的不同。

```objective-c
// AVOID:

BOOL great = [foo isGreat];
if (great == YES) {  // AVOID.
  // ...be great!
}
```

```objective-c
// GOOD:

BOOL great = [foo isGreat];
if (great) {         // GOOD.
  // ...be great!
}
```

### 没有实例变量的接口

没有声明任何实例变量的接口，应省略空花括号。

```objective-c
// GOOD:

@interface MyClass : NSObject
// Does a lot of stuff.
- (void)fooBarBam;
@end
```

```objective-c
// AVOID:

@interface MyClass : NSObject {
}
// Does a lot of stuff.
- (void)fooBarBam;
@end
```

## Cocoa 模式

### 委托模式

在创建循环引用时，不应保留委托、目标对象和块指针。

为了避免引起循环引用，当一个委托或目标指针被清除时，就应该立即释放，这样就不再需要对对象进行消息传递了。

如果没有明确的时间，委托或目标指针不再需要，指针只应该被弱引用。

代码块指针不能被弱引用。为了避免在客户端代码中造成循环引用，代码块指针应该被用于回调，只有在它们被调用或者不再需要它们之后才可以显式地释放它们。否则，回调应该通过弱委托或目标指针来完成。

## Objective-C++

### 匹配语言的风格

在一个 Objective-C++ 源文件中，遵循你正在实现的函数或方法的语言的风格。为了减少在混合使用 Cocoa/Objective-C++和C++时不同命名风格之间的冲突，请遵循所实现的方法的风格。

对于 `@implementation`块中的代码，使用 Objective-C 命名规则。对于 C++ 类方法中的代码，使用C++命名规则。

对于在类实现之外的 Objective-C++ 文件中的代码，在文件中保持一致。

```objective-c
// GOOD:

// file: cross_platform_header.h

class CrossPlatformAPI {
 public:
  ...
  int DoSomethingPlatformSpecific();  // impl on each platform
 private:
  int an_instance_var_;
};

// file: mac_implementation.mm
#include "cross_platform_header.h"

// A typical Objective-C class, using Objective-C naming.
@interface MyDelegate : NSObject {
 @private
  int _instanceVar;
  CrossPlatformAPI* _backEndObject;
}

- (void)respondToSomething:(id)something;

@end

@implementation MyDelegate

- (void)respondToSomething:(id)something {
  // bridge from Cocoa through our C++ backend
  _instanceVar = _backEndObject->DoSomethingPlatformSpecific();
  NSString* tempString = [NSString stringWithFormat:@"%d", _instanceVar];
  NSLog(@"%@", tempString);
}

@end

// The platform-specific implementation of the C++ class, using
// C++ naming.
int CrossPlatformAPI::DoSomethingPlatformSpecific() {
  NSString* temp_string = [NSString stringWithFormat:@"%d", an_instance_var_];
  NSLog(@"%@", temp_string);
  return [temp_string intValue];
}
```

项目可能会选择使用 80 列的长度限制来与Google的C++风格指南保持一致。

## Objective-C 风格异常

### 显示风格异常

没有期望遵循这些样式推荐的代码行，需要在行末尾添加 `// NOLINT` 或前一行的末尾添加 `// NOLINTNEXTLINE`。有时，Objective-C 部分代码必须忽略这些样式的建议(例如，代码可能是机器生成的，或者代码结构是不可能正确的风格)。

某一行的`// NOLINT` 或前面一行 `// NOLINTNEXTLINE` 注释可以用来指示读者，代码是故意忽略样式的指导方针的。此外，这些注释还可以通过诸如 linters 和 handle code 之类的自动化工具来获得。注意，在 `//` 和 `NOLINT*` 之间有一个空格。