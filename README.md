# Git Workshop: Collaborative Calculator App

## Overview
This workshop uses a simple Java calculator project to practice essential Git and GitHub workflows including:
- Creating and using branches
- Making commits with semantic commit messages
- Creating and merging Pull Requests
- Handling merge conflicts
- Rebasing branches

## Setup Instructions
#### Person A:
1. Open GitHub and fork the instructor's repository
2. Clone your fork to your local machine:
   ```bash
   git clone https://github.com/your-username/calculator-app.git
   cd calculator-app
   ```
3. Verify remote URL:
   ```bash
   git remote -v
   ```

#### Person B:
1. Collaborate with Person A by cloning their repository:
   ```bash
   git clone https://github.com/personA-username/calculator-app.git
   cd calculator-app
   ```

## Workshop Activities

### 1. Working with Branches

#### Person A:
##### Create a new branch for subtraction feature
```bash
git checkout -b feature/subtract
```
##### Add subtraction functionality to Calculator.java
```bash
echo 'package com.workshop.calculator;

public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
    
    public int subtract(int a, int b) {
        return a - b;
    }
    
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        System.out.println("2 + 3 = " + calc.add(2, 3));
        System.out.println("5 - 2 = " + calc.subtract(5, 2));
    }
}' > src/main/java/com/workshop/calculator/Calculator.java
```
##### Commit and push changes
```bash
git add .
git commit -m "feat: add subtraction functionality"
git push origin feature/subtract
```

#### Person B:
##### Create a new branch for multiplication feature
```bash
git checkout -b feature/multiply
```
##### Add multiplication functionality to Calculator.java
```bash
echo 'package com.workshop.calculator;

public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
    
    public int multiply(int a, int b) {
        return a * b;
    }
    
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        System.out.println("2 + 3 = " + calc.add(2, 3));
        System.out.println("2 * 3 = " + calc.multiply(2, 3));
    }
}' > src/main/java/com/workshop/calculator/Calculator.java
```

##### Commit and push changes
```bash
git add src/main/java/com/workshop/calculator/Calculator.java
git commit -m "feat: add multiplication functionality"
git push origin feature/multiply
```

### 2. Creating Pull Requests

Both participants should:
1. Go to the repository on GitHub
2. Click on "Pull requests" > "New pull request"
3. Select your feature branch to merge into main
4. Add an appropriate title and description
5. Create the pull request

### 3. Merging and Handling Conflicts

#### As A, Review and Merge Person B's PR First:
1. Review the PR from Person B (feature/multiply)
2. Click "Merge pull request" > "Create merge commit"
3. Confirm the merge

#### Person A Updates Their Branch:
```bash
# Update local main branch
git checkout main
git pull origin main

# Switch to feature branch and rebase
git checkout feature/subtract
git rebase main

# Resolve any conflicts in Calculator.java
# After resolving conflicts:
git add .
git rebase --continue

# Push updated branch (requires force push)
git push -f origin feature/subtract
```

#### As B, Review and Merge Person A's PR:
1. Review the updated PR from Person A
2. Click "Merge pull request" > "Create merge commit"
3. Confirm the merge

### 4. Adding Another Feature

#### Person B:
```bash
# Update local main branch
git checkout main
git pull origin main

# Create new branch for division feature
git checkout -b feature/divide

# Add division functionality
echo 'package com.workshop.calculator;

public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
    
    public int subtract(int a, int b) {
        return a - b;
    }
    
    public int multiply(int a, int b) {
        return a * b;
    }
    
    public int divide(int a, int b) {
        if (b == 0) {
            throw new ArithmeticException("Cannot divide by zero");
        }
        return a / b;
    }
    
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        System.out.println("2 + 3 = " + calc.add(2, 3));
        System.out.println("5 - 2 = " + calc.subtract(5, 2));
        System.out.println("2 * 3 = " + calc.multiply(2, 3));
        System.out.println("6 / 2 = " + calc.divide(6, 2));
    }
}' > src/main/java/com/workshop/calculator/Calculator.java

# Commit and push changes
git add src/main/java/com/workshop/calculator/Calculator.java
git commit -m "feat: add division functionality with zero check"
git push origin feature/divide
```

### 5. Tagging a Release

After merging all features:

```bash
# Make sure you're on main and up-to-date
git checkout main
git pull origin main

# Create an annotated tag
git tag -a v1.0.0 -m "First release with basic arithmetic operations"
git push origin v1.0.0
```

## Concepts Covered

- **Git Branching**: Creating isolated workspaces for feature development
- **Semantic Commits**: Using descriptive commit messages with types (feat, fix, etc.)
- **Pull Requests**: Reviewing and discussing code changes before merging
- **Rebasing**: Integrating changes from one branch to another
- **Conflict Resolution**: Handling conflicting changes between branches
- **Tagging**: Marking specific points in history as important

## References

- [Conventional Commits](https://www.conventionalcommits.org/)
- [GitHub Flow](https://guides.github.com/introduction/flow/)
- [Git Documentation](https://git-scm.com/doc)
