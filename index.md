# C# coding guidelines <!-- omit in toc -->

Single page version of <https://csharpcodingguidelines.com/> .

- [Class Design Guidelines](#class-design-guidelines)
  - [AV1000: A class or interface should have a single purpose](#av1000-a-class-or-interface-should-have-a-single-purpose)
  - [AV1001: Only create a constructor that returns a useful object](#av1001-only-create-a-constructor-that-returns-a-useful-object)
  - [AV1003: An interface should be small and focused](#av1003-an-interface-should-be-small-and-focused)
  - [AV1004: Use an interface rather than a base class to support multiple implementations](#av1004-use-an-interface-rather-than-a-base-class-to-support-multiple-implementations)
  - [AV1005: Use an interface to decouple classes from each other](#av1005-use-an-interface-to-decouple-classes-from-each-other)
  - [AV1008: Avoid static classes](#av1008-avoid-static-classes)
  - [AV1010: Don't suppress compiler warnings using the `new` keyword](#av1010-dont-suppress-compiler-warnings-using-the-new-keyword)
  - [AV1011: It should be possible to treat a derived type as if it were a base type](#av1011-it-should-be-possible-to-treat-a-derived-type-as-if-it-were-a-base-type)
  - [AV1013: Don't refer to derived classes from the base class](#av1013-dont-refer-to-derived-classes-from-the-base-class)
  - [AV1014: Avoid exposing the other objects an object depends on](#av1014-avoid-exposing-the-other-objects-an-object-depends-on)
  - [AV1020: Avoid bidirectional dependencies](#av1020-avoid-bidirectional-dependencies)
  - [AV1025: Classes should have state and behavior](#av1025-classes-should-have-state-and-behavior)
  - [AV1026: Classes should protect the consistency of their internal state](#av1026-classes-should-protect-the-consistency-of-their-internal-state)
- [Member Design Guidelines](#member-design-guidelines)
  - [AV1100: Allow properties to be set in any order](#av1100-allow-properties-to-be-set-in-any-order)
  - [AV1105: Use a method instead of a property](#av1105-use-a-method-instead-of-a-property)
  - [AV1110: Don't use mutually exclusive properties](#av1110-dont-use-mutually-exclusive-properties)
  - [AV1115: A property, method or local function should do only one thing](#av1115-a-property-method-or-local-function-should-do-only-one-thing)
  - [AV1125: Don't expose stateful objects through static members](#av1125-dont-expose-stateful-objects-through-static-members)
  - [AV1130: Return interfaces to unchangeable collections](#av1130-return-interfaces-to-unchangeable-collections)
  - [AV1135: Properties, arguments and return values representing strings, collections or tasks should never be `null`](#av1135-properties-arguments-and-return-values-representing-strings-collections-or-tasks-should-never-be-null)
  - [AV1137: Define parameters as specific as possible](#av1137-define-parameters-as-specific-as-possible)
  - [AV1140: Consider using domain-specific value types rather than primitives](#av1140-consider-using-domain-specific-value-types-rather-than-primitives)
- [Miscellaneous Design Guidelines](#miscellaneous-design-guidelines)
  - [AV1200: Throw exceptions rather than returning some kind of status value](#av1200-throw-exceptions-rather-than-returning-some-kind-of-status-value)
  - [AV1202: Provide a rich and meaningful exception message text](#av1202-provide-a-rich-and-meaningful-exception-message-text)
  - [AV1205: Throw the most specific exception that is appropriate](#av1205-throw-the-most-specific-exception-that-is-appropriate)
  - [AV1210: Don't swallow errors by catching generic exceptions](#av1210-dont-swallow-errors-by-catching-generic-exceptions)
  - [AV1215: Properly handle exceptions in asynchronous code](#av1215-properly-handle-exceptions-in-asynchronous-code)
  - [AV1220: Always check an event handler delegate for `null`](#av1220-always-check-an-event-handler-delegate-for-null)
  - [AV1235: Don't pass `null` as the `sender` argument when raising an event](#av1235-dont-pass-null-as-the-sender-argument-when-raising-an-event)
  - [AV1240: Use generic constraints if applicable](#av1240-use-generic-constraints-if-applicable)
  - [AV1250: Evaluate the result of a LINQ expression before returning it](#av1250-evaluate-the-result-of-a-linq-expression-before-returning-it)
  - [AV1251: Do not use `this` and `base` prefixes unless it is required](#av1251-do-not-use-this-and-base-prefixes-unless-it-is-required)
- [Maintainability Guidelines](#maintainability-guidelines)
  - [AV1500: Methods should not exceed 7 statements](#av1500-methods-should-not-exceed-7-statements)
  - [AV1501: Make all members `private` and types `internal sealed` by default](#av1501-make-all-members-private-and-types-internal-sealed-by-default)
  - [AV1502: Avoid conditions with double negatives](#av1502-avoid-conditions-with-double-negatives)
  - [AV1505: Name assemblies after their contained namespace](#av1505-name-assemblies-after-their-contained-namespace)
  - [AV1506: Name a source file to the type it contains](#av1506-name-a-source-file-to-the-type-it-contains)
  - [AV1507: Limit the contents of a source code file to one type](#av1507-limit-the-contents-of-a-source-code-file-to-one-type)
  - [AV1508: Name a source file to the logical function of the partial type](#av1508-name-a-source-file-to-the-logical-function-of-the-partial-type)
  - [AV1510: Use `using` statements instead of fully qualified type names](#av1510-use-using-statements-instead-of-fully-qualified-type-names)
  - [AV1515: Don't use "magic" numbers](#av1515-dont-use-magic-numbers)
  - [AV1520: Only use `var` when the type is evident](#av1520-only-use-var-when-the-type-is-evident)
  - [AV1521: Declare and initialize variables as late as possible](#av1521-declare-and-initialize-variables-as-late-as-possible)
  - [AV1522: Assign each variable in a separate statement](#av1522-assign-each-variable-in-a-separate-statement)
  - [AV1523: Favor object and collection initializers over separate statements](#av1523-favor-object-and-collection-initializers-over-separate-statements)
  - [AV1525: Don't make explicit comparisons to `true` or `false`](#av1525-dont-make-explicit-comparisons-to-true-or-false)
  - [AV1530: Don't change a loop variable inside a `for` loop](#av1530-dont-change-a-loop-variable-inside-a-for-loop)
  - [AV1532: Avoid nested loops](#av1532-avoid-nested-loops)
  - [DG1535: Always add a block after the keywords `if`, `else`, `do`, `while`, `for`, `foreach` and `case`](#dg1535-always-add-a-block-after-the-keywords-if-else-do-while-for-foreach-and-case)
  - [AV1536: Always add a `default` block after the last `case` in a `switch` statement](#av1536-always-add-a-default-block-after-the-last-case-in-a-switch-statement)
  - [AV1537: Finish every `if`-`else`-`if` statement with an `else` clause](#av1537-finish-every-if-else-if-statement-with-an-else-clause)
  - [AV1540: Be reluctant with multiple `return` statements](#av1540-be-reluctant-with-multiple-return-statements)
  - [AV1545: Don't use an `if`-`else` construct instead of a simple (conditional) assignment](#av1545-dont-use-an-if-else-construct-instead-of-a-simple-conditional-assignment)
  - [AV1546: Prefer interpolated strings over concatenation or `string.Format`](#av1546-prefer-interpolated-strings-over-concatenation-or-stringformat)
  - [AV1547: Encapsulate complex expressions in a property, method or local function](#av1547-encapsulate-complex-expressions-in-a-property-method-or-local-function)
  - [AV1551: Call the more overloaded method from other overloads](#av1551-call-the-more-overloaded-method-from-other-overloads)
  - [AV1553: Only use optional parameters to replace overloads](#av1553-only-use-optional-parameters-to-replace-overloads)
  - [AV1554: Do not use optional parameters in interface methods or their concrete implementations](#av1554-do-not-use-optional-parameters-in-interface-methods-or-their-concrete-implementations)
  - [AV1555: Avoid using named arguments](#av1555-avoid-using-named-arguments)
  - [AV1561: Don't declare signatures with more than 3 parameters](#av1561-dont-declare-signatures-with-more-than-3-parameters)
  - [AV1562: Don't use `ref` or `out` parameters](#av1562-dont-use-ref-or-out-parameters)
  - [AV1564: Avoid signatures that take a `bool` parameter](#av1564-avoid-signatures-that-take-a-bool-parameter)
  - [AV1568: Don't use parameters as temporary variables](#av1568-dont-use-parameters-as-temporary-variables)
  - [AV1570: Prefer `is` patterns over `as` operations](#av1570-prefer-is-patterns-over-as-operations)
  - [AV1575: Don't comment out code](#av1575-dont-comment-out-code)
  - [AV1580: Write code that is easy to debug](#av1580-write-code-that-is-easy-to-debug)
- [Naming Guidelines](#naming-guidelines)
  - [AV1701: Use US English](#av1701-use-us-english)
  - [DG1702: Use proper casing for language elements](#dg1702-use-proper-casing-for-language-elements)
  - [AV1704: Don't include numbers in variables, parameters and type members](#av1704-dont-include-numbers-in-variables-parameters-and-type-members)
  - [AV1705: Don't prefix fields](#av1705-dont-prefix-fields)
  - [AV1706: Don't use abbreviations](#av1706-dont-use-abbreviations)
  - [AV1707: Name members, parameters and variables according to their meaning and not their type](#av1707-name-members-parameters-and-variables-according-to-their-meaning-and-not-their-type)
  - [AV1708: Name types using nouns, noun phrases or adjective phrases](#av1708-name-types-using-nouns-noun-phrases-or-adjective-phrases)
  - [AV1709: Name generic type parameters with descriptive names](#av1709-name-generic-type-parameters-with-descriptive-names)
  - [AV1710: Don't repeat the name of a class or enumeration in its members](#av1710-dont-repeat-the-name-of-a-class-or-enumeration-in-its-members)
  - [AV1711: Name members similarly to members of related .NET Framework classes](#av1711-name-members-similarly-to-members-of-related-net-framework-classes)
  - [AV1712: Avoid short names or names that can be mistaken for other names](#av1712-avoid-short-names-or-names-that-can-be-mistaken-for-other-names)
  - [AV1715: Properly name properties](#av1715-properly-name-properties)
  - [AV1720: Name methods and local functions using verbs or verb-object pairs](#av1720-name-methods-and-local-functions-using-verbs-or-verb-object-pairs)
  - [AV1725: Name namespaces using names, layers, verbs and features](#av1725-name-namespaces-using-names-layers-verbs-and-features)
  - [AV1735: Use a verb or verb phrase to name an event](#av1735-use-a-verb-or-verb-phrase-to-name-an-event)
  - [AV1737: Use `-ing` and `-ed` to express pre-events and post-events](#av1737-use--ing-and--ed-to-express-pre-events-and-post-events)
  - [AV1738: Prefix an event handler with "On"](#av1738-prefix-an-event-handler-with-on)
  - [AV1739: Use an underscore for irrelevant lambda parameters](#av1739-use-an-underscore-for-irrelevant-lambda-parameters)
  - [AV1745: Group extension methods in a class suffixed with Extensions](#av1745-group-extension-methods-in-a-class-suffixed-with-extensions)
  - [AV1755: Postfix asynchronous methods with `Async` or `TaskAsync`](#av1755-postfix-asynchronous-methods-with-async-or-taskasync)
- [Performance Guidelines](#performance-guidelines)
  - [AV1800: Consider using `Any()` to determine whether an `IEnumerable<T>` is empty](#av1800-consider-using-any-to-determine-whether-an-ienumerablet-is-empty)
  - [AV1820: Only use `async` for low-intensive long-running activities](#av1820-only-use-async-for-low-intensive-long-running-activities)
  - [AV1825: Prefer `Task.Run` or `Task.Factory.StartNew` for CPU-intensive activities](#av1825-prefer-taskrun-or-taskfactorystartnew-for-cpu-intensive-activities)
  - [AV1830: Beware of mixing up `async`/`await` with `Task.Wait`](#av1830-beware-of-mixing-up-asyncawait-with-taskwait)
  - [AV1835: Beware of `async`/`await` deadlocks in special environments (e.g. WPF)](#av1835-beware-of-asyncawait-deadlocks-in-special-environments-eg-wpf)
  - [AV1840: Await `ValueTask` and `ValueTask<T>` directly and exactly once](#av1840-await-valuetask-and-valuetaskt-directly-and-exactly-once)
- [Framework Guidelines](#framework-guidelines)
  - [AV2201: Use C# type aliases instead of the types from the `System` namespace](#av2201-use-c-type-aliases-instead-of-the-types-from-the-system-namespace)
  - [AV2202: Prefer language syntax over explicit calls to underlying implementations](#av2202-prefer-language-syntax-over-explicit-calls-to-underlying-implementations)
  - [AV2207: Don't hard-code strings that change based on the deployment](#av2207-dont-hard-code-strings-that-change-based-on-the-deployment)
  - [AV2210: Build with the highest warning level](#av2210-build-with-the-highest-warning-level)
  - [AV2220: Avoid LINQ query syntax for simple expressions](#av2220-avoid-linq-query-syntax-for-simple-expressions)
  - [AV2221: Use lambda expressions instead of anonymous methods](#av2221-use-lambda-expressions-instead-of-anonymous-methods)
  - [AV2230: Only use the `dynamic` keyword when talking to a dynamic object](#av2230-only-use-the-dynamic-keyword-when-talking-to-a-dynamic-object)
  - [AV2235: Favor `async`/`await` over `Task` continuations](#av2235-favor-asyncawait-over-task-continuations)
- [Documentation Guidelines](#documentation-guidelines)
  - [AV2301: Write comments and documentation in US English](#av2301-write-comments-and-documentation-in-us-english)
  - [AV2305: Document all `public`, `protected` and `internal` types and members](#av2305-document-all-public-protected-and-internal-types-and-members)
  - [AV2306: Write XML documentation with other developers in mind](#av2306-write-xml-documentation-with-other-developers-in-mind)
  - [AV2307: Write MSDN-style documentation](#av2307-write-msdn-style-documentation)
  - [AV2310: Avoid inline comments](#av2310-avoid-inline-comments)
  - [AV2316: Only write comments to explain complex algorithms or decisions](#av2316-only-write-comments-to-explain-complex-algorithms-or-decisions)
  - [AV2318: Don't use comments for tracking work to be done later](#av2318-dont-use-comments-for-tracking-work-to-be-done-later)
- [Layout Guidelines](#layout-guidelines)
  - [DG2400: Use a common layout](#dg2400-use-a-common-layout)
  - [DG2402: Order namespaces in alphabetic order](#dg2402-order-namespaces-in-alphabetic-order)
  - [DG2406: Place members in a well-defined order](#dg2406-place-members-in-a-well-defined-order)
  - [AV2407:  Do not use `#region`](#av2407--do-not-use-region)
  - [AV2410: Use expression-bodied members appropriately](#av2410-use-expression-bodied-members-appropriately)
- [About this document](#about-this-document)
  - [Useful links](#useful-links)
  - [What is this](#what-is-this)
  - [What is different compared to Aviva / CSharpGuidelines](#what-is-different-compared-to-aviva--csharpguidelines)
  - [Why would you use this document](#why-would-you-use-this-document)
  - [Basic principles](#basic-principles)
  - [How do you get started](#how-do-you-get-started)
  - [Why did Dennis Doomen create it](#why-did-dennis-doomen-create-it)
  - [Is this a coding standard](#is-this-a-coding-standard)
  - [Feedback and disclaimer](#feedback-and-disclaimer)
  - [Can I create my own version](#can-i-create-my-own-version)

## Class Design Guidelines

### AV1000: A class or interface should have a single purpose

A class or interface should have a single purpose within the system it functions in. In general, a class either represents a primitive type like an email or ISBN number, an abstraction of some business concept, a plain data structure, or is responsible for orchestrating the interaction between other classes. It is never a combination of those. This rule is widely known as the [Single Responsibility Principle](https://8thlight.com/blog/uncle-bob/2014/05/08/SingleReponsibilityPrinciple.html), one of the S.O.L.I.D. principles.

**Tip:** A class with the word `And` in it is an obvious violation of this rule.

**Tip:** Use [Design Patterns](http://en.wikipedia.org/wiki/Design_pattern_(computer_science)) to communicate the intent of a class. If you can't assign a single design pattern to a class, chances are that it is doing more than one thing.

**Note** If you create a class representing a primitive type you can greatly simplify its use by making it immutable.

### AV1001: Only create a constructor that returns a useful object

There should be no need to set additional properties before the object can be used for whatever purpose it was designed. However, if your constructor needs more than three parameters (which violates [AV1561](#av1561-dont-declare-signatures-with-more-than-3-parameters)), your class might have too much responsibility (and violates [AV1000](#av1000-a-class-or-interface-should-have-a-single-purpose)).

### AV1003: An interface should be small and focused

Interfaces should have a name that clearly explains their purpose or role in the system. Do not combine many vaguely related members on the same interface just because they were all on the same class. Separate the members based on the responsibility of those members, so that callers only need to call or implement the interface related to a particular task. This rule is more commonly known as the [Interface Segregation Principle](https://lostechies.com/wp-content/uploads/2011/03/pablos_solid_ebook.pdf).

### AV1004: Use an interface rather than a base class to support multiple implementations

If you want to expose an extension point from your class, expose it as an interface rather than as a base class. You don't want to force users of that extension point to derive their implementations from a base class that might have an undesired behavior. However, for their convenience you may implement a(n abstract) default implementation that can serve as a starting point.

### AV1005: Use an interface to decouple classes from each other

Interfaces are a very effective mechanism for decoupling classes from each other:

- They can prevent bidirectional associations.
- They simplify the replacement of one implementation with another.
- They allow the replacement of an expensive external service or resource with a temporary stub for use in a non-production environment.
- They allow the replacement of the actual implementation with a dummy implementation or a fake object in a unit test.
- Using a dependency injection framework you can centralize the choice of which class is used whenever a specific interface is requested.

### AV1008: Avoid static classes

With the exception of extension method containers, static classes very often lead to badly designed code. They are also very difficult, if not impossible, to test in isolation, unless you're willing to use some very hacky tools.

**Note:** If you really need that static class, mark it as static so that the compiler can prevent instance members and instantiating your class. This relieves you of creating an explicit private constructor.

### AV1010: Don't suppress compiler warnings using the `new` keyword

Compiler warning [CS0114](https://docs.microsoft.com/en-us/dotnet/csharp/misc/cs0114) is issued when breaking [Polymorphism](http://en.wikipedia.org/wiki/Polymorphism_in_object-oriented_programming), one of the most essential object-orientation principles.
The warning goes away when you add the `new` keyword, but it keeps sub-classes difficult to understand. Consider the following two classes:

```csharp
public class Book  
{
    public virtual void Print()  
    {
        Console.WriteLine("Printing Book");
    }  
}

public class PocketBook : Book  
{
    public new void Print()
    {
        Console.WriteLine("Printing PocketBook");
    }  
}
```

This will cause behavior that you would not normally expect from class hierarchies:

```csharp
PocketBook pocketBook = new PocketBook();

pocketBook.Print(); // Outputs "Printing PocketBook "

((Book)pocketBook).Print(); // Outputs "Printing Book"
```

It should not make a difference whether you call `Print()` through a reference to the base class or through the derived class.

### AV1011: It should be possible to treat a derived type as if it were a base type

In other words, you should be able to pass an instance of a derived class wherever its base class is expected, without the callee knowing the derived class. A very notorious example of a violation of this rule is throwing a `NotImplementedException` when overriding methods from a base class. A less subtle example is not honoring the behavior expected by the base class.
  
**Note:** This rule is also known as the Liskov Substitution Principle, one of the [S.O.L.I.D.](http://www.lostechies.com/blogs/chad_myers/archive/2008/03/07/pablo-s-topic-of-the-month-march-solid-principles.aspx) principles.

### AV1013: Don't refer to derived classes from the base class

Having dependencies from a base class to its sub-classes goes against proper object-oriented design and might prevent other developers from adding new derived classes.

### AV1014: Avoid exposing the other objects an object depends on

If you find yourself writing code like this then you might be violating the [Law of Demeter](http://en.wikipedia.org/wiki/Law_of_Demeter).

```csharp
someObject.SomeProperty.GetChild().Foo()
```

An object should not expose any other classes it depends on because callers may misuse that exposed property or method to access the object behind it. By doing so, you allow calling code to become coupled to the class you are using, and thereby limiting the chance that you can easily replace it in a future stage.

**Note:** Using a class that is designed using the [Fluent Interface](http://en.wikipedia.org/wiki/Fluent_interface) pattern seems to violate this rule, but it is simply returning itself so that method chaining is allowed.

**Exception:** Inversion of Control or Dependency Injection frameworks often require you to expose a dependency as a public property. As long as this property is not used for anything other than dependency injection I would not consider it a violation.

### AV1020: Avoid bidirectional dependencies

This means that two classes know about each other's public members or rely on each other's internal behavior. Refactoring or replacing one of those classes requires changes on both parties and may involve a lot of unexpected work. The most obvious way of breaking that dependency is to introduce an interface for one of the classes and using Dependency Injection.

**Exception:** Domain models such as defined in [Domain-Driven Design](http://domaindrivendesign.org/) tend to occasionally involve bidirectional associations that model real-life associations. In those cases, make sure they are really necessary, and if they are, keep them in.

### AV1025: Classes should have state and behavior

In general, if you find a lot of data-only classes in your code base, you probably also have a few (static) classes with a lot of behavior (see [AV1008](#av1008-avoid-static-classes)). Use the principles of object-orientation explained in this section and move the logic close to the data it applies to.

**Exception:** The only exceptions to this rule are classes that are used to transfer data over a communication channel, also called [Data Transfer Objects](http://martinfowler.com/eaaCatalog/dataTransferObject.html), or a class that wraps several parameters of a method.

### AV1026: Classes should protect the consistency of their internal state

Validate incoming arguments from public members. For example:

```csharp
public void SetAge(int years)
{
    AssertValueIsInRange(years, 0, 200, nameof(years));

    this.age = years;
}
```

Protect invariants on internal state. For example:

```csharp
public void Render()
{
    AssertNotDisposed();

    // ...
}
```

## Member Design Guidelines

### AV1100: Allow properties to be set in any order

Properties should be stateless with respect to other properties, i.e. there should not be a difference between first setting property `DataSource` and then `DataMember` or vice-versa.

### AV1105: Use a method instead of a property

- If the work is more expensive than setting a field value.
- If it represents a conversion such as the `Object.ToString` method.
- If it returns a different result each time it is called, even if the arguments didn't change. For example, the `NewGuid` method returns a different value each time it is called.
- If the operation causes a side effect such as changing some internal state not directly related to the property (which violates the [Command Query Separation](http://martinfowler.com/bliki/CommandQuerySeparation.html) principle).

**Exception:** Populating an internal cache or implementing [lazy-loading](http://www.martinfowler.com/eaaCatalog/lazyLoad.html) is a good exception.

### AV1110: Don't use mutually exclusive properties

Having properties that cannot be used at the same time typically signals a type that represents two conflicting concepts. Even though those concepts may share some of their behavior and states, they obviously have different rules that do not cooperate.

This violation is often seen in domain models and introduces all kinds of conditional logic related to those conflicting rules, causing a ripple effect that significantly increases the maintenance burden.

### AV1115: A property, method or local function should do only one thing

Similarly to rule [AV1000](#av1000-a-class-or-interface-should-have-a-single-purpose), a method body should have a single responsibility.

### AV1125: Don't expose stateful objects through static members

A stateful object is an object that contains many properties and lots of behavior behind it. If you expose such an object through a static property or method of some other object, it will be very difficult to refactor or unit test a class that relies on such a stateful object. In general, introducing a construct like that is a great example of violating many of the guidelines of this chapter.

A classic example of this is the `HttpContext.Current` property, part of ASP.NET. Many see the `HttpContext` class as a source of a lot of ugly code.

### AV1130: Return interfaces to unchangeable collections

You generally don't want callers to be able to change an internal collection, so don't return arrays, lists or other collection classes directly. Instead, return an `IEnumerable<T>`, `IAsyncEnumerable<T>`, `IQueryable<T>`, `IReadOnlyCollection<T>`, `IReadOnlyList<T>`, `IReadOnlySet<T>` or `IReadOnlyDictionary<TKey, TValue>`.

**Exception:** Immutable collections such as `ImmutableArray<T>`, `ImmutableList<T>` and `ImmutableDictionary<TKey, TValue>` prevent modifications from the outside and are thus allowed.

### AV1135: Properties, arguments and return values representing strings, collections or tasks should never be `null`

Returning `null` can be unexpected by the caller. Always return an empty collection or an empty string instead of a `null` reference. When your member returns `Task` or `Task<T>`, return `Task.CompletedTask` or `Task.FromResult()`. This also prevents cluttering your code base with additional checks for `null`, or even worse, `string.IsNullOrEmpty()`.

### AV1137: Define parameters as specific as possible

If your method or local function needs a specific piece of data, define parameters as specific as that and don't take a container object instead. For instance, consider a method that needs a connection string that is exposed through a central `IConfiguration` interface. Rather than taking a dependency on the entire configuration, just define a parameter for the connection string. This not only prevents unnecessary coupling, it also improves maintainability in the long run.

**Note:** An easy trick to remember this guideline is the *Don't ship the truck if you only need a package*.

### AV1140: Consider using domain-specific value types rather than primitives

Instead of using strings, integers and decimals for representing domain-specific types such as an ISBN number, an email address or amount of money, consider creating dedicated value objects that wrap both the data and the validation rules that apply to it. By doing this, you prevent ending up having multiple implementations of the same business rules, which both improves maintainability and prevents bugs.

## Miscellaneous Design Guidelines

### AV1200: Throw exceptions rather than returning some kind of status value

A code base that uses return values to report success or failure tends to have nested if-statements sprinkled all over the code. Quite often, a caller forgets to check the return value anyway. Structured exception handling has been introduced to allow you to throw exceptions and catch or replace them at a higher layer. In most systems it is quite common to throw exceptions whenever an unexpected situation occurs.

### AV1202: Provide a rich and meaningful exception message text

The message should explain the cause of the exception, and clearly describe what needs to be done to avoid the exception.

### AV1205: Throw the most specific exception that is appropriate

For example, if a method receives a `null` argument, it should throw `ArgumentNullException` instead of its base type `ArgumentException`.

### AV1210: Don't swallow errors by catching generic exceptions

Avoid swallowing errors by catching non-specific exceptions, such as `Exception`, `SystemException`, and so on, in application code. Only in top-level code, such as a last-chance exception handler, you should catch a non-specific exception for logging purposes and a graceful shutdown of the application.

### AV1215: Properly handle exceptions in asynchronous code

When throwing or handling exceptions in code that uses `async`/`await` or a `Task` remember the following two rules:

- Exceptions that occur within an `async`/`await` block and inside a `Task`'s action are propagated to the awaiter.
- Exceptions that occur in the code preceding the asynchronous block are propagated to the caller.

### AV1220: Always check an event handler delegate for `null`

An event that has no subscribers is `null`. So before invoking, always make sure that the delegate list represented by the event variable is not `null`.
Invoke using the null conditional operator, because it additionally prevents conflicting changes to the delegate list from concurrent threads.

```csharp
event EventHandler<NotifyEventArgs> Notify;

protected virtual void OnNotify(NotifyEventArgs args)
{
    Notify?.Invoke(this, args);
}
```

### AV1235: Don't pass `null` as the `sender` argument when raising an event

Often an event handler is used to handle similar events from multiple senders. The sender argument is then used to get to the source of the event. Always pass a reference to the source (typically `this`) when raising the event. Furthermore don't pass `null` as the event data parameter when raising an event. If there is no event data, pass `EventArgs.Empty` instead of `null`.

**Exception:** On static events, the sender argument should be `null`.

### AV1240: Use generic constraints if applicable

Instead of casting to and from the object type in generic types or methods, use `where` constraints or the `as` operator to specify the exact characteristics of the generic parameter. For example:

```csharp
class SomeClass  
{

}

// Don't  
class MyClass  
{
    void SomeMethod(T t)  
    {  
        object temp = t;
        SomeClass obj = (SomeClass) temp;
    }  
}

// Do  
class MyClass where T : SomeClass  
{
    void SomeMethod(T t)  
    {  
        SomeClass obj = t;
    }  
}
```

### AV1250: Evaluate the result of a LINQ expression before returning it

Consider the following code snippet

```csharp
public IEnumerable<GoldMember> GetGoldMemberCustomers()
{
    const decimal GoldMemberThresholdInEuro = 1_000_000;

    var query =
        from customer in db.Customers
        where customer.Balance > GoldMemberThresholdInEuro
        select new GoldMember(customer.Name, customer.Balance);

    return query;
}
```

Since LINQ queries use deferred execution, returning `query` will actually return the expression tree representing the above query. Each time the caller evaluates this result using a `foreach` loop or similar, the entire query is re-executed resulting in new instances of `GoldMember` every time. Consequently, you cannot use the `==` operator to compare multiple `GoldMember` instances. Instead, always explicitly evaluate the result of a LINQ query using `ToList()`, `ToArray()` or similar methods.

### AV1251: Do not use `this` and `base` prefixes unless it is required

In a class hierarchy, it is not necessary to know at which level a member is declared to use it. Refactoring derived classes is harder if that level is fixed in the code.

## Maintainability Guidelines

### AV1500: Methods should not exceed 7 statements

A method that requires more than 7 statements is simply doing too much or has too many responsibilities. It also requires the human mind to analyze the exact statements to understand what the code is doing. Break it down into multiple small and focused methods with self-explaining names, but make sure the high-level algorithm is still clear.

### AV1501: Make all members `private` and types `internal sealed` by default

To make a more conscious decision on which members to make available to other classes, first restrict the scope as much as possible. Then carefully decide what to expose as a public member or type.

### AV1502: Avoid conditions with double negatives

Although a property like `customer.HasNoOrders` makes sense, avoid using it in a negative condition like this:

```csharp
bool hasOrders = !customer.HasNoOrders;
```

Double negatives are more difficult to grasp than simple expressions, and people tend to read over the double negative easily.

### AV1505: Name assemblies after their contained namespace

All DLLs should be named according to the pattern *Company*.*Component*.dll where *Company* refers to your company's name and *Component* contains one or more dot-separated clauses. For example `AvivaSolutions.Web.Controls.dll`.

As an example, consider a group of classes organized under the namespace `AvivaSolutions.Web.Binding` exposed by a certain assembly. According to this guideline, that assembly should be called `AvivaSolutions.Web.Binding.dll`.

**Exception:** If you decide to combine classes from multiple unrelated namespaces into one assembly, consider suffixing the assembly name with `Core`, but do not use that suffix in the namespaces. For instance, `AvivaSolutions.Consulting.Core.dll`.

### AV1506: Name a source file to the type it contains

Use Pascal casing to name the file and don't use underscores. Don't include (the number of) generic type parameters in the file name.

### AV1507: Limit the contents of a source code file to one type

**Exception:** Nested types should be part of the same file.

**Exception:** Types that only differ by their number of generic type parameters should be part of the same file.

### AV1508: Name a source file to the logical function of the partial type

When using partial types and allocating a part per file, name each file after the logical part that part plays. For example:

```csharp
// In MyClass.cs
public partial class MyClass
{...}

// In MyClass.Designer.cs
public partial class MyClass
{...}
```

### AV1510: Use `using` statements instead of fully qualified type names

Limit usage of fully qualified type names to prevent name clashing. For example, don't do this:

```csharp
var list = new System.Collections.Generic.List<string>();
```

Instead, do this:

```csharp
using System.Collections.Generic;

var list = new List<string>();
```

If you do need to prevent name clashing, use a `using` directive to assign an alias:

```csharp
using Label = System.Web.UI.WebControls.Label;
```

### AV1515: Don't use "magic" numbers

Don't use literal values, either numeric or strings, in your code, other than to define symbolic constants. For example:

```csharp
public class Whatever  
{
    public static readonly Color PapayaWhip = new Color(0xFFEFD5);
    public const int MaxNumberOfWheels = 18;
    public const byte ReadCreateOverwriteMask = 0b0010_1100;
}
```

Strings intended for logging or tracing are exempt from this rule. Literals are allowed when their meaning is clear from the context, and not subject to future changes, For example:

```csharp
mean = (a + b) / 2; // okay  
WaitMilliseconds(waitTimeInSeconds * 1000); // clear enough
```

If the value of one constant depends on the value of another, attempt to make this explicit in the code.

```csharp
public class SomeSpecialContainer  
{  
    public const int MaxItems = 32;
    public const int HighWaterMark = 3 * MaxItems / 4;// at 75%  
}
```

**Note:** An enumeration can often be used for certain types of symbolic constants.

### AV1520: Only use `var` when the type is evident

Use `var` for anonymous types (typically resulting from a LINQ query), or if the type is [evident](https://www.jetbrains.com/help/resharper/2021.3/Using_var_Keyword_in_Declarations.html#use-var-when-evident-details).
Never use `var` for [built-in types](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/built-in-types).

```csharp
// Projection into anonymous type.
var largeOrders =
    from order in dbContext.Orders
    where order.Items.Count > 10 && order.TotalAmount > 1000
    select new { order.Id, order.TotalAmount };

// Built-in types.
bool isValid = true;
string phoneNumber = "(unavailable)";
uint pageSize = Math.Max(itemCount, MaxPageSize);  

// Types are evident.
var customer = new Customer();
var invoice = Invoice.Create(customer.Id);
var user = sessionCache.Resolve<User>("john.doe@mail.com");
var subscribers = new List<Subscriber>();
var summary = shoppingBasket.ToOrderSummary(); 

// All other cases.
IQueryable<Order> recentOrders = ApplyFilter(order => order.CreatedAt > DateTime.Now.AddDays(-30));
LoggerMessage message = Compose(context);
ReadOnlySpan<char> key = ExtractKeyFromPair("email=john.doe@mail.com");
IDictionary<Category, Product> productsPerCategory = shoppingBasket.Products.ToDictionary(product => product.Category);
```

### AV1521: Declare and initialize variables as late as possible

Avoid the C and Visual Basic styles where all variables have to be defined at the beginning of a block, but rather define and initialize each variable at the point where it is needed.

### AV1522: Assign each variable in a separate statement

Don't use confusing constructs like the one below:

```csharp
var result = someField = GetSomeMethod();
```

**Exception:** Multiple assignments per statement are allowed by using out variables, is-patterns or deconstruction into tuples. Examples:

```csharp
bool success = int.TryParse(text, out int result);

if ((items[0] is string text) || (items[1] is Action action))
{
}

(string name, string value) = SplitNameValuePair(text);
```

### AV1523: Favor object and collection initializers over separate statements

Instead of:

```csharp
var startInfo = new ProcessStartInfo("myapp.exe");
startInfo.StandardOutput = Console.Output;
startInfo.UseShellExecute = true;

var countries = new List();
countries.Add("Netherlands");
countries.Add("United States");

var countryLookupTable = new Dictionary<string, string>();
countryLookupTable.Add("NL", "Netherlands");
countryLookupTable.Add("US", "United States");
```

Use [Object and Collection Initializers](http://msdn.microsoft.com/en-us/library/bb384062.aspx):

```csharp
var startInfo = new ProcessStartInfo("myapp.exe")  
{
    StandardOutput = Console.Output,
    UseShellExecute = true  
};

var countries = new List { "Netherlands", "United States" };

var countryLookupTable = new Dictionary<string, string>
{
    ["NL"] = "Netherlands",
    ["US"] = "United States"
};
```

### AV1525: Don't make explicit comparisons to `true` or `false`

It is usually bad style to compare a `bool`-type expression to `true` or `false`. For example:

```csharp
while (condition == false) // wrong; bad style  
while (condition != true) // also wrong  
while (((condition == true) == true) == true) // where do you stop?  
while (condition) // OK
```

### AV1530: Don't change a loop variable inside a `for` loop

Updating the loop variable within the loop body is generally considered confusing, even more so if the loop variable is modified in more than one place.

```csharp
for (int index = 0; index < 10; ++index)  
{  
    if (someCondition)
    {
        index = 11; // Wrong! Use 'break' or 'continue' instead.  
    }
}
```

### AV1532: Avoid nested loops

A method that nests loops is more difficult to understand than one with only a single loop. In fact, in most cases nested loops can be replaced with a much simpler LINQ query that uses the `from` keyword twice or more to *join* the data.

### DG1535: Always add a block after the keywords `if`, `else`, `do`, `while`, `for`, `foreach` and `case`

Please note that this also avoids possible confusion in statements of the form:

```csharp
if (isActive) if (isVisible) Foo(); else Bar(); // which 'if' goes with the 'else'?

// The right way:  
if (isActive)  
{  
    if (isVisible)  
    {  
        Foo()
    }  
    else  
    {  
        Bar();
    }  
}
```

Note that a block after the keyword `using` is also expected, but can be omitted when two `using`s are used successively.
  
**Exception:** `case` statements that only call `return`.  

### AV1536: Always add a `default` block after the last `case` in a `switch` statement

Add a descriptive comment if the `default` block is supposed to be empty. Moreover, if that block is not supposed to be reached throw an `InvalidOperationException` to detect future changes that may fall through the existing cases. This ensures better code, because all paths the code can travel have been thought about.

```csharp
void Foo(string answer)  
{  
    switch (answer)  
    {  
        case "no":  
        {
            Console.WriteLine("You answered with No");
            break;
        }  

        case "yes":
        {  
            Console.WriteLine("You answered with Yes");
            break;
        }

        default:  
        {
            // Not supposed to end up here.  
            throw new InvalidOperationException("Unexpected answer " + answer);
        }  
    }  
}
```

### AV1537: Finish every `if`-`else`-`if` statement with an `else` clause

For example:

```csharp
void Foo(string answer)  
{  
    if (answer == "no")  
    {  
        Console.WriteLine("You answered with No");
    }  
    else if (answer == "yes")  
    {  
        Console.WriteLine("You answered with Yes");
    }  
    else  
    {  
        // What should happen when this point is reached? Ignored? If not,
        // throw an InvalidOperationException.  
    }  
}
```

### AV1540: Be reluctant with multiple `return` statements

One entry, one exit is a sound principle and keeps control flow readable. However, if the method body is very small and complies with guideline [AV1500](#av1500-methods-should-not-exceed-7-statements) then multiple return statements may actually improve readability over some central boolean flag that is updated at various points.

### AV1545: Don't use an `if`-`else` construct instead of a simple (conditional) assignment

Express your intentions directly. For example, rather than:

```csharp
bool isPositive;

if (value > 0)
{
    isPositive = true;
}
else
{
    isPositive = false;
}
```

write:

```csharp
bool isPositive = value > 0;
```

Or instead of:

```csharp
string classification;

if (value > 0)
{
    classification = "positive";
}
else
{
    classification = "negative";
}

return classification;
```

write:

```csharp
return value > 0 ? "positive" : "negative";
```

Or instead of:

```csharp
int result;

if (offset == null)
{
    result = -1;
}
else
{
    result = offset.Value;
}

return result;
```

write:

```csharp
return offset ?? -1;
```

Or instead of:

```csharp
private DateTime? firstJobStartedAt;

public void RunJob()
{
    if (firstJobStartedAt == null)
    {
        firstJobStartedAt = DateTime.UtcNow;
    }
}
```

write:

```csharp
private DateTime? firstJobStartedAt;

public void RunJob()
{
    firstJobStartedAt ??= DateTime.UtcNow;
}
```

Or instead of:

```csharp
if (employee.Manager != null)
{
    return employee.Manager.Name;
}
else
{
    return null;
}
```

write:

```csharp
return employee.Manager?.Name;
```

### AV1546: Prefer interpolated strings over concatenation or `string.Format`

Since .NET 6, interpolated strings are optimized at compile-time, which inlines constants and reduces memory allocations due to boxing and string copying.

```csharp
// GOOD
string result = $"Welcome, {firstName} {lastName}!";

// BAD
string result = string.Format("Welcome, {0} {1}!", firstName, lastName);

// BAD
string result = "Welcome, " + firstName + " " + lastName + "!";

// BAD
string result = string.Concat("Welcome, ", firstName, " ", lastName, "!");
```

### AV1547: Encapsulate complex expressions in a property, method or local function

Consider the following example:

```csharp
if (member.HidesBaseClassMember && member.NodeType != NodeType.InstanceInitializer)
{
    // do something
}
```

In order to understand what this expression is about, you need to analyze its exact details and all of its possible outcomes. Obviously, you can add an explanatory comment on top of it, but it is much better to replace this complex expression with a clearly named method:

```csharp
if (NonConstructorMemberUsesNewKeyword(member))  
{  
    // do something
}  


private bool NonConstructorMemberUsesNewKeyword(Member member)  
{  
    return member.HidesBaseClassMember &&
           member.NodeType != NodeType.InstanceInitializer;
}
```

You still need to understand the expression if you are modifying it, but the calling code is now much easier to grasp.

### AV1551: Call the more overloaded method from other overloads

This guideline only applies to overloads that are intended to provide optional arguments. Consider, for example, the following code snippet:

```csharp
public class MyString  
{
    private string someText;

    public int IndexOf(string phrase)  
    {  
        return IndexOf(phrase, 0);
    }

    public int IndexOf(string phrase, int startIndex)  
    {  
        return IndexOf(phrase, startIndex, someText.Length - startIndex);
    }

    public virtual int IndexOf(string phrase, int startIndex, int count)  
    {  
        return someText.IndexOf(phrase, startIndex, count);
    }  
}
```

The class `MyString` provides three overloads for the `IndexOf` method, but two of them simply call the one with one more parameter. Notice that the same rule applies to class constructors; implement the most complete overload and call that one from the other overloads using the `this()` operator. Also notice that the parameters with the same name should appear in the same position in all overloads.

**Important:** If you also want to allow derived classes to override these methods, define the most complete overload as a non-private `virtual` method that is called by all overloads.

### AV1553: Only use optional parameters to replace overloads

The only valid reason for using C# 4.0's optional parameters is to replace the example from rule [AV1551](#av1551-call-the-more-overloaded-method-from-other-overloads) with a single method like:

```csharp
public virtual int IndexOf(string phrase, int startIndex = 0, int count = -1)
{
    int length = count == -1 ? someText.Length - startIndex : count;
    return someText.IndexOf(phrase, startIndex, length);
}
```

Since strings, collections and tasks should never be `null` according to rule [AV1135](#av1135-properties-arguments-and-return-values-representing-strings-collections-or-tasks-should-never-be-null), if you have an optional parameter of these types with default value `null` then you must use overloaded methods instead.

Strings, unlike other reference types, can have non-null default values. So an optional string parameter may be used to replace overloads with the condition of having a non-null default value.

Regardless of optional parameters' types, following caveats always apply:

1) The default values of the optional parameters are stored at the caller side. As such, changing the default argument without recompiling the calling code will not apply the new default value. Unless your method is private or internal, this aspect should be carefully considered before choosing optional parameters over method overloads.

2) If optional parameters cause the method to follow and/or exit from alternative paths, overloaded methods are probably a better fit for your case.

### AV1554: Do not use optional parameters in interface methods or their concrete implementations

When an interface method defines an optional parameter, its default value is discarded during overload resolution unless you call the concrete class through the interface reference.

When a concrete implementation of an interface method sets a default argument for a parameter, the default value is discarded during overload resolution if you call the concrete class through the interface reference.

See the series on optional argument corner cases by Eric Lippert (part [one](https://docs.microsoft.com/en-us/archive/blogs/ericlippert/optional-argument-corner-cases-part-one), [two](https://docs.microsoft.com/en-us/archive/blogs/ericlippert/optional-argument-corner-cases-part-two), [three](https://docs.microsoft.com/en-us/archive/blogs/ericlippert/optional-argument-corner-cases-part-three), [four](https://docs.microsoft.com/en-us/archive/blogs/ericlippert/optional-argument-corner-cases-part-four)) for more details.

### AV1555: Avoid using named arguments

C# 4.0's named arguments have been introduced to make it easier to call COM components that are known for offering many optional parameters. If you need named arguments to improve the readability of the call to a method, that method is probably doing too much and should be refactored.

**Exception:** The only exception where named arguments improve readability is when calling a method of some code base you don't control that has a `bool` parameter, like this:  

```csharp
object[] myAttributes = type.GetCustomAttributes(typeof(MyAttribute), inherit: false);
```

### AV1561: Don't declare signatures with more than 3 parameters

To keep constructors, methods, delegates and local functions small and focused, do not use more than three parameters. Do not use tuple parameters. Do not return tuples with more than two elements.

If you want to use more parameters, use a structure or class to pass multiple arguments, as explained in the [Specification design pattern](http://en.wikipedia.org/wiki/Specification_pattern).
In general, the fewer the parameters, the easier it is to understand the method. Additionally, unit testing a method with many parameters requires many scenarios to test.

**Exception:** A parameter that is a collection of tuples is allowed.

### AV1562: Don't use `ref` or `out` parameters

They make code less understandable and might cause people to introduce bugs. Instead, return compound objects or tuples.

**Exception:** Calling and declaring members that implement the [TryParse](https://docs.microsoft.com/en-us/dotnet/api/system.int32.tryparse) pattern is allowed. For example:

```csharp
bool success = int.TryParse(text, out int number);
```

### AV1564: Avoid signatures that take a `bool` parameter

Consider the following method signature:

```csharp
public Customer CreateCustomer(bool platinumLevel) 
{

}
```

On first sight this signature seems perfectly fine, but when calling this method you will lose this purpose completely:

```csharp
Customer customer = CreateCustomer(true);
```

Often, a method taking such a bool is doing more than one thing and needs to be refactored into two or more methods. An alternative solution is to replace the bool with an enumeration.

### AV1568: Don't use parameters as temporary variables

Never use a parameter as a convenient variable for storing temporary state. Even though the type of your temporary variable may be the same, the name usually does not reflect the purpose of the temporary variable.

### AV1570: Prefer `is` patterns over `as` operations

If you use 'as' to safely upcast an interface reference to a certain type, always verify that the operation does not return `null`. Failure to do so may cause a `NullReferenceException` at a later stage if the object did not implement that interface.
Pattern matching syntax prevents this and improves readability. For example, instead of:

```csharp
var remoteUser = user as RemoteUser;
if (remoteUser != null)
{
}
```

write:

```csharp
if (user is RemoteUser remoteUser)
{
}
```

### AV1575: Don't comment out code

Never check in code that is commented out. Instead, use a work item tracking system to keep track of some work to be done. Nobody knows what to do when they encounter a block of commented-out code. Was it temporarily disabled for testing purposes? Was it copied as an example? Should I delete it?

### AV1580: Write code that is easy to debug

Because debugger breakpoints cannot be set inside expressions, avoid overuse of nested method calls. For example, a line like:

```csharp
string result = ConvertToXml(ApplyTransforms(ExecuteQuery(GetConfigurationSettings(source))));
```

requires extra steps to inspect intermediate method return values. On the other hard, were this expression broken into intermediate variables, setting a breakpoint on one of them would be sufficient.

**Note** This does not apply to chaining method calls, which is a common pattern in fluent APIs.

## Naming Guidelines

### AV1701: Use US English

All identifiers (such as types, type members, parameters and variables) should be named using words from the American English language.

- Choose easily readable, preferably grammatically correct names. For example, `HorizontalAlignment` is more readable than `AlignmentHorizontal`.
- Favor readability over brevity. The property name `CanScrollHorizontally` is better than `ScrollableX` (an obscure reference to the X-axis).
- Avoid using names that conflict with keywords of widely used programming languages.

### DG1702: Use proper casing for language elements

| Language element                                  | Casing | Example                                                                                                                                                                |
| :------------------------------------------------ | :----- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Namespace                                         | Pascal | `System.Drawing`                                                                                                                                                       |
| Type parameter                                    | Pascal | `TView`                                                                                                                                                                |
| Interface                                         | Pascal | `IBusinessService`                                                                                                                                                     |
| Class, struct                                     | Pascal | `AppDomain`                                                                                                                                                            |
| Enum                                              | Pascal | `ErrorLevel`                                                                                                                                                           |
| Enum member                                       | Pascal | `FatalError`                                                                                                                                                           |
| Resource key                                      | Pascal | `SaveButtonTooltipText`                                                                                                                                                |
| Private field (incl. const / static readonly)     | Camel  | `listItem`                                                                                                                                                             |
| Non-private field (incl. const / static readonly) | Pascal | `MainPanel`                                                                                                                                                            |
| Property                                          | Pascal | `BackColor`                                                                                                                                                            |
| Event                                             | Pascal | `Click`                                                                                                                                                                |
| Method                                            | Pascal | `ToString`                                                                                                                                                             |
| Local function                                    | Pascal | `FormatText`                                                                                                                                                           |
| Parameter                                         | Camel  | `typeName`                                                                                                                                                             |
| Tuple element names                               | Pascal | `(string First, string Last) name = ("John", "Doe");` <br/>`var name = (First: "John", Last: "Doe");` <br/>`(string First, string Last) GetName() => ("John", "Doe");` |
| Variables declared using tuple syntax             | Camel  | `(string first, string last) = ("John", "Doe");` <br/>`var (first, last) = ("John", "Doe");` <br/>                                                                     |
|                                                   |        | `var (first, last) = ("John", "Doe");`                                                                                                                                 |
| Local variable                                    | Camel  | `listOfValues`                                                                                                                                                         |

**Note:** in case of ambiguity, the rule higher in the table wins.

### AV1704: Don't include numbers in variables, parameters and type members

In most cases they are a lazy excuse for not defining a clear and intention-revealing name.

### AV1705: Don't prefix fields

For example, don't use `g_` or `s_` to distinguish static from non-static fields. A method in which it is difficult to distinguish local variables from member fields is generally too big. Examples of incorrect identifier names are: `_currentUser`, `mUserName`, `m_loginTime`.

### AV1706: Don't use abbreviations

For example, use `ButtonOnClick` rather than `BtnOnClick`. Avoid single character variable names, such as `i` or `q`. Use `index` or `query` instead.

**Exceptions:** Use well-known acronyms and abbreviations that are widely accepted or well-known in your work domain. For instance, use acronym `UI` instead of `UserInterface` and abbreviation `Id` instead of `Identity`.

### AV1707: Name members, parameters and variables according to their meaning and not their type

- Use functional names. For example, `GetLength` is a better name than `GetInt`.
- Don't use terms like `Enum`, `Class` or `Struct` in a name.
- Identifiers that refer to a collection type should have plural names.

### AV1708: Name types using nouns, noun phrases or adjective phrases

For example, the name IComponent uses a descriptive noun, ICustomAttributeProvider uses a noun phrase and IPersistable uses an adjective.
Bad examples include `SearchExamination` (a page to search for examinations), `Common` (does not end with a noun, and does not explain its purpose) and `SiteSecurity` (although the name is technically okay, it does not say anything about its purpose).

Don't include terms like `Utility` or `Helper` in classes. Classes with names like that are usually static classes and are introduced without considering object-oriented principles (see also [AV1008](#av1008-avoid-static-classes)).

### AV1709: Name generic type parameters with descriptive names

- Always prefix type parameter names with the letter `T`.
- Always use a descriptive name unless a single-letter name is completely self-explanatory and a longer name would not add value. Use the single letter `T` as the type parameter in that case.
- Consider indicating constraints placed on a type parameter in the name of the parameter. For example, a parameter constrained to `ISession` may be called `TSession`.

### AV1710: Don't repeat the name of a class or enumeration in its members

```csharp
class Employee
{
  // Wrong!
  static GetEmployee() {...}
  DeleteEmployee() {...}

  // Right
  static Get() {...}
  Delete() {...}

  // Also correct.
  AddNewJob() {...}
  RegisterForMeeting() {...}
}
```

### AV1711: Name members similarly to members of related .NET Framework classes

.NET developers are already accustomed to the naming patterns the framework uses, so following this same pattern helps them find their way in your classes as well. For instance, if you define a class that behaves like a collection, provide members like `Add`, `Remove` and `Count` instead of `AddItem`, `Delete` or `NumberOfItems`.

### AV1712: Avoid short names or names that can be mistaken for other names

Although technically correct, statements like the following can be confusing:

```csharp
bool b001 = lo == l0 ? I1 == 11 : lOl != 101;
```

### AV1715: Properly name properties

- Name properties with nouns, noun phrases, or occasionally adjective phrases.
- Name boolean properties with an affirmative phrase. E.g. `CanSeek` instead of `CannotSeek`.
- Consider prefixing boolean properties with `Is`, `Has`, `Can`, `Allows`, or `Supports`.
- Consider giving a property the same name as its type. When you have a property that is strongly typed to an enumeration, the name of the property can be the same as the name of the enumeration. For example, if you have an enumeration named `CacheLevel`, a property that returns one of its values can also be named `CacheLevel`.

### AV1720: Name methods and local functions using verbs or verb-object pairs

Name a method or local function using a verb like `Show` or a verb-object pair such as `ShowDialog`. A good name should give a hint on the *what* of a member, and if possible, the *why*.

Also, don't include `And` in the name of a method or local function. That implies that it is doing more than one thing, which violates the Single Responsibility Principle explained in [AV1115](#av1115-a-property-method-or-local-function-should-do-only-one-thing).

### AV1725: Name namespaces using names, layers, verbs and features

For instance, the following namespaces are good examples of that guideline.

```csharp
AvivaSolutions.Commerce.Web
NHibernate.Extensibility
Microsoft.ServiceModel.WebApi
Microsoft.VisualStudio.Debugging
FluentAssertion.Primitives
CaliburnMicro.Extensions
```

**Note:** Never allow namespaces to contain the name of a type, but a noun in its plural form (e.g. `Collections`) is usually OK.

### AV1735: Use a verb or verb phrase to name an event

Name events with a verb or a verb phrase. For example: `Click`, `Deleted`, `Closing`, `Minimizing`, and `Arriving`. For example, the declaration of the `Search` event may look like this:

```csharp
public event EventHandler<SearchArgs> Search;
```

### AV1737: Use `-ing` and `-ed` to express pre-events and post-events

For example, a close event that is raised before a window is closed would be called `Closing`, and one that is raised after the window is closed would be called `Closed`. Don't use `Before` or `After` prefixes or suffixes to indicate pre and post events.

Suppose you want to define events related to the deletion of an object. Avoid defining the `Deleting` and `Deleted` events as `BeginDelete` and `EndDelete`. Define those events as follows:

- `Deleting`: Occurs just before the object is getting deleted.
- `Delete`: Occurs when the object needs to be deleted by the event handler.
- `Deleted`: Occurs when the object is already deleted.

### AV1738: Prefix an event handler with "On"

It is good practice to prefix the method that handles an event with "On". For example, a method that handles its own `Closing` event should be named `OnClosing`. And a method that handles the `Click` event of its `okButton` field should be named `OkButtonOnClick`.

### AV1739: Use an underscore for irrelevant lambda parameters

If you use a lambda expression (for instance, to subscribe to an event) and the actual parameters of the event are irrelevant, use the following convention to make that explicit:

```csharp
button.Click += (_, __) => HandleClick();
```

**Note** If using C# 9 or higher, use a single underscore (discard) for all unused lambda parameters and variables.

### AV1745: Group extension methods in a class suffixed with Extensions

If the name of an extension method conflicts with another member or extension method, you must prefix the call with the class name. Having them in a dedicated class with the `Extensions` suffix improves readability.

### AV1755: Postfix asynchronous methods with `Async` or `TaskAsync`

The general convention for methods and local functions that return `Task` or `Task<TResult>` is to postfix them with `Async`. But if such a method already exists, use `TaskAsync` instead.

## Performance Guidelines

### AV1800: Consider using `Any()` to determine whether an `IEnumerable<T>` is empty

When a member or local function returns an `IEnumerable<T>` or other collection class that does not expose a `Count` property, use the `Any()` extension method rather than `Count()` to determine whether the collection contains items. If you do use `Count()`, you risk that iterating over the entire collection might have a significant impact (such as when it really is an `IQueryable<T>` to a persistent store).

**Note:** If you return an `IEnumerable<T>` to prevent changes from calling code as explained in [AV1130](#av1130-return-an-ienumerablet-or-icollectiont-instead-of-a-concrete-collection-class), and you're developing in .NET 4.5 or higher, consider the new read-only classes.

### AV1820: Only use `async` for low-intensive long-running activities

The usage of `async` won't automagically run something on a worker thread like `Task.Run` does. It just adds the necessary logic to allow releasing the current thread, and marshal the result back on that same thread if a long-running asynchronous operation has completed. In other words, use `async` only for I/O bound operations.

### AV1825: Prefer `Task.Run` or `Task.Factory.StartNew` for CPU-intensive activities

If you do need to execute a CPU bound operation, use `Task.Run` to offload the work to a thread from the Thread Pool. For long-running operations use `Task.Factory.StartNew` with `TaskCreationOptions.LongRunning` parameter to create a new thread. Remember that you have to marshal the result back to your main thread manually.

### AV1830: Beware of mixing up `async`/`await` with `Task.Wait`

`await` does not block the current thread but simply instructs the compiler to generate a state-machine. However, `Task.Wait` blocks the thread and may even cause deadlocks (see [AV1835](#av1835-beware-of-asyncawait-deadlocks-in-single-threaded-environments)).

### AV1835: Beware of `async`/`await` deadlocks in special environments (e.g. WPF)

Consider the following asynchronous method:

```csharp
private async Task<string> GetDataAsync()
{
    var result = await MyWebService.GetDataAsync();
    return result.ToString();
}
```

Now when a button event handler is implemented like this:

```csharp
public async void Button1_Click(object sender, RoutedEventArgs e)
{
    var data = GetDataAsync().Result;
    textBox1.Text = data;
}
```

You will likely end up with a deadlock. Why? Because the `Result` property getter will block until the `async` operation has completed, but since an `async` method _could_ automatically marshal the result back to the original thread (depending on the current `SynchronizationContext` or `TaskScheduler`) and WPF uses a single-threaded synchronization context, they'll be waiting on each other. A similar problem can also happen on UWP, WinForms, classical ASP.NET (not ASP.NET Core) or a Windows Store C#/XAML app. Read more about this [here](https://devblogs.microsoft.com/pfxteam/await-and-ui-and-deadlocks-oh-my/).

### AV1840: Await `ValueTask` and `ValueTask<T>` directly and exactly once

The consumption of the newer and performance related `ValueTask` and `ValueTask<T>` types is more restrictive than consuming `Task` or `Task<T>`. Starting with .NET Core 2.1 the `ValueTask<T>` is not only able to wrap the result `T` or a `Task<T>`, with this version it is also possible to wrap a `IValueTaskSource` / `IValueTaskSource<T>` which gives the developer extra support for reuse and pooling. This enhanced support might lead to unwanted side-effects, as the ValueTask-returning developer might reuse the underlying object after it got awaited. The safest way to consume a `ValueTask` / `ValueTask<T>` is to directly `await` it once, or call `.AsTask()` to get a `Task` / `Task<T>` to overcome these limitations.

```csharp
// OK / GOOD
int bytesRead = await stream.ReadAsync(buffer, cancellationToken);

// OK / GOOD
int bytesRead = await stream.ReadAsync(buffer, cancellationToken).ConfigureAwait(false);

// OK / GOOD - Get task if you want to overcome the limitations exposed by ValueTask / ValueTask<T>
Task<int> task = stream.ReadAsync(buffer, cancellationToken).AsTask();
```

Other usage patterns might still work (like saving the `ValueTask` / `ValueTask<T>` into a variable and awaiting later), but may lead to misuse eventually. Not awaiting a `ValueTask` / `ValueTask<T>` may also cause unwanted side-effects. Read more about `ValueTask` / `ValueTask<T>` and the correct usage [here](https://devblogs.microsoft.com/dotnet/understanding-the-whys-whats-and-whens-of-valuetask/).


## Framework Guidelines

### AV2201: Use C# type aliases instead of the types from the `System` namespace

For instance, use `object` instead of `Object`, `string` instead of `String`, and `int` instead of `Int32`. These aliases have been introduced to make the primitive types first class citizens of the C# language, so use them accordingly. When referring to static members of those types, use `int.Parse()` instead of `Int32.Parse()`.

**Exception:** For interop with other languages, it is custom to use the [CLS-compliant name](https://docs.microsoft.com/en-us/dotnet/standard/common-type-system) in type and member signatures, e.g. `HexToInt32Converter`, `GetUInt16`.

### AV2202: Prefer language syntax over explicit calls to underlying implementations

Language syntax makes code more concise. The abstractions make later refactorings easier (and sometimes allow for extra optimizations).

Prefer:

```csharp
(string, int) tuple = ("", 1);
```

rather than:

```csharp
ValueTuple<string, int> tuple = new ValueTuple<string, int>("", 1);
```

Prefer:

```csharp
DateTime? startDate;
```

rather than:

```csharp
Nullable<DateTime> startDate;
```

Prefer:

```csharp
if (startDate != null) ...
```

rather than:

```csharp
if (startDate.HasValue) ...
```

Prefer:

```csharp
if (startDate > DateTime.Now) ...
```

rather than:

```csharp
if (startDate.HasValue && startDate.Value > DateTime.Now) ...
```

Prefer:

```csharp
(DateTime startTime, TimeSpan duration) tuple1 = GetTimeRange();
(DateTime startTime, TimeSpan duration) tuple2 = GetTimeRange();

if (tuple1 == tuple2) ...
```

rather than:

```csharp
if (tuple1.startTime == tuple2.startTime && tuple1.duration == tuple2.duration) ...
```

### AV2207: Don't hard-code strings that change based on the deployment

Examples include connection strings, server addresses, etc. Use `Resources`, the `ConnectionStrings` property of the `ConfigurationManager` class, or the `Settings` class generated by Visual Studio. Maintain the actual values into the `app.config` or `web.config` (and most definitely not in a custom configuration store).

### AV2210: Build with the highest warning level

Configure the development environment to use the highest available warning level for the C# compiler, and enable the option **Treat warnings as errors**. This allows the compiler to enforce the highest possible code quality.

### AV2220: Avoid LINQ query syntax for simple expressions

Rather than:

```csharp
var query = from item in items where item.Length > 0 select item;
```

prefer the use of extension methods from the `System.Linq` namespace:

```csharp
var query = items.Where(item => item.Length > 0);
```

The second example is a bit less convoluted.

### AV2221: Use lambda expressions instead of anonymous methods

Lambda expressions provide a more elegant alternative for anonymous methods. So instead of:

```csharp
Customer customer = Array.Find(customers, delegate(Customer customer)
{
    return customer.Name == "Tom";
});
```

use a lambda expression:

```csharp
Customer customer = Array.Find(customers, customer => customer.Name == "Tom");
```

Or even better:

```csharp
var customer = customers.FirstOrDefault(customer => customer.Name == "Tom");
```

### AV2230: Only use the `dynamic` keyword when talking to a dynamic object

The `dynamic` keyword has been introduced for interop with languages where properties and methods can appear and disappear at runtime. Using it can introduce a serious performance bottleneck, because various compile-time checks (such as overload resolution) need to happen at runtime, again and again on each invocation. You'll get better performance using cached reflection lookups, `Activator.CreateInstance()` or pre-compiled expressions (see [here](https://andrewlock.net/benchmarking-4-reflection-methods-for-calling-a-constructor-in-dotnet/) for examples and benchmark results).

While using `dynamic` may improve code readability, try to avoid it in library code (especially in hot code paths). However, keep things in perspective: we're talking microseconds here, so perhaps you'll gain more by optimizing your SQL statements first.

### AV2235: Favor `async`/`await` over `Task` continuations

Using the new C# 5.0 keywords results in code that can still be read sequentially and also improves maintainability a lot, even if you need to chain multiple asynchronous operations. For example, rather than defining your method like this:

```csharp
public Task<Data> GetDataAsync()
{
    return MyWebService.FetchDataAsync()
      .ContinueWith(t => new Data(t.Result));
}
```

define it like this:

```csharp
public async Task<Data> GetDataAsync()
{
    string result = await MyWebService.FetchDataAsync();
    return new Data(result);
}
```

**Tip:** Even if you need to target .NET Framework 4.0 you can use the `async` and `await` keywords. Simply install the [Async Targeting Pack](http://www.microsoft.com/en-us/download/details.aspx?id=29576).

## Documentation Guidelines

### AV2301: Write comments and documentation in US English

### AV2305: Document all `public`, `protected` and `internal` types and members

Documenting your code allows Visual Studio, [Visual Studio Code](https://code.visualstudio.com/) or [Jetbrains Rider](https://www.jetbrains.com/rider/) to pop-up the documentation when your class is used somewhere else. Furthermore, by properly documenting your classes, tools can generate professionally looking class documentation.

### AV2306: Write XML documentation with other developers in mind

Write the documentation of your type with other developers in mind. Assume they will not have access to the source code and try to explain how to get the most out of the functionality of your type.

### AV2307: Write MSDN-style documentation

Following the MSDN online help style and word choice helps developers find their way through your documentation more easily.

### AV2310: Avoid inline comments

If you feel the need to explain a block of code using a comment, consider replacing that block with a method with a clear name.

### AV2316: Only write comments to explain complex algorithms or decisions

Try to focus comments on the *why* and *what* of a code block and not the *how*. Avoid explaining the statements in words, but instead help the reader understand why you chose a certain solution or algorithm and what you are trying to achieve. If applicable, also mention that you chose an alternative solution because you ran into a problem with the obvious solution.

### AV2318: Don't use comments for tracking work to be done later

Annotating a block of code or some work to be done using a *TODO* or similar comment may seem a reasonable way of tracking work-to-be-done. But in reality, nobody really searches for comments like that. Use a work item tracking system to keep track of leftovers.

## Layout Guidelines

### DG2400: Use a common layout

- Keep the length of each line under 130 characters.

- Use an indentation of 4 spaces, and don't use tabs

- Keep one space between keywords like `if` and the expression, but don't add spaces after `(` and before `)` such as: `if (condition == null)`.

- Add a space around operators like `+`, `-`, `==`, etc.

- Always put opening and closing curly braces on a new line. Exception: auto-properties.

- Don't indent object/collection initializers and initialize each property on a new line, so use a format like this:

```csharp
var dto = new ConsumerDto
{
    Id = 123,
    Name = "Microsoft",
    PartnerShip = PartnerShip.Gold,
    ShoppingCart =
    {
        ["VisualStudio"] = 1
    }
};
```

- Don't indent lambda statement blocks and use a format like this:

```csharp
methodThatTakesAnAction.Do(x =>
{ 
    // do something like this 
}
```

- Keep expression-bodied-members on one line. Break long lines after the arrow sign, like this:

```csharp
private string GetLongText =>
    "ABC ABC ABC ABC ABC ABC ABC ABC ABC ABC ABC ABC ABC ABC ABC ABC ABC ABC ABC ABC ABC";
```

- Put the entire LINQ statement on one line, or start each keyword at the same indentation, like this:

```csharp
var query = from product in products where product.Price > 10 select product;
```

or

```csharp
var query =  
    from product in products  
    where product.Price > 10  
    select product;
```

- Start the LINQ statement with all the `from` expressions and don't interweave them with restrictions.

- Remove redundant parentheses in expressions if they do not clarify precedence. Add parentheses in expressions to avoid non-obvious precedence. For example, in nested conditional expressions: `overruled || (enabled && active)`, bitwise and shift operations: `foo | (bar >> size)`.

- Add an empty line between multi-line statements, between multi-line members, after the closing curly braces, between unrelated code blocks, and between the `using` statements of different root namespaces.

### DG2402: Order namespaces in alphabetic order

```csharp
using AvivaSolutions.Business;
using AvivaSolutions.Standard;
using System;
using System.Collections.Generic;
using System.Xml;
using Telerik.WebControls;
using Telerik.Ajax;
```

Using static directives and using alias directives should be written below regular using directives.
Always place these directives at the top of the file, before any namespace declarations (not inside them).

### DG2406: Place members in a well-defined order

Maintaining a common order allows other team members to find their way in your code more easily. In general, a source file should be readable from top to bottom, as if reading a book, to prevent readers from having to browse up and down through the code file.

1. Public Delegates, Enums
2. Static fields and constants
3. Events
4. Fields
5. Properties, Indexers
6. Constructors and the finalizer
7. All other members in calling order
8. Nested Types

Declare local functions at the bottom of their containing method bodies (after all executable code).

### AV2407:  Do not use `#region`

Regions require extra work without increasing the quality or the readability of code. Instead they make code harder to view and refactor.

### AV2410: Use expression-bodied members appropriately

Favor expression-bodied member syntax over regular member syntax only when:

- the body consists of a single statement and
- the body fits on a single line.

## About this document

### Useful links

In addition to the many links provided throughout this document, I'd like to recommend the following books, articles and sites for everyone interested in software quality:

- [Code Complete: A Practical Handbook of Software Construction](http://www.amazon.com/Code-Complete-Practical-Handbook-Construction/dp/0735619670) (Steve McConnel)  
One of the best books I've ever read. It deals with all aspects of software development, and even though the book was originally written in 2004 you'll be surprised when you see how accurate it still is. I wrote a [review](http://www.continuousimprover.com/2009/07/book-review-code-complete-2nd-edition.html) in 2009 if you want to get a sense of its contents.

- [The Art of Agile Development](http://www.amazon.com/Art-Agile-Development-James-Shore/dp/0596527675) (James Shore)  
Another great all-encompassing trip through the many practices preached by processes like Scrum and Extreme Programming. If you're looking for a quick introduction with a pragmatic touch, make sure you read James's book.

- [Applying Domain-Driven Design and Patterns: With Examples in C# and .NET](http://www.amazon.com/Applying-Domain-Driven-Design-Patterns-Examples/dp/0321268202) (Jimmy Nilsson)  
The book that started my interest for both Domain-Driven Design and Test-Driven Development. It's one of those books that I wished I had read a few years earlier. It would have spared me from many mistakes.

- [Jeremy D. Miller's Blog](https://jeremydmiller.com/)
Jeremy has written some excellent blog posts on Test-Driven Development, Design Patterns and design principles. I've learned a lot from his real-life and practical insights.

- [LINQ Framework Design Guidelines](https://blogs.msdn.microsoft.com/mirceat/2008/03/12/linq-framework-design-guidelines/)  
A set of rules and recommendations that you should adhere to when creating your own implementations of `IQueryable`.

- [Guidance on Asynchronous Programming](https://github.com/davidfowl/AspNetCoreDiagnosticScenarios/blob/master/AsyncGuidance.md) (David Fowler)
Best practices for `async`/`await` with examples of bad and good patterns of how to write asynchronous code.

- [Best Practices for c# async/await](https://msdn.microsoft.com/en-us/magazine/jj991977.aspx)  
Older (but still valid) overview of crucial practices to follow when adopting `async` and `await` in your own code base.

### What is this

This document attempts to provide guidelines (or coding standards if you like) for all versions of C# up to and including v10 that are both valuable and pragmatic. Of course, if you create such a document you should practice what you preach. So rest assured, these guidelines are representative to what we at [Aviva Solutions](https://www.avivasolutions.nl) do in our day-to-day work. Notice that not all guidelines have a clear rationale. Some of them are simply choices we made at Aviva Solutions. In the end, it doesn't matter what choice you made, as long as you make one and apply it consistently.

These guidelines are based on: <https://csharpcodingguidelines.com/> by Dennis Doomen of Aviva solutions. Most of the rules are kept as is, but some are updated.

### What is different compared to Aviva / CSharpGuidelines

Some rules have been changed to match personal preferences. I renamed the rule code to be prefixed with DG instead of AV to avoid confusion.

- AV1225: Removed
- AV1230: Removed
- AV1535: 1. Added exception for `case` with `return`. 2. Added note for `using`. (now DG1535)
- AV1702: All private fields are now Camel (now DG1702)
- AV2400: Added exception for auto-property newlines. (now DG2400)
- AV2402: Order all namespaces alphabetically, not System first. (now DG2402)
- AV2406: Ordered the default Resharper way. (now DG2406)

### Why would you use this document

Although some might see coding guidelines as undesired overhead or something that limits creativity, this approach has already proven its value for many years. This is because not every developer:

- is aware that code is generally read 10 times more than it is changed.
- is aware of the potential pitfalls of certain constructs in C#.
- is up to speed on certain conventions when using the .NET Framework such as `IDisposable`, `async`/`await`, or the deferred execution nature of LINQ.
- is aware of the impact of using (or neglecting to use) particular solutions on aspects like security, performance, multi-language support, etc.
- realizes that not every developer is as capable, skilled or experienced to understand elegant, but potentially very abstract solutions.

### Basic principles

There are many unexpected things I run into during my work as a consultant, each deserving at least one guideline. Unfortunately, I still need to keep this document within a reasonable size. But unlike what some junior developers believe, that doesn't mean that something is okay just because it is not mentioned in this document.

In general, if I have a discussion with a colleague about a smell that this document does not cover, I'll refer back to a set of basic principles that apply to all situations, regardless of context. These include:

- The Principle of Least Surprise (or Astonishment): you should choose a solution that everyone can understand, and that keeps them on the right track.
- Keep It Simple Stupid (a.k.a. KISS): the simplest solution is more than sufficient.
- You Ain't Gonna Need It (a.k.a. YAGNI): create a solution for the problem at hand, not for the ones you think may happen later on. Can you predict the future?
- Don't Repeat Yourself (a.k.a. DRY): avoid duplication within a component, a source control repository or  a [bounded context](http://martinfowler.com/bliki/BoundedContext.html), without forgetting the [Rule of Three](http://lostechies.com/derickbailey/2012/10/31/abstraction-the-rule-of-three/) heuristic.
- The [four principles of object-oriented programming](https://github.com/TelerikAcademy/Object-Oriented-Programming/tree/master/Topics/04.%20OOP-Principles-Part-1): encapsulation, abstraction, inheritance and polymorphism.
- In general, generated code should not need to comply with coding guidelines. However, if it is possible to modify the templates used for generation, try to make them generate code that complies as much as possible.

Regardless of the elegance of someone's solution, if it's too complex for the ordinary developer, exposes unusual behavior, or tries to solve many possible future issues, it is very likely the wrong solution and needs redesign. The worst response a developer can give you to these principles is: "But it works?".

### How do you get started

- Ask all developers to carefully read this document at least once. This will give them a sense of the kind of guidelines the document contains.
- Make sure there are always a few hard copies of the [Cheat Sheet](https://github.com/dennisdoomen/CSharpGuidelines/releases/latest) close at hand.
- Include the most critical coding guidelines on your [Project Checklist](https://www.continuousimprover.com/2010/03/alm-practices-5-checklists.html) and verify the remainder as part of your [Peer Review](https://www.continuousimprover.com/2010/02/tfs-development-practices-part-2-peer.html).
- Jetbrain's [ReSharper](http://www.jetbrains.com/resharper/) and their fully fledged Visual Studio replacement [Rider](https://www.jetbrains.com/rider/), has an intelligent code inspection engine that, with some configuration, already supports many aspects of the Coding Guidelines. It automatically highlights any code that does not match the rules for naming members (e.g. Pascal or Camel casing), detects dead code, and many other things. One click of the mouse button (or the corresponding keyboard shortcut) is usually enough to fix it.
- ReSharper also has a File Structure window that displays an overview of the members of your class or interface, and allows you to easily rearrange them using a simple drag-and-drop action.
- [CSharpGuidelinesAnalyzer](https://github.com/bkoelman/CSharpGuidelinesAnalyzer) verifies over 40 of our guidelines, while typing code in Visual Studio 2017-2022 and during CI builds. An updated Resharper settings file is included.

### Why did Dennis Doomen create it

The idea started in 2002 when Vic Hartog (Philips Medical Systems) and I were assigned the task of writing up a [coding standard](http://www.tiobe.com/content/paperinfo/gemrcsharpcs.pdf) for C# 1.0. Since then, I've regularly added, removed and changed rules based on experiences, feedback from the community and new tooling support offered by a continuous stream of new developments in the .NET ecosystem. Special thanks go to [Bart Koelman](https://github.com/bkoelman) for being a very active contributor over all those years.

Additionally, after reading [Robert C. Martin](https://sites.google.com/site/unclebobconsultingllc/)'s book [Clean Code: A Handbook of Agile Software Craftsmanship](http://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882), I became a big fan of his ideas and decided to include some of his smells and heuristics as guidelines. Notice though, that this document is in no way a replacement for his book. I sincerely recommend that you read his book to gain a solid understanding of the rationale behind his recommendations.

I've also decided to include some design guidelines in addition to simple coding guidelines. They are too important to ignore and have a big influence in reaching high quality code.

### Is this a coding standard

The document does not state that projects must comply with these guidelines, neither does it say which guidelines are more important than others. However, we encourage projects to decide themselves which guidelines are important, what deviations a project will use, who is the consultant in case doubts arise, and what kind of layout must be used for source code. Obviously, you should make these decisions before starting the real coding work.

### Feedback and disclaimer

This document has been compiled using many contributions from community members, blog posts, on-line discussions and two decades of developing in C#. If you have questions, comments or suggestions, just let me know by sending me an email at [dennis.doomen@avivasolutions.nl](mailto:dennis.doomen@avivasolutions.nl), [creating an issue](https://github.com/dennisdoomen/csharpguidelines/issues) or Pull Request on GitHub, ping me at [http://twitter.com/ddoomen](http://twitter.com/ddoomen) or join the [Gitter discussions](https://gitter.im/dennisdoomen/CSharpGuidelines). I will try to revise and republish this document with new insights, experiences and remarks on a regular basis.

Notice though that it merely reflects my view on proper C# code so Aviva Solutions will not be liable for any direct or indirect damages caused by applying the guidelines of this document. This document is published under a Creative Commons license, specifically the [Creative Commons Attribution-ShareAlike 4.0](http://creativecommons.org/licenses/by-sa/4.0/) license.

### Can I create my own version

Absolutely. The corresponding [license](https://github.com/dennisdoomen/CSharpGuidelines/blob/master/LICENSE.md) allows you to [fork](https://github.com/dennisdoomen/csharpguidelines/fork), adapt and distribute that modified version within your organization as long as you refer back to the original version here. It's not required, but you would make me a very happy man if you credit me as the original author. And if you have any great ideas, recommendations or corrections, either submit an issue, or even better, fork the repository and provide me with a pull request.
