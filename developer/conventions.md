## Conventions

\section conventions_code_cpp C++

\subsection conventions_code_cpp_general C++ General
* *File naming*
  * *Header files* - Must end with *hpp* extension.
  * *Implementation files* - Must end with *cpp* extension.
* *Scope indentation* - 4 spaces, no tabs.
* *Namespaces*
  * *In header file* - Use something like: *namespace Finjin { namespace Engine { ... } }*
  * *In implementation file* - Use something like: *using namespace Finjin::Engine;*
* *this* - In an instance method, member variable accesses must be qualified with *this*. For example: *this->value = 0;*
* *Brace placement* - { and } braces are on their own line.
* *switch statement 'case' braces* - If the logic can fit neatly on a single line, no braces are necessary. Otherwise, braces are always used.
* *using vs typedef* - Use 'using' by default. The only time 'typedef' should be used is in code that needs to be compatible with the Finjin exporters (which use older compilers). See <a href="#conventions_code_cpp_old_code">Old Code</a> for more information.
* *size_t vs uint64_t* - When expressing counts/lengths and indexes/offsets that fit into system memory, use size_t. When expressing an unknown or potentially very large value, such as a streaming byte count or a file length, use uint64_t (to avoid 32-bit/64-bit issues associated with size_t). In either case, use (size_t)-1 or (uint64_t)-1, respectively, to indicate an invalid value.
* *Type casting* - Prefer C++ style static_cast and reinterpret_cast, rarely use dynamic_cast, and never use const_cast unless interfacing with external code that (improperly) requires it. In some cases the C style is acceptable, such as when casting a literal value (such as (size_t)-1), or in very rare cases performing an unusual cast in a template function.
* *Maximum line length* - There's no hard limit on how long a line can be. Use common sense when determining how much code to place onto a line. See <a href="#conventions_code_general_breaking_line">Breaking Up Long Lines</a> for tips on breaking up long lines.
* *Single include guard* - Use '#pragma once' at the top of the file.

\subsection conventions_code_cpp_naming C++ Naming

| Element                   | Style                                                  | Example                                                                                                                      | Notes                                                                                           |
| :-----------------------: | :----------------------------------------------------: | :--------------------------------------------------------------------------------------------------------------------------: | :---------------------------------------------------------------------------------------------: |
| Header file               | Upper camel case                                       | SomeFile.hpp                                                                                                                 | The file name will often correspond to a class contained within the file.                       |
| Implementation file       | Upper camel case                                       | SomeFile.cpp                                                                                                                 | The file name should match the corresponding header file name.                                  |
| Variable                  | Lower camel case                                       | int someVariable;                                                                                                            | Avoid abbreviations.                                                                            |
| Function/method           | Upper camel case                                       | void DoSomething();                                                                                                          | Avoid abbreviations.                                                                            |
| Class                     | Upper camel case                                       | class SomeClass                                                                                                              |                                                                                                 |
| Macro                     | Upper case                                             | #define FINJIN_SOME_MACRO 1                                                                                                  | In header file, use FINJIN prefix. In implementation file no prefix is needed.                  |
| Enum                      | Upper camel case name, upper case values               | enum class SomeEnum { FIRST_VALUE, SECOND_VALUE };                                                                           |                                                                                                 |
| Enum flags                | Same as regular enum, often with 'Flag' name suffix    | enum class SomeFlag { NONE = 0, ONE = 1 << 0, TWO = 1 << 1 }; FINJIN_ENUM_BITWISE_OPERATIONS(SomeFlag)                       | To use FINJIN_ENUM_BITWISE_OPERATIONS: #include "finjin/common/EnumBitwise.hpp"                 |
| Configuration keys/values | Lower case                                             | background-color=dark-red                                                                                                    | These appear in configuration files and asset files. Use '-' (not '_') to separate words.       |


\subsection conventions_code_cpp_collections_containers C++ Collections / Containers

