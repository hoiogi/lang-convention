# NCSOFT Objective-C code style guide

## 배경
- 본 문서는 Objective-C 언어를 사용하여 NCSOFT 서비스를 개발함에 있어서, 개발자들 사이의 코딩 스타일을 일치 시켜 추후 유지 보수 작업에서 보다 나은 가독성을 제공하기 위해서 작성되었음.

- 해당 문서는 아래의 문서에 기반하여 작성 됨.
    - [Apple’s Cocoa Coding Guidelines]
    - [Google Objective-C Style Guide]

## Spacing And Fromatting
### Space vs. Tabs
- 들여쓰기에는 4 space 를 사용한다.
	- Xcode > Preferences > Text Editing > Indentation [Tab] 에서 
		- Tab width를 4 spaces 로 설정.
		- Tab key를 Indents in leading whitespace 로 설정. 

### Line Length
- 각각의 라인의 길이는 최대 120 자를 넘지 않도록 한다. 단, 부득이하게 Block 코딩과 같이 들여쓰가 많이 된 경우는 제외한다.
	- Xcode > Preferences > Text Editing > Editing [Tab] 에서 Page guilde at column 을 120 으로 설정.

### Method Declarations and Definitions
- **-** or **+** 뒤에는 1 space를 준다.
- 파라미터 타입이 포인터인 경우 _(ClassName *)paramName_ 으로 작성.
- **-** or **+** 뒤에오는 문자는 _(ClassName *)paramName_ 제외하고 공백없이 작성한다.

```objc
// YES
- (void)doSomethingWithString:(NSString *)string
{
}

// No
- (void) doSomethingWithString: (NSString *) string
{
}
```

- 메소드 시작 표시( “{“ ) 는 마지막 파라미터 다음 줄에 작성.

```objc
- (void)doSomethingWithString:(NSString *)string
{
}
```

>- 만약, 파라미터 갯수가 많아서 한줄에 120자가 넘어 갈 경우엔 파라미터를 다음 라인으로 넘긴다.

```objc
- (void)doSomethingWithString:(NSString *)string
                         rect:(CGRect)rect
                     interval:(CGFloat)interval
{
}
```

>- 단, 아래와 같이 줄바꿈 후 콜론기준으로 정렬되지 않을 경우는 줄바꿈을 하지 않는다.

```objc
// Yes
- (BOOL)doSomethingWithObject:(NSObject *)obj veryVeryLongLongLongNameParameterName:(NSString *)parameterName otherParameter:(NSObject *)otherParameter
{
}

// No
- (BOOL)doSomethingWithObject:(NSObject *)obj
veryVeryLongLongLongNameParameterName:(NSString *)parameterName
               otherParameter:(NSObject *)otherParameter
{
}
```

### Method Invocations
- 메소드 실행 명령은 120자가 넘지 않을 경우 한 줄에 작성한다

```objc
[myObject doFooWith:arg1 name:arg2 error:arg3];
```

- 120자가 넘어갈 경우

```objc
[myObject doFooWith:arg1
               name:arg2
              error:arg3];
```

- 아래와 같이 사용하지 않도록 한다.

```objc
[myObject doFooWith:arg1 name:arg2  // some lines with >1 arg
              error:arg3];

[myObject doFooWith:arg1
               name:arg2 error:arg3];

[myObject doFooWith:arg1
          name:arg2  // aligning keywords instead of colons
          error:arg3];
```

### @public and @private
- @public, @private 키워드는 4 space 들여 쓰기한다.

```objc
@interface MyClass : NSObject 
{
    @public
         ...
    @private
         ...
}
@end
```

### Contition statement

- if - else 구문은 다른 라인에 작성한다.

```objc
// comment 1
if (isCondition) {
}
// comment 2
else if () {
}
// comment 3
else {
}

// comment
while (YES) {
}

switch (case) {
	CASE1:
    {
        // comment
    }
		break;
	default:
    {
        // comment
	}
		break;
}
```

### Container Literlas
- 한 줄에 120자가 넘어가지 않으면 한 줄로 작성한다.

```objc
NSArray *array = @[[foo description], @"Another String", [bar description]];

NSDictionary *dict = @{ NSForegroundColorAttributeName : [NSColor redColor] };
```

- 만약 여러 줄로 써야 하는 경우 아래와 같이 작성한다.

```objc
NSArray* array = @[
                   @"This",
                   @"is",
                   @"an",
                   @"array"
                  ];

NSDictionary* dictionary = @{
    			             NSFontAttributeName : [NSFont fontWithName:@"Helvetica-Bold" size:12],
    			             NSForegroundColorAttributeName : fontColor
                            };
```

## Naming
### File Names
- .h : C/C++/Objective-C header file
- .m : Objective-C implementation file
- .mm : Objective-C++ implementation file
- .cc : Pure C++ Implementation file
- .c : C Implementation file

### Class Names
- 클래스 이름은 반드시 대문자 두 글자로 시작하는 접두어를 붙이도록 한다.
- ex) NCTester, NCAlert …

