# Test Directory

This directory contains all tests for the todolist application.

## Structure

- `/unit/` - Unit tests for individual functions and components
- `/integration/` - Integration tests for API routes and complex components
- `/e2e/` - End-to-end tests for critical user flows
- `/coverage/` - Test coverage reports (generated)

## Running Tests

```bash
# Run all tests
npm test

# Run tests in watch mode
npm run test:watch

# Run tests with coverage
npm run test:coverage

# Run specific test file
npm test -- path/to/test.test.ts
```

## Writing Tests

- Use descriptive test names
- Follow the Arrange-Act-Assert pattern
- Mock external dependencies
- Test both success and error cases
- Aim for high coverage but focus on meaningful tests