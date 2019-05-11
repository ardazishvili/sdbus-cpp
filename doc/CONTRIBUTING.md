Contributing to sdbus-c++
=========================

How can I contribute:
--------------------
// TODO

Branch naming
-------------
* `feature/*` - adding new feature, e.g. `feature/add-support-for-client-async-methods`
* `bugfix/*` - fixing a bug, e.g. `bugfix/fix-memory-leak`
* `refactor/*` - refactoring, e.g. `refactor/introduce-dependency-injection-to-xxx-class-to-support-mocking`
* `doc/*` - adding documentation, diagrams, e.g. `doc/add-doxygen-documentation`
* `test/*` - adding tests, checks, e.g. `test/add-integration-tests-of-xxx-class` 

Style guides:
------------
**Git Commit messages**
* Use the present tense ("Add feature" not "Added feature")
* Use the imperative mood ("Move the cursor to..." not "Moves the cursor to...")
* Capitalize the subject line and limit it to 50 characters or less.
* Do not end the subject with a period.
* Separate subject and body with a blank line
* Wrap the body at 72 characters
* Tell _what and why_ instead of _how_ in body

**C++ style guide**
* Prefer explicit r-value semantics in move-only classes. See `Connection` class constructors for details.
* Classes that have an interface for clients should have factories to create them. Meanwhile, "raw"
  constructors may be used for testing purposes.
* If-else should contain `else` with `assert(false)`. This helps to localize a possible bug later.
* Prefer sdbus-c++ to generic header inclusion order. Rationale: this helps writing self-contained headers,
  as missing, forgotten more-generic includes in other sdbus-c++ headers are not masked, but revealed immediately.
* Use SDBUS_CXX_ for header guard prefix
* Prefer `default` keyword to empty body constructors/destructors
* Use one header file per class interface. Move implementation to dedicated .cpp file
* Use one line for separation
* Opening curly brace in class declaration should be placed on a separate line. Example
```
// Good                    
class Foo                  
{                          
...                        
}

// Bad
class Bar {
...
}                          
```
**Unit tests style guide**
* Use Arrange-Act-Assert idiom in each test
* Prefer atomic test to complex one. Usually, there should be one assertion per test
* Isolate tests, i.e. there have not to be dependencies between them
* Tests should compile and run fast enough. If there are dependencies on slow collaborators, e.g. files,
  they should be mocked.
* Use behavior-oriented approach in test naming. It increases readability and maintainability. Example:
```
// Good
TEST(FooClass, ThrowsAtConstructionIfPreconditionsAreNotMet)
{
...
}

// Bad
TEST(FooClassTest, ConstuctorThrows)
{
...
}
```
* If class interaction is not a key interaction of test prefer to use ON_CALL instead of EXPECT_CALL.
  See [Google test cookbook](https://github.com/google/googletest/blob/master/googlemock/docs/CookBook.md#knowing-when-to-expect)
  for details


