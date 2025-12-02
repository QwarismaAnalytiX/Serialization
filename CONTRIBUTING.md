# Contributing to Qwarisma AnalytiX Serialization Library

Thank you for your interest in contributing to the Serialization library! This document provides guidelines and information for contributors.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Setup](#development-setup)
- [How to Contribute](#how-to-contribute)
- [Pull Request Process](#pull-request-process)
- [Coding Standards](#coding-standards)
- [Testing Guidelines](#testing-guidelines)
- [Issue Guidelines](#issue-guidelines)

---

## Code of Conduct

### Our Pledge

We are committed to providing a friendly, safe, and welcoming environment for all contributors, regardless of experience level, gender identity, sexual orientation, disability, personal appearance, body size, race, ethnicity, age, religion, or nationality.

### Our Standards

**Examples of behavior that contributes to a positive environment:**

- Using welcoming and inclusive language
- Being respectful of differing viewpoints and experiences
- Gracefully accepting constructive criticism
- Focusing on what is best for the community
- Showing empathy towards other community members

**Examples of unacceptable behavior:**

- Trolling, insulting/derogatory comments, and personal or political attacks
- Public or private harassment
- Publishing others' private information without explicit permission
- Other conduct which could reasonably be considered inappropriate in a professional setting

### Enforcement

Instances of abusive, harassing, or otherwise unacceptable behavior may be reported by contacting the project maintainers at **[qwarismaanalytix@hotmail.com](mailto:qwarismaanalytix@hotmail.com)**. All complaints will be reviewed and investigated promptly and fairly. All reports will be handled with discretion.

---

## Getting Started

### Prerequisites

Before you begin, ensure you have:

- **C++20 compatible compiler**: GCC 11+, Clang 13+, or MSVC 19.29+
- **CMake 3.15** or higher
- **Git** for version control
- A GitHub account

### Understanding the Project

Before contributing, familiarize yourself with:

1. The [README.md](README.md) for project overview and features
2. The codebase structure:
   ```
   Serialization/
   ├── include/              # Main library headers and sources
   │   ├── common/           # Core components (reflection, concepts, macros)
   │   ├── util/             # Utility classes (streams, registry, exports)
   │   └── Testing/          # Test files
   ├── ThirdParty/           # Third-party dependencies (nlohmann/json)
   ├── cmake/                # CMake configuration files
   └── CMakeLists.txt        # Main build configuration
   ```

---

## Development Setup

### 1. Fork and Clone

```bash
# Fork the repository on GitHub, then clone your fork
git clone https://github.com/YOUR_USERNAME/Serialization.git
cd Serialization

# Add upstream remote
git remote add upstream https://github.com/QwarismaAnalytiX/Serialization.git
```

### 2. Build the Project

```bash
# Create build directory
mkdir build && cd build

# Configure with CMake
cmake ..

# Build
cmake --build . --config Debug

# Run tests
ctest --output-on-failure
```

### 3. Keep Your Fork Updated

```bash
git fetch upstream
git checkout main
git merge upstream/main
```

---

## How to Contribute

### Types of Contributions

We welcome:

- 🐛 **Bug fixes** - Help us squash bugs
- ✨ **New features** - Propose and implement new functionality
- 📝 **Documentation** - Improve README, comments, or create tutorials
- 🧪 **Tests** - Add or improve test coverage
- 🎨 **Code quality** - Refactoring, performance improvements
- 🔧 **Build system** - CMake improvements, CI/CD enhancements

### Before You Start

1. **Check existing issues** - See if someone else is already working on it
2. **Open an issue first** - For significant changes, discuss your approach
3. **Create a feature branch** - Never work directly on `main`

---

## Pull Request Process

### 1. Create a Feature Branch

```bash
git checkout -b feature/your-feature-name
# or
git checkout -b fix/bug-description
```

### 2. Make Your Changes

- Write clean, readable code
- Follow the [coding standards](#coding-standards)
- Add/update tests as needed
- Update documentation if applicable

### 3. Test Your Changes

```bash
cd build
cmake --build .
ctest --output-on-failure
```

### 4. Commit Your Changes

Use clear, descriptive commit messages:

```bash
git commit -m "feat: Add support for std::chrono types"
# or
git commit -m "fix: Resolve memory leak in multi_process_stream"
# or
git commit -m "docs: Update installation instructions"
```

**Commit Message Prefixes:**

| Prefix | Description |
|--------|-------------|
| `feat:` | New feature |
| `fix:` | Bug fix |
| `docs:` | Documentation changes |
| `test:` | Adding or updating tests |
| `refactor:` | Code refactoring |
| `perf:` | Performance improvements |
| `chore:` | Build system, CI, or tooling changes |

### 5. Push and Create PR

```bash
git push origin feature/your-feature-name
```

Then open a Pull Request on GitHub with:

- Clear title describing the change
- Description of what and why
- Reference to related issues (e.g., "Fixes #123")
- Screenshots/examples if applicable

### PR Review Checklist

Before requesting review, ensure:

- [ ] Code compiles without warnings
- [ ] All tests pass
- [ ] New code has appropriate test coverage
- [ ] Documentation is updated
- [ ] Code follows project style guidelines
- [ ] Commit messages are clear and descriptive

---

## Coding Standards

### C++ Style Guide

#### General

- Use **C++20** features where appropriate
- Prefer `const` correctness
- Use `auto` for complex types, explicit types for clarity
- Use `constexpr` where possible for compile-time computation

#### Naming Conventions

```cpp
// Classes: PascalCase
class MySerializer {};

// Functions/Methods: snake_case
void process_data();

// Member variables: trailing underscore
int value_;

// Constants: UPPER_SNAKE_CASE
constexpr int MAX_BUFFER_SIZE = 1024;

// Template parameters: PascalCase
template <typename ElementType>
class Container {};

// Concepts: PascalCase
template <typename T>
concept Serializable = requires { ... };
```

#### Code Formatting

- Use **4 spaces** for indentation (no tabs)
- Maximum line length: **100 characters**
- Use braces for all control structures
- Opening brace on same line

```cpp
if (condition) {
    do_something();
} else {
    do_something_else();
}
```

#### Includes

Order includes as follows:

```cpp
// 1. Corresponding header (for .cpp files)
#include "myclass.h"

// 2. C++ standard library
#include <string>
#include <vector>

// 3. Third-party libraries
#include <nlohmann/json.hpp>

// 4. Project headers
#include "common/reflection.h"
#include "util/registry.h"
```

---

## Testing Guidelines

### Writing Tests

- Use **Google Test** framework
- Place tests in `include/Testing/Cxx/`
- Name test files: `*_test.cpp`

### Test Structure

```cpp
#include <gtest/gtest.h>
#include "serialization_impl.h"

class SerializationTest : public ::testing::Test {
protected:
    void SetUp() override {
        // Setup code
    }

    void TearDown() override {
        // Cleanup code
    }
};

TEST_F(SerializationTest, VectorSerialization) {
    std::vector<int> data{1, 2, 3};
    json archive;

    serialization::save(archive, data);

    std::vector<int> loaded;
    serialization::load(archive, loaded);

    EXPECT_EQ(data, loaded);
}
```

### Running Tests

```bash
cd build
ctest --output-on-failure

# Run specific test
./Debug/YourTestName
```

---

## Issue Guidelines

### Reporting Bugs

When reporting bugs, include:

1. **Environment**: OS, compiler, compiler version
2. **Steps to reproduce**: Minimal code example
3. **Expected behavior**: What should happen
4. **Actual behavior**: What actually happens
5. **Error messages**: Full error output

### Feature Requests

When requesting features:

1. **Use case**: Describe the problem you're solving
2. **Proposed solution**: How you envision it working
3. **Alternatives**: Other approaches you've considered
4. **Examples**: Code examples if applicable

### Issue Labels

| Label | Description |
|-------|-------------|
| `bug` | Something isn't working |
| `enhancement` | New feature or improvement |
| `documentation` | Documentation improvements |
| `good first issue` | Good for newcomers |
| `help wanted` | Extra attention needed |

---

## Questions?

If you have questions about contributing:

1. Check existing [issues](https://github.com/QwarismaAnalytiX/Serialization/issues)
2. Open a new issue with the `question` label
3. Email us at [qwarismaanalytix@hotmail.com](mailto:qwarismaanalytix@hotmail.com)

---

**Thank you for contributing to Qwarisma AnalytiX Serialization Library!** 🎉
