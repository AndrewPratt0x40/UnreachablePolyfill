# UnreachablePolyfill
This small library provides C++23's `std::unreachable()` in earlier versions of C++.
The implementation is taken from [cppreference.com](https://cppreference.com/) under the [CC BY-SA 3.0 DEED](https://creativecommons.org/licenses/by-sa/3.0/) license.
The copied implementation can be found [here](https://en.cppreference.com/w/cpp/utility/unreachable).
# Installation
## Manual
Simply copy unreachable_polyfill.h into your project's source directory and #include it as you normally would.
If the symbol `UNREACHABLE_POLYFILL_GLOBAL_NAMESPACE` is defined, then `unreachable()` will be declared globally. Otherwise, it will be defined in the namespace `::Unreachable_polyfill`.
## CMake
This project can be included with CMake via FetchContent.
Below is an example CMakeLists.txt:
```
cmake_minimum_required(VERSION 3.27)

project(Foo)

include(FetchContent)
FetchContent_Declare(
	UnreachablePolyfill
	GIT_REPOSITORY https://github.com/AndrewPratt0x40/UnreachablePolyfill.git
	GIT_TAG <Enter the SHA tag for the latest commit here>
)
FetchContent_MakeAvailable(UnreachablePolyfill)

add_executable(Foo main.cpp)

target_link_libraries(Foo PUBLIC UnreachablePolyfill::UnreachablePolyfill)
```
When using CMake, the following cache variables are available:

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| UNREACHABLE_POLYFILL_GLOBAL_NAMESPACE | Boolean | OFF | True if `unreachable()` should be defined globally. False if `unreachable()` should be defined in the namespace named by cache variable UNREACHABLE_POLYFILL_NAMESPACE. |
| UNREACHABLE_POLYFILL_NAMESPACE | String | "Unreachable_polyfill" | The namespace to define `unreachable()` in. |

If the symbol `UNREACHABLE_POLYFILL_GLOBAL_NAMESPACE` is defined, then `unreachable()` will be declared globally. Otherwise, it will be defined in the namespace named by cache variable UNREACHABLE_POLYFILL_NAMESPACE.
