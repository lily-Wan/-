

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

Mac软件中的一个例外是标记为`@IBOutlets`,的实例变量，这些变量被假定为不被保留。

