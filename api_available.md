## API 版本控制

```
#ifndef __OS_AVAILABILITY__
#define __OS_AVAILABILITY__

#include <AvailabilityInternal.h>

/*
 Macros for defining which versions/platform a given symbol can be used.
 
 @see http://clang.llvm.org/docs/AttributeReference.html#availability

 * Note that these macros are only compatible with clang compilers that
 * support the following target selection options:
 *
 * -mmacosx-version-min
 * -miphoneos-version-min
 * -mwatchos-version-min
 * -mtvos-version-min
 * -mbridgeos-version-min
 */

#if defined(__has_feature) && defined(__has_attribute)
 #if __has_attribute(availability)

    /*
     * API Introductions
     *
     * Use to specify the release that a particular API became available.
     *
     * Platform names:
     *   macos, ios, tvos, watchos
     *
     * Examples:
     *    API_AVAILABLE(macos(10.10))
     *    API_AVAILABLE(macos(10.9), ios(10.0))
     *    API_AVAILABLE(macos(10.4), ios(8.0), watchos(2.0), tvos(10.0))
     */

    #define API_AVAILABLE(...) __API_AVAILABLE_GET_MACRO(__VA_ARGS__,__API_AVAILABLE5, __API_AVAILABLE4, __API_AVAILABLE3, __API_AVAILABLE2, __API_AVAILABLE1)(__VA_ARGS__)

    /*
     * API Deprecations
     *
     * Use to specify the release that a particular API became unavailable.
     *
     * Platform names:
     *   macos, ios, tvos, watchos
     *
     * Examples:
     *
     *    API_DEPRECATED("No longer supported", macos(10.4, 10.8))
     *    API_DEPRECATED("No longer supported", macos(10.4, 10.8), ios(2.0, 3.0), watchos(2.0, 3.0), tvos(9.0, 10.0))
     *
     *    API_DEPRECATED_WITH_REPLACEMENT("-setName:", tvos(10.0, 10.4), ios(9.0, 10.0))
     *    API_DEPRECATED_WITH_REPLACEMENT("SomeClassName", macos(10.4, 10.6), watchos(2.0, 3.0))
     */

    #define API_DEPRECATED(...) __API_DEPRECATED_MSG_GET_MACRO(__VA_ARGS__,__API_DEPRECATED_MSG6,__API_DEPRECATED_MSG5,__API_DEPRECATED_MSG4,__API_DEPRECATED_MSG3,__API_DEPRECATED_MSG2,__API_DEPRECATED_MSG1)(__VA_ARGS__)
    #define API_DEPRECATED_WITH_REPLACEMENT(...) __API_DEPRECATED_REP_GET_MACRO(__VA_ARGS__,__API_DEPRECATED_REP6,__API_DEPRECATED_REP5,__API_DEPRECATED_REP4,__API_DEPRECATED_REP3,__API_DEPRECATED_REP2,__API_DEPRECATED_REP1)(__VA_ARGS__)


    /*
     * API Unavailability
     * Use to specify that an API is unavailable for a particular platform.
     *
     * Example:
     *    API_UNAVAILABLE(macos)
     *    API_UNAVAILABLE(watchos, tvos)
     */

    #define API_UNAVAILABLE(...) __API_UNAVAILABLE_GET_MACRO(__VA_ARGS__,__API_UNAVAILABLE4,__API_UNAVAILABLE3,__API_UNAVAILABLE2,__API_UNAVAILABLE1)(__VA_ARGS__)
 #else

    /* 
     * Evaluate to nothing for compilers that don't support availability.
     */
   
     #define API_AVAILABLE(...)
     #define API_DEPRECATED(...)
     #define API_DEPRECATED_WITH_REPLACEMENT(...)
     #define API_UNAVAILABLE(...)
 #endif /* __has_attribute(availability) */
#else

    /* 
     * Evaluate to nothing for compilers that don't support clang language extensions.
     */
    
    #define __API_AVAILABLE(...)
    #define __API_DEPRECATED(...)
    #define __API_DEPRECATED_WITH_REPLACEMENT(...)
    #define __API_UNAVAILABLE(...)
#endif /* #if defined(__has_feature) && defined(__has_attribute) */

#endif /* __OS_AVAILABILITY__ */

```


