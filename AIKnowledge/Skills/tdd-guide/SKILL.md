---
name: "tdd-guide"
description: "Provides Test-Driven Development guidance and best practices. Invoke when user needs help with TDD methodology, test writing, or test-first development workflows."
---

# TDD Guide

## Overview

TDD Guide is a comprehensive skill for Test-Driven Development methodology, providing guidance, best practices, and practical examples for writing tests before code.

## Features

- **TDD Methodology**: Complete guide to test-first development
- **Test Writing**: Best practices for writing effective tests
- **Test Patterns**: Common testing patterns and anti-patterns
- **Refactoring Guidance**: Safe refactoring with test coverage
- **Test Frameworks**: Support for various testing frameworks
- **Code Coverage**: Strategies for achieving good test coverage

## When to Use

Invoke this skill when:

- You want to learn or apply TDD methodology
- You need help writing effective tests
- You're starting a new feature and want to follow test-first approach
- You need guidance on test structure and organization
- You want to improve code quality through testing
- You need help with refactoring legacy code safely

## The TDD Cycle

### Red-Green-Refactor

```
1. RED    - Write a failing test
2. GREEN  - Write minimal code to pass the test
3. REFACTOR - Improve code while keeping tests green
```

### Detailed Steps

1. **Add a test**: Write a test for the next small piece of functionality
2. **Run all tests**: The new test should fail (RED)
3. **Write code**: Write just enough code to make the test pass
4. **Run tests**: All tests should pass (GREEN)
5. **Refactor**: Clean up the code while keeping tests passing
6. **Repeat**: Continue with the next test

## Test Structure

### AAA Pattern

```javascript
// Arrange - Set up test data and conditions
const input = 5;
const expected = 10;

// Act - Execute the code being tested
const result = double(input);

// Assert - Verify the outcome
expect(result).toBe(expected);
```

### Test Naming Convention

```
should_[expected behavior]_when_[condition]

Examples:
- should_return_empty_array_when_list_is_empty
- should_throw_exception_when_input_is_null
- should_calculate_total_correctly_when_items_added
```

## Best Practices

### Test Quality

- **One assertion per test**: Each test should verify one thing
- **Keep tests simple**: Tests should be easy to understand
- **Test behavior, not implementation**: Focus on what, not how
- **Use descriptive names**: Test names should document expected behavior
- **Keep tests independent**: Tests should not depend on each other
- **Make tests fast**: Fast tests encourage running them often

### TDD Principles

- **Write tests first**: Always write the test before the code
- **Write minimal code**: Only write code to pass the current test
- **Refactor continuously**: Keep code clean throughout the process
- **Small steps**: Make small, incremental changes
- **Green bar addiction**: Always keep the test suite passing

## Test Types

### Unit Tests

- Test individual functions or methods
- Mock external dependencies
- Fast and isolated
- High coverage target: 80%+

### Integration Tests

- Test interaction between components
- Verify API contracts
- Test database interactions
- Slower than unit tests

### Acceptance Tests

- Test from user perspective
- Verify business requirements
- End-to-end scenarios
- Slowest but most valuable

## Common Patterns

### Arrange-Act-Assert

```python
def test_add_item_to_cart():
    # Arrange
    cart = ShoppingCart()
    item = Item("Book", 29.99)
    
    # Act
    cart.add(item)
    
    # Assert
    assert cart.item_count == 1
    assert cart.total == 29.99
```

### Test Doubles

```javascript
// Mock - Verify interactions
const mockService = {
  save: jest.fn().mockResolvedValue(true)
};

// Stub - Provide canned responses
const stubConfig = {
  get: () => 'test-value'
};

// Fake - Working implementation for testing
class FakeRepository {
  constructor() { this.items = []; }
  save(item) { this.items.push(item); }
  find(id) { return this.items.find(i => i.id === id); }
}
```

### Parameterized Tests

```java
@ParameterizedTest
@ValueSource(ints = {1, 2, 3, 4, 5})
void should_handle_multiple_inputs(int value) {
    assertTrue(isValid(value));
}
```

## Refactoring with TDD

### Safe Refactoring Steps

1. Ensure all tests pass
2. Make small refactoring changes
3. Run tests frequently
4. If tests fail, revert and try again
5. Commit when refactoring is complete

### Common Refactorings

- Extract Method
- Rename Variable/Method
- Move Method/Class
- Replace Conditional with Polymorphism
- Introduce Null Object

## Test Frameworks

### JavaScript/TypeScript

- Jest
- Mocha + Chai
- Jasmine
- Vitest

### Python

- pytest
- unittest
- nose2

### Java

- JUnit
- TestNG
- Mockito

### C#

- xUnit
- NUnit
- MSTest

## Getting Started

### Step-by-Step Guide

1. **Choose a test framework** for your language
2. **Set up test project** structure
3. **Write your first test** (expect it to fail)
4. **Implement minimal code** to pass
5. **Refactor** while keeping tests green
6. **Repeat** for each new feature

### Example Workflow

```
// 1. Write failing test
test('should return sum of two numbers', () => {
  expect(add(2, 3)).toBe(5);
});

// 2. Run test - RED (fails)

// 3. Implement code
function add(a, b) {
  return a + b;
}

// 4. Run test - GREEN (passes)

// 5. Refactor (if needed)

// 6. Add more tests
test('should handle negative numbers', () => {
  expect(add(-1, 1)).toBe(0);
});
```

## Common Mistakes

- Writing too much code before testing
- Testing implementation instead of behavior
- Making tests too complex
- Not running tests frequently
- Skipping refactoring step
- Writing tests after code (not TDD)

## Resources

- **Books**: 
  - "Test-Driven Development: By Example" by Kent Beck
  - "Growing Object-Oriented Software, Guided by Tests"
- **Websites**:
  - [testdriven.io](https://testdriven.io)
  - [martinfowler.com/bliki/TestDrivenDevelopment.html](https://martinfowler.com/bliki/TestDrivenDevelopment.html)

## Contributing

To contribute to this skill or suggest improvements, please visit the GitHub repository or community forum.

## License

This skill is provided under the MIT License.