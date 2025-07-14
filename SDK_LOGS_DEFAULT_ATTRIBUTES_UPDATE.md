# SDK Logs Default Attributes Documentation Update

## Summary

This document summarizes the changes made to update all SDK documentation files that have logging support to indicate what attributes they set by default. The changes were made based on the information from the [Sentry Developer Documentation for Logs](https://develop.sentry.dev/sdk/telemetry/logs/#default-attributes).

## Changes Made

### 1. Created Modular Default Attributes Platform Includes

Created a new modular structure in `platform-includes/logs/default-attributes/` with separate files for different types of attributes:

#### Core Shared Attributes
- **`core.mdx`**: Core attributes common to all SDKs
  - `sentry.environment`, `sentry.release`, `sentry.trace.parent_span_id`, `sentry.sdk.name`, `sentry.sdk.version`

- **`user.mdx`**: User attributes common to all SDKs
  - `user.id`, `user.name`, `user.email`

- **`browser.mdx`**: Browser-specific attributes
  - `browser.name`, `browser.version`

- **`server.mdx`**: Server-specific attributes
  - `server.address`

- **`mobile.mdx`**: Mobile device-specific attributes
  - `os.name`, `os.version`, `device.brand`, `device.model`, `device.family`

#### Message Template Attributes (SDK-specific)
- **`message-template/javascript.mdx`**: For `logger.fmt` or format strings
- **`message-template/python.mdx`**: For `{attribute_name}` placeholder syntax
- **`message-template/php.mdx`**: For format specifiers like `%s`
- **`message-template/java.mdx`**: For format specifiers like `%s`
- **`message-template/ruby.mdx`**: For format specifiers like `%s`
- **`message-template/android.mdx`**: For format specifiers
- **`message-template/dart.mdx`**: For format specifiers
- **`message-template/rust.mdx`**: For format specifiers
- **`message-template/go.mdx`**: For format specifiers like `%v`

#### SDK-Specific Composition Files
Each SDK has its own composition file that includes the relevant modular components:

- **`javascript.mdx`**: Includes core + javascript message template + user + browser + server
- **`python.mdx`**: Includes core + python message template + user + server
- **`php.mdx`**: Includes core + php message template + user + server
- **`java.mdx`**: Includes core + java message template + user + server
- **`ruby.mdx`**: Includes core + ruby message template + user + server
- **`android.mdx`**: Includes core + android message template + user + mobile
- **`react-native.mdx`**: Includes core + javascript message template + user + mobile
- **`dart.mdx`**: Includes core + dart message template + user + mobile
- **`rust.mdx`**: Includes core + rust message template + user + server

### 2. Updated SDK Documentation Files

Updated all SDK documentation files to include the new "Default Attributes" section:

#### Files Using Platform Includes:
- `docs/platforms/python/logs/index.mdx`
- `docs/platforms/javascript/common/logs/index.mdx`
- `docs/platforms/php/common/logs/index.mdx`
- `docs/platforms/java/common/logs/index.mdx`
- `docs/platforms/ruby/logs/index.mdx`
- `docs/platforms/android/logs/index.mdx`
- `docs/platforms/react-native/logs/index.mdx`
- `docs/platforms/dart/guides/flutter/logs/index.mdx`

#### Files Updated to Use Modular Includes:
- `docs/platforms/go/common/logs/index.mdx` - Updated to use modular includes
- `docs/platforms/rust/common/logs/index.mdx` - Updated to use modular includes

## Benefits of Modular Structure

### 1. **Maintainability**
- Each type of attribute is defined in one place
- Changes to core attributes affect all SDKs automatically
- No duplication of common content

### 2. **Consistency**
- All SDKs use the same definitions for shared attributes
- Consistent formatting and explanations across all platforms

### 3. **Flexibility**
- Easy to add new attribute types
- Simple to customize message template explanations per SDK
- Easy to compose different attribute sets for different SDK types

### 4. **Reusability**
- Common attributes can be reused across multiple SDKs
- Easy to add new SDKs by composing existing modules

## Default Attributes by SDK Type

### Core Attributes (All SDKs)
- `sentry.environment`: Environment set in SDK if defined
- `sentry.release`: Release set in SDK if defined
- `sentry.trace.parent_span_id`: Span ID of active span (only if there was an active span)
- `sentry.sdk.name`: Name of the SDK that sent the log
- `sentry.sdk.version`: Version of the SDK that sent the log

### Message Template Attributes (All SDKs)
- `sentry.message.template`: The parameterized template string
- `sentry.message.parameter.X`: Parameters to the template string

### User Attributes (All SDKs)
- `user.id`: User ID
- `user.name`: Username
- `user.email`: Email address

### Backend SDKs (Node.js, Python, PHP, Ruby, Go, Java, etc.)
- `server.address`: Address of the server that sent the log

### Browser SDKs (JavaScript in browser)
- `browser.name`: Display name of the browser application
- `browser.version`: Version string of the browser

### Mobile SDKs (Android, iOS, React Native, Flutter)
- `os.name`: Name of the operating system
- `os.version`: Version of the operating system
- `device.brand`: Brand of the device
- `device.model`: Model of the device
- `device.family`: Family of the device

## File Structure

```
platform-includes/logs/default-attributes/
├── core.mdx                    # Core attributes (all SDKs)
├── user.mdx                    # User attributes (all SDKs)
├── browser.mdx                 # Browser attributes (browser SDKs)
├── server.mdx                  # Server attributes (backend SDKs)
├── mobile.mdx                  # Mobile attributes (mobile SDKs)
├── message-template/           # Message template attributes (SDK-specific)
│   ├── javascript.mdx          # logger.fmt syntax
│   ├── python.mdx              # {attribute_name} syntax
│   ├── php.mdx                 # %s format specifiers
│   ├── java.mdx                # %s format specifiers
│   ├── ruby.mdx                # %s format specifiers
│   ├── android.mdx             # format specifiers
│   ├── dart.mdx                # format specifiers
│   ├── rust.mdx                # format specifiers
│   └── go.mdx                  # %v format specifiers
├── javascript.mdx              # Composition for JavaScript SDK
├── python.mdx                  # Composition for Python SDK
├── php.mdx                     # Composition for PHP SDK
├── java.mdx                    # Composition for Java SDK
├── ruby.mdx                    # Composition for Ruby SDK
├── android.mdx                 # Composition for Android SDK
├── react-native.mdx            # Composition for React Native SDK
├── dart.mdx                    # Composition for Dart SDK
└── rust.mdx                    # Composition for Rust SDK
```

## Implementation Details

1. **Modular Design**: Each attribute type is defined once and reused across relevant SDKs
2. **Attribute Specificity**: Each SDK only includes attributes relevant to its platform type
3. **Message Template Context**: Each SDK has its own message template explanation for its specific syntax
4. **Consistent Formatting**: All shared attributes use the same formatting and descriptions

## SDKs Supported

All SDKs listed on the [Logs Getting Started page](https://docs.sentry.io/product/explore/logs/getting-started/) now have modular default attributes documentation that provides consistent, maintainable information about what attributes will be automatically attached to their log entries.

This modular approach makes it easy to maintain consistency across all SDK documentation while allowing for platform-specific customizations where needed.