The Finjin classes should generally be used in favor of the STL classes, due to stricter behavior on memory usage.
| STL                                            | Finjin Equivalent                                                                                                               |
| :--------------------------------------------: | :-----------------------------------------------------------------------------------------------------------------------------: |
| std::vector                                    | Finjin::Common::DynamicVector or Finjin::Common::StaticVector                                                                   |
| std::vector<uint8_t>                           | Finjin::Common::DynamicVector<uint8_t>, Finjin::Common::StaticVector<uint8_t>, or Finjin::Common::ByteBuffer                    |
| std::array                                     | None. Acceptable to use.                                                                                                        |
| std::array<SomeType, (size_t)SomeEnum::COUNT>  | Finjin::Common::EnumArray<SomeEnum, SomeEnum::COUNT, SomeType>. To use EnumArray: #include "finjin/common/EnumArray.hpp"     |
| std::list                                      | None. If a list is really needed, use an std::vector equivalent and make a intrusive list (some type of member 'next' pointer). |
| std::unordered_map                             | Finjin::Common::DynamicUnorderedMap or Finjin::Common::StaticUnorderedMap                                                       |
| std::queue                                     | Finjin::Common::DynamicQueue or Finjin::Common::StaticQueue                                                                     |
| std::string                                    | Finjin::Common::Utf8String                                                                                                      |
| std::bitset                                    | Acceptable to use. Also Finjin::Common::BitArray                                                                                |
| std::optional                                  | Finjin::Common::Setting                                                                                                         |
| Anything not listed here                       | Do not use.                                                                                                                     |


\subsection conventions_code_cpp_example C++ Example

Header File (ApplicationError.hpp)
```
#pragma once


//Types------------------------------------------------------------------------
namespace Finjin { namespace Engine {

    enum class ApplicationErrorCode
    {
        NONE,
        OUT_OF_MEMORY
    };
    
    class ApplicationError
    {
    public:
        ApplicationError();
        ApplicationError(ApplicationErrorCode code);
        
        const char* GetString() const;
    
    private:
        ApplicationErrorCode code;
    };
    
} }
```

Implementation File (ApplicationError.cpp)
```
//Includes---------------------------------------------------------------------
#include "ApplicationError.hpp"

using namespace Finjin::Engine;


//Macros-----------------------------------------------------------------------
#define DEFAULT_CODE ApplicationErrorCode::NONE


//Implementation---------------------------------------------------------------
ApplicationError::ApplicationError()
{
    this->code = DEFAULT_CODE;
}

ApplicationError::ApplicationError(ApplicationErrorCode code)
{
    this->code = code;
}

const char* ApplicationError::GetString() const
{
    switch (this->code)
    {
        case ApplicationErrorCode::NONE: return "<none>";
        case ApplicationErrorCode::OUT_OF_MEMORY: return "Out of memory";
        default:
        {
            assert(0 && "Invalid enum.");
            return "<invalid>";
        }
    }
}
```

\subsection conventions_code_cpp_old_code C++ Old Code
Most of the code associated with Finjin, such as finjin-common and finjin-engine, is considered 'new' code.

However, finjin-exporter is considered 'old' code due to the fact that:
1. Much of it pre-dates finjin-common and finjin-engine.
2. The code must remain compatible with older compilers to accomodate the requirements of the 3DS Max and Maya SDKs.

Because of this, 'old' code breaks with the style guidelines and should not be used as a reference when writing 'new' code.


\section conventions_code_objcpp Objective C++

The only Objective C++ code that exists in Finjin is located within the Apple (macOS, iOS, tvOS) implementation in finjin-engine. Additionally, the Apple versions of user-generated projects have some Objective C++ skeleton code.

Objective C++ conventions inherit most of the standard C++ conventions, in addition to those listed below.

\subsection conventions_code_objcpp_general Objective C++ General
* *File naming*
  * *Header files* - If the file contains predominantly C++ code, it must end with *hpp* extension. Otherwise, it must end with *h* extension.
  * *Implementation files* - Must end with *mm* extension.
