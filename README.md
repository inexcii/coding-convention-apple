# coding-convention-apple

Guide for how to read these conventions effectively:
* The order of each document listed under each programming language matters from Most to Less important. If a rule is duplicated in multiple documents, follow the first one you read.
* The most important parts/sections are listed under each document. You should read and understand them first.

### Objective-C 

1. [Apple Document](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html#//apple_ref/doc/uid/10000146-SW1)
    1. Code Naming Basics
    1. Naming Methods
        1. General Rules
        1. Accessor Methods
        1. Delegate Methods
        1. Method Arguments
    1. Naming Properties and Data Types
        1. Declared Properties and Instance Variables
        1. Constants
    1. Tips and Techniques for Framework Developers
1. [NYTimes](https://github.com/NYTimes/objective-c-style-guide)
    1. Dot Notation Syntax
    1. Spacing
        * **Refer the following example** rather than in the document:
        ```swift
            if (user.isHappy) {
                // Do something
            } else {
                // Do something else
            }
        ```
    1. Conditionals
    1. Methods
    1. Variables
    1. Naming
    1. Comments
    1. init and dealloc
    1. Literals
    1. CGRect Functions
    1. Constants
    1. Enumerated Types
    1. Private Properties
    1. Booleans
    1. Singletons
    1. Imports
    1. Protocols

### Swift

1. [Swift Document](https://swift.org/documentation/api-design-guidelines/)
    1. Fundamentals
    1. Naming
        1. Promote Clear Usage
    1. Conventions
1. [Raywenderlich](https://github.com/raywenderlich/swift-style-guide)
    1. Correctness
    1. Naming
        1. Class Prefixes
        1. Delegates
        1. Use Type Inferred Context
        1. Language
    1. Code Organization
    1. Spacing
        1. **Using 4 spaces** rather than 2 as described in the document.
    1. Comments
    1. Class and Structures
        1. Use of Self
        1. Computed Properties
    1. Closure Expressions
    1. Types
        1. Constants
        1. Optionals
        1. Lazy Initialization
        1. Type Inference
        1. Syntactic Sugar
    1. Memory Management
    1. Access Control
    1. Control Flow
    1. Golden Path
    1. Parentheses
1. [Github](https://github.com/github/swift-style-guide) (optional)

# Code Layout inside a Source Code File

As a general principle, from top to down side in a single scope(e.g. a struct/class) of source code file, the code should be layout as following:
* Properties should be listed upper than functions
* Class extensions should be listed at the lowest position
* Access-control attributes should be listed from highest to lowest access level, as following:
    * `open` → `public` → `internal` → `fileprivate` → `private`
* In-class/struct should be listed at the upper most of the single scope

### Properties

As for properties:
* Inside each level of access-control attribute, constants('let') should be listed upper than variables('var')
* Override properties should be listed at upper most in each access-control level

Syntax/Category |	Description |	Notes
--------------- | ----------- | -----
`open` / `public`	| read and write both outside and inside of module | `open` has the capability of subclassing while `public` has not
`open` / `public` `internal(set)` |	read-only outside module and write-able inside it | (the same as above)
(no attributes needed) | module-wise read and write |	The default 'internal' access level
`fileprivate(set)` / `private(set)`	| module-wise read-only and write-able under source file scope | can be written throughout a source code file
default computed property with getter-only | module-wise read-only | <pre lang="swift">var aProperty: Bool { return true }</pre>
`fileprivate` / `private` |	read and write under source file scope | can only be written in a single scope(inside struct, class etc.)

### Functions

As for functions:

* Each access level(called 'section' in the list below) should be divided by drawing a line as: `// MARK: - `
    * e.g. // MARK: - Initialization
    * If multiple giant classes exists inside a single source file(currently as BGSDownloader.swift), it is better to draw the line for each class and use // MARK: instead for the sections
* Override functions should be listed at upper most in each sections

The code layout of functions should be listed, by sections, as the order of the following list:

Section |	Notes
------- | -----
Initialization | 1. deinit{} is a **MUST** implement and are recommended to be listed on the upper most <br> 2. designated initializers should be listed upper than convenient ones
Open | functions that can be accessed and inherited outside the module, AKA the APIs of the SDK
Public | functions that can be accessed outside the module, AKA the APIs of the SDK
Internal | functions that can be accessed only within the module
Delegate | Generally, delegates are recommended to be implemented in the extention section of a class. <br> If listed, the delegates should be separated by their own names, started by `// MARK:` <br> e.g. // MARK: ArchiveManagerDelegate
Fileprivate | functions that can be accessed only within the same source file
Private	| functions that can be accessed only within a single scope(struct, class etc.) of the source file

### Example

* AssetFilesStorage and AssetFilesLoader class in BGSDownloader.swift
* PlaybackVideo.swift and OfflineVideo.swift
