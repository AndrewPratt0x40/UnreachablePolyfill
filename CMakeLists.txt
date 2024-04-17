cmake_minimum_required(VERSION 3.27)

project(UnreachablePolyfill
	VERSION 1.0.0
	DESCRIPTION "A polyfill for C++23's std::unreachable()"
	HOMEPAGE_URL "https://github.com/AndrewPratt0x40/UnreachablePolyfill"
	LANGUAGES CXX
)


# Options
option(
	UNREACHABLE_POLYFILL_GLOBAL_NAMESPACE
	"Generates the polyfill for std::unreachable() in global scope."
	OFF
)
set(
	UNREACHABLE_POLYFILL_NAMESPACE
	"Unreachable_polyfill"
	CACHE
	STRING
	"The qualified namespace to generate the polyfill for std::unreachable() in. Shouldn't contain a leading scope resolution operator (ex. use Foo::Bar, not ::Foo::Bar). Ignored if UNREACHABLE_POLYFILL_GLOBAL_NAMESPACE is enabled."
)


add_library(UnreachablePolyfill INTERFACE
	"unreachable_polyfill.h"
)


if(UNREACHABLE_POLYFILL_GLOBAL_NAMESPACE)
	target_compile_definitions(unreachable_polyfill PUBLIC "UNREACHABLE_POLYFILL_GLOBAL_NAMESPACE")
endif()


# Generate unreachable_polyfill.h in the project's binary directory
configure_file(unreachable_polyfill.h.in unreachable_polyfill.h)


target_include_directories(UnreachablePolyfill
	INTERFACE "${PROJECT_BINARY_DIR}"
)