* *self* - In an instance method, member getter/setter property accesses must be qualified with *self*. For example: *self.someProperty = 0;*
* *Member variable naming* - Must be prefixed with '_'. For example: *int _value;*
* *Including an Objective C++ header file* - Use '#import'. For example: #import "SomeFile.h"
* *Single include guard* - None. Using '#import' eliminates the need for this.


\section conventions_code_java Java

The only Java code that exists in Finjin is located within the Android implementation in finjin-engine.

\subsection conventions_code_java_general Java General
* *File naming* - The file is named for the only public class within the file.
* *Scope indentation* - 4 spaces, no tabs.
* *Packages* - Use something like: *com.finjin.engine*
* *this* - In an instance method, member variable accesses must be qualified with *this*. For example: *this.value = 0;*
* *Brace placement* - { and } braces are on their own line. Yes, this differs from normal Java conventions.
* *switch statement 'case' braces* - If the logic can fit neatly on a single line, no braces are necessary. Otherwise, braces are always used.
* *Maximum line length* - There's no hard limit on how long a line can be. Use common sense when determining how much code to place onto a line. See <a href="#conventions_code_general_breaking_line">Breaking Up Long Lines</a> for tips on breaking up long lines.
* *Annotations* - Annotations such as *Override* should be on their own line.
* *Modifiers* - Modifiers should appear in the following order: *public protected private abstract default static final transient volatile synchronized native strictfp*
* For anything not mentioned here, the Java conventions in the [Google Java Style Guide (External link)](https://google.github.io/styleguide/javaguide.html) are acceptable.

\subsection conventions_code_java_naming Java Naming

| Element                   | Style                  | Example                                        | Notes                                                                                           |
| :-----------------------: | :--------------------: | :--------------------------------------------: | :---------------------------------------------------------------------------------------------: |
| Class                     | Upper camel case       | class SomeClass                                |                                                                                                 |
| Class file                | Upper camel case       | SomeClass.java                                 | The file name corresponds to the public class contained within the file.                        |
| Variable                  | Lower camel case       | private int someVariable;                      | Avoid abbreviations.                                                                            |
| Method                    | Lower camel case       | public void doSomething();                     | Avoid abbreviations.                                                                            |
| Final values              | Upper case             | public static final int MAX_COUNT = 1;         |                                                                                                 |

\subsection conventions_code_java_example Java Example

Class File (SomeNativeActivity.java)
```
package com.finjin.engine;

import android.app.NativeActivity;

public class SomeNativeActivity extends NativeActivity 
{
    @Override
    public void onCreate(Bundle savedInstanceState) 
    {
        getKeyCodeStrings();
        
        super.onCreate(savedInstanceState);
    }
    
    private void getKeyCodeStrings()
    {
        for (int i = 0; i < MAX_KEY_CODES; i++)
        {
            try
            {
                String asString = KeyEvent.keyCodeToString(i);
                this.keyCodeStrings[this.keyCodeStringCount++] = asString;
            }
            catch (Exception ex)
            {
                //Unsupported key code
            }
        }
    }
    
    private static final int MAX_KEY_CODES = 300;
    private String[] keyCodeStrings = new String[MAX_KEY_CODES];
    private int keyCodeStringCount = 0;
}
```


\section conventions_code_general General

\subsection conventions_code_general_breaking_line General Breaking Up Long Lines

Breaking Long Function Declaration or Call
```
SomeFunction
    (
    firstValue,
    secondValue,
    thirdValue,
    fourthValue,
    fifthValue,
    sixthValue
    );
```

Breaking Long Series of Tests
```
bool SomeChecks(int value)
{
    return
        value == 111 ||
        value > 222 ||
        TestSomeValue(value) ||
        (IsOdd(444) && !IsEven(555)) ||
        IsBetween(value, 666, 777)
        ;
}
```

Breaking Long Constructor
```
SomeClass::SomeClass(int a, int b, int c, int d, int e) :
    BaseClass(a),
	aMember(a),
	bMember(b),
	cMember(c),
	dMember(d),
	eMember(e)
{
}
```