### Objective-C Method Names
- method name 은 소문자로 시작하고, 다음 단어부터는 대소문자를 혼용하여 작성.
 - (e.g. convertPoint:fromRect: or replaceCharactersInRange:withString:)
- method name은 자연스럽게 읽을 수 있는 문장이 되도록 작성한다. (참고. Apple’s Guide to Naming Methods)

### Variable Names
- 변수 이름은 소문자로 시작하고, 다음 단어부터는 대소문자를 혼용하여 작성.
 - `(ex: myLocalVariable, _myInstanceVariable)`
- 변수 타입은 이름의 마지막에 붙여준다.
 - `(ex: userIdLabel, _userNickNameLabel)`

>#### Common Variable Names
Do not use Hungarian notation for syntactic attributes, such as the static type of a variable (int or pointer).
Give as descriptive a name as possible, within reason.
Don't worry about saving horizontal space as it is far more important to make your code immediately understandable by a new reader. For example:

```objc
int w;
int nerr;
int nCompConns;
tix = [[NSMutableArray alloc] init];
obj = [someObject object];
p = [network port];

int numErrors;
int numCompletedConnections;
tickets = [[NSMutableArray alloc] init];
userInfo = [someObject object];
port = [network port];
```

##### Instance Variables
- 인스턴스 변수 이름은 underscore 로 시작하고, 이후는 본 문서의 변수 naming 규칙을 따른다. `(ex: _userNameTextField)`

#### Constants
- 상수 (enums, const 변수, etc.) 는 소문자 k 로 시작한다. 이후는 본 문서의 변수 naming 규칙을 따른다.

```objc
const int kNumberOfFiles = 12;
NSString *const kUserKey = @"kUserKey";
NS_ENUM(NSInteger, DisplayTinge) {
    kDisplayTingeGreen = 1,
    kDisplayTingeBlue = 2
};
```

- Because Objective-C does not provide namespacing, constants with global scope should have an appropriate prefix to minimize the chance of name collision, typically like kClassNameFoo.
- **#define** 은 대문자로만 namaing 한다. 단어는 underscore 로 구분한다.
 - (ex: #define FONT_NAME @”fontName”)


## Comment
- 주석 스타일은 appledoc comment 스타일로 작성한다.(xcode5에서 지원)

### Declaration Comments
- 새로운 interface, category, protocol에 설명이 필요한 경우 아래와 같이 주석을 작성한다.

```objc
/*!
 A delegate for NSApplication to handle notifications about app
 launch and shutdown. Owned by the main app controller.
 */
@interface MyAppDelegate : NSObject {
  ...
}
@end
```

### Method Comments

```objc
/*!
 NCSOFT Push Service Provider에 등록에 사용되는 method.

 @note NCSOFT Push Service Provider 등록 후 재 실행시 기존에 등록한 값(_deviceTokenString_)과 동일하면 동작하지 않음.
 @warning if _deviceTokenString_ is nil, throw exception.

 @param deviceTokenString Apple Push Service 로 부터 발급 받은 `NSData` 객체를 16진수로 변환한 `NSString` 객체.
 @param serviceKindCode NCSOFT Push Provider Server에 등록된 해당 앱의 코드. NCSOFT에서 부여 받은 값.
 @param userId 게임에서 사용되는 사용자 ID. 특정 사용자에게 푸쉬메시지를 보낼 때 사용.
 @param success	등록 성공시에 호출되는 block. Return value is void.
 @param failure	등록 실패시에 호출되는 block. NCSOFT Push Service Provider에 등록이 실패하면 `NSError` 객체로 전달됨. Return value is void.
 */
+ (void)addDeviceTokenString:(NSString *)deviceTokenString
	         serviceKindCode:(NSInteger)serviceKindCode
		              userId:(NSString *)userId
		             success:(void (^)(void))success
		             failure:(void (^)(NSError *))failure;
```


[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)

[Apple’s Cocoa Coding Guidelines]: <https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html>
[Google Objective-C Style Guide]: <https://google.github.io/styleguide/objcguide.xml>
