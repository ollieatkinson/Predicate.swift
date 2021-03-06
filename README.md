# Predicate

[![Swift 5.2](https://img.shields.io/badge/swift-5.2-ED523F.svg?style=flat)](https://swift.org/download/) 
[![SPM](https://img.shields.io/badge/swift-SPM-ED523F.svg?style=flat)](https://swift.org/package-manager/)
![SPM](https://img.shields.io/badge/os-linux-lightgrey.svg?style=flat)
![macOS](https://img.shields.io/badge/os-macOS-lightgrey.svg?style=flat)
[![Licence](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat)](LICENCE)

Predicate Composition

## API

### Equals
```swift
public func == <Root, Value>(block: @escaping (Root) -> Value, value: Value) -> (Root) -> Bool where Value : Equatable
public func != <Root, Value>(block: @escaping (Root) -> Value, value: Value) -> (Root) -> Bool where Value : Equatable
```

#### Example
```swift
users.filter(\.name == "Milos")
users.filter(\.name != "Ste")
```

### Less Than & More Than
```swift
public func < <Root, Value>(block: @escaping (Root) -> Value, value: Value) -> (Root) -> Bool where Value : Comparable
public func > <Root, Value>(block: @escaping (Root) -> Value, value: Value) -> (Root) -> Bool where Value : Comparable
public func <= <Root, Value>(block: @escaping (Root) -> Value, value: Value) -> (Root) -> Bool where Value : Comparable
public func >= <Root, Value>(block: @escaping (Root) -> Value, value: Value) -> (Root) -> Bool where Value : Comparable
```

#### Example
```swift
users.filter(\.age > 25)
users.filter(\.age <= 55)
```

### Similar to

```swift
public func << <Root, S>(block: @escaping (Root) -> S.Element, value: S) -> (Root) -> Bool where S : Sequence, S.Element : Equatable
public func ~= <Root>(block: @escaping (Root) -> String, regex: Regex) -> (Root) -> Bool
public func == <Root, Value>(block: @escaping (Root) -> Value, value: (Value, Value)) -> (Root) -> Bool where Value : FloatingPoint
public func ± <Value>(number: Value, accuracy: Value) -> (Value, Value) where Value : FloatingPoint
```

#### Example

- `<<` sequence contains
- `±` comparing floating point numbers to a degree of accuracy
- `~=` Regex

```swift
users.filter(\.age << 30...35)
users.filter(\.age << [ 30, 32, 34 ])
users.filter(\.weight == 85 ± 4
users.filter(\.name ~= "o(s|ah)$")
```

### Boolean Logic

```swift
public prefix func ! <Root>(block: @escaping (Root) -> Bool) -> (Root) -> Bool
public func && <Root>(lhs: @autoclosure @escaping () -> Bool, rhs: @escaping (Root) -> Bool) -> (Root) -> Bool
public func || <Root>(lhs: @autoclosure @escaping () -> Bool, rhs: @escaping (Root) -> Bool) -> (Root) -> Bool
public func && <Root>(lhs: @escaping (Root) -> Bool, rhs: @autoclosure @escaping () -> Bool) -> (Root) -> Bool
public func || <Root>(lhs: @escaping (Root) -> Bool, rhs: @autoclosure @escaping () -> Bool) -> (Root) -> Bool
public func && <Root>(lhs: @escaping (Root) -> Bool, rhs: @escaping (Root) -> Bool) -> (Root) -> Bool
public func || <Root>(lhs: @escaping (Root) -> Bool, rhs: @escaping (Root) -> Bool) -> (Root) -> Bool
```

#### Example

```swift
users.filter(\.isClearToFly && \.name == "Noah")
users.filter(\.age > 30 && \.name != "Noah")
```

# Installation

## SwiftPM:

```swift
package.append(.package(url: "https://github.com/ollieatkinson/Predicate", from: "1.0.0"))
```
