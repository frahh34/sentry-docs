# SDK Logs Default Attributes Documentation Update

## Summary

This document summarizes the changes made to update all SDK documentation files that have logging support to indicate what attributes they set by default. The changes were made based on the information from the [Sentry Developer Documentation for Logs](https://develop.sentry.dev/sdk/telemetry/logs/#default-attributes).

## Changes Made

### 1. Created Default Attributes Platform Includes

Created a new directory `platform-includes/logs/default-attributes/` with specific files for each SDK:

- **JavaScript SDK** (`javascript.mdx`):
  - Core attributes: `sentry.environment`, `sentry.release`, `sentry.trace.parent_span_id`, `sentry.sdk.name`, `sentry.sdk.version`
  - Message template attributes: `sentry.message.template`, `sentry.message.parameter.X`
  - User attributes: `user.id`, `user.name`, `user.email`
  - **Browser-specific**: `browser.name`, `browser.version`
  - **Server-specific**: `server.address`

- **Python SDK** (`python.mdx`):
  - Core attributes: Standard SDK attributes
  - Message template attributes: For `{attribute_name}` placeholder syntax
  - User attributes: Standard user attributes
  - **Server-specific**: `server.address`

- **PHP SDK** (`php.mdx`):
  - Core attributes: Standard SDK attributes
  - Message template attributes: For format specifiers like `%s`
  - User attributes: Standard user attributes
  - **Server-specific**: `server.address`

- **Java SDK** (`java.mdx`):
  - Core attributes: Standard SDK attributes
  - Message template attributes: For format specifiers like `%s`
  - User attributes: Standard user attributes
  - **Server-specific**: `server.address`

- **Ruby SDK** (`ruby.mdx`):
  - Core attributes: Standard SDK attributes
  - Message template attributes: For format specifiers like `%s`
  - User attributes: Standard user attributes
  - **Server-specific**: `server.address`

- **Android SDK** (`android.mdx`):
  - Core attributes: Standard SDK attributes with `sentry.java.android` as sdk name
  - Message template attributes: For format specifiers
  - User attributes: Standard user attributes
  - **Mobile-specific**: `os.name`, `os.version`, `device.brand`, `device.model`, `device.family`

- **React Native SDK** (`react-native.mdx`):
  - Core attributes: Standard SDK attributes with `sentry.javascript.react-native` as sdk name
  - Message template attributes: For `logger.fmt` or format strings
  - User attributes: Standard user attributes
  - **Mobile-specific**: `os.name`, `os.version`, `device.brand`, `device.model`, `device.family`

- **Dart SDK** (`dart.mdx`):
  - Core attributes: Standard SDK attributes with `sentry.dart` or `sentry.dart.flutter` as sdk name
  - Message template attributes: For format specifiers
  - User attributes: Standard user attributes
  - **Mobile-specific** (Flutter): `os.name`, `os.version`, `device.brand`, `device.model`, `device.family`

- **Rust SDK** (`rust.mdx`):
  - Core attributes: Standard SDK attributes with `sentry.rust` as sdk name
  - Message template attributes: For format specifiers
  - User attributes: Standard user attributes
  - **Server-specific**: `server.address`

### 2. Updated SDK Documentation Files

Updated the following SDK documentation files to include the new "Default Attributes" section:

#### Files Using Platform Includes:
- `docs/platforms/python/logs/index.mdx`
- `docs/platforms/javascript/common/logs/index.mdx`
- `docs/platforms/php/common/logs/index.mdx`
- `docs/platforms/java/common/logs/index.mdx`
- `docs/platforms/ruby/logs/index.mdx`
- `docs/platforms/android/logs/index.mdx`
- `docs/platforms/react-native/logs/index.mdx`
- `docs/platforms/dart/guides/flutter/logs/index.mdx`

#### Files with Explicit Content:
- `docs/platforms/go/common/logs/index.mdx` - Added detailed default attributes section
- `docs/platforms/rust/common/logs/index.mdx` - Added detailed default attributes section

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

## Implementation Details

1. **Attribute Specificity**: Each SDK only mentions attributes relevant to its platform type. For example:
   - Browser attributes are only mentioned for JavaScript browser SDKs
   - Mobile device attributes are only mentioned for Android, React Native, and Flutter SDKs
   - Server attributes are only mentioned for backend SDKs

2. **Message Template Context**: Each SDK's default attributes documentation explains its specific message templating syntax:
   - JavaScript: `logger.fmt` or format strings
   - Python: `{attribute_name}` placeholder syntax
   - PHP/Java/Ruby: Format specifiers like `%s`
   - Go: Format specifiers like `%v`
   - Rust: Format syntax

3. **SDK Name Specificity**: Each SDK documents its specific `sentry.sdk.name` value:
   - JavaScript: `sentry.javascript.browser`, `sentry.javascript.node`, etc.
   - Python: `sentry.python`
   - PHP: `sentry.php`
   - Java: `sentry.java`
   - Android: `sentry.java.android`
   - React Native: `sentry.javascript.react-native`
   - Dart: `sentry.dart` or `sentry.dart.flutter`
   - Go: `sentry.go`
   - Ruby: `sentry.ruby`
   - Rust: `sentry.rust`

## SDKs Supported

All SDKs listed on the [Logs Getting Started page](https://docs.sentry.io/product/explore/logs/getting-started/) now have default attributes documentation:

### JavaScript (all variants)
- Browser JavaScript, Angular, Astro, AWS Lambda, Azure Functions, Bun, Cloudflare, Connect, Electron, Ember, Express, Fastify, Gatsby, Google Cloud Functions, Hapi, Hono, Koa, Nest.js, Node.js, Next.js, Nuxt, React, React Router, Remix, Solid, SolidStart, Svelte, SvelteKit, TanStack Start, Vue, Wasm

### Java
- Java, Spring, Spring Boot

### Mobile
- Android, Flutter, React Native

### PHP
- PHP, Laravel

### Python
- Python

### Ruby
- Ruby

### Go
- Go

### Rust
- Rust

This ensures that developers using any of these SDKs can now understand exactly what default attributes will be automatically attached to their log entries, helping them make better use of Sentry's structured logging capabilities.