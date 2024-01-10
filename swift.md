# Swift Knowledge Database

## Variables

```swift
private var x: Bool = false; 

let y: String = "Hello World";
```

## States

```swift
@State private var showModal = false;

print(showModal) // -> false
print($showModal) // -> false (as Binding)
print(_showModal) // -> false (to initialize Value) Does not re-render when changed
```

## Bindings

Bindings in Swift allow a child function or a child view to read and modify a variable defined in a parent view. By using a binding, changes made to the variable in the child view are reflected in the parent view.

### Declaration
To indicate that a structure or class needs a binding to a variable, the `@Binding` property wrapper declaration is used. For example:

```swift
@Binding var isShown: Bool
```

This declaration means that isShown is a binding to a Bool variable.

### Usage
A binding is typically passed from a parent view to a child view. In the parent view, a `@State` variable is used to manage the state:

```swift
@State private var isShown: Bool = false
```

Then, a binding to this `State` variable is passed to the child view:

```swift
ChildView(isShown: $isShown)
```

Here, `$isShown` is a binding to the `@State` variable `isShown`.

### Important to Note
* A `@Binding` can only be bound to a `@State` variable or another source of truth (like `@ObservedObject` or `@EnvironmentObject`).
* If a variable is declared as a `@Binding`, it expects a binding as input. Passing a regular value directly (without the `$` prefix) will result in a compilation error.


## Structs
* Leightweight
* Performant
* Value Type

## Classes
* Inheritance
* Reference Type

## Visibility

- public
- internal
- fileprivate
- private

