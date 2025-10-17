
# Automated Theorem Generator △1

**User Manual**

---

## System Requirements

- **Operating System**: Windows 10 or later
    
- **Memory**: Minimum 4 GB RAM (8 GB or more recommended)
    
- **Storage**: At least 100 MB of available space
    

---

## Program Overview

The **Automated Theorem Generator** is a tool based on the _Triangle Standard Contradiction Separation_.  
It automatically generates theorems from logical literals provided by the user.  
The program features a graphical user interface, making it simple to operate and suitable for both research and teaching.

---

## Features

- **Literal Parsing**: Parses logical literals such as `p(a)` or `~q(b)`.
    
- **Enhanced Input Validation**: Comprehensive validation system with detailed error reporting:
  - Full-width character detection
  - Parentheses matching verification
  - Predicate name format validation
  - Parameter format validation
  - Specific error messages for each type of validation failure
    
- **Automated Literals Generation**: Generates test literals automatically:
  - Customizable number of literals (2-100)
  - Random predicate generation with unique names
  - Random parameter generation (variables and constants)
  - Random negation assignment
  - Ensures all generated literals follow validation rules
    
- **Input Validation**: Checks whether inputs follow syntax and logical rules.
    
- **Theorem Generation**: Produces of the input literals and generates theorems.
    
- **CNF Output**: Converts results into CNF (Conjunctive Normal Form) compliant with the TPTP format.
    
- **Paging and Browsing**: Allows navigation through theorems generated.
    

---

## Input Rules

### Input Format

Literals must follow propositional logic and first-order logic syntax:

```
Predicate(term1, term2, ...)
```

- Predicates must begin with a letter; letters, digits, and underscores are allowed.
    
- The terms can be constants (e.g., a, b, c) or variables (e.g., X, Y, Z) or function terms (e.g., f(X,Y),g(X,Y,Z,U)).
    
- Negation is supported: prefix the predicate with `~` (e.g., `~p(a)`).
    
- Compound terms are supported (e.g., `f(a)`, `g(X, Y)`).
    
- Only half-width characters are allowed in the input.

### Examples

```
p(a)
~q(b)
r(f(X))
s(g(a), h(b, c))
~t(f(g(X), Y), Z)
```

### Validation Rules

1. **No Identical Predicate Symbols**
    
    - Invalid: `p(a)` and `p(b)`
        
    - Valid: `p(a)` and `q(b)`
        
2. **No Complementary Predicate Symbols**
    
    - Invalid: `p(a)` and `~p(a)`
        
    - Valid: `p(a)` and `~q(b)`
        
3. **Functions with Consistent Arity**
    
    - Invalid: `f(a)` and `f(a, b)`
        
    - Valid: `f(a)` and `g(a, b)`
        
4. **Enhanced Input Validation**
    
    - **Full-width Character Detection**: Input containing full-width characters will be rejected with a specific error message indicating which literal contains the issue.
    
    - **Parentheses Matching**: Each literal must have balanced parentheses. Unmatched parentheses will result in a specific error message.
    
    - **Predicate Name Format**: Predicate names must start with a lowercase letter. Invalid predicate names will trigger specific error messages.
    
    - **Parameter Format**: Parameters must be non-empty and start with a letter (uppercase for variables, lowercase for constants). Empty or invalid parameters will be identified with precise error messages.

---

## How to Use

### Literal Input

1. Select **"Literal Input"**.
    
2. Enter multiple literals separated by semicolons, e.g.:
    
    ```
    p(a); ~q(b); r(f(X)); s(g(Y), Z)
    ```
    
3. The program automatically parses and validates all inputs, providing detailed error messages if validation fails.
    

### Automated Literals Generation

1. In the **"Literal Input"** section, locate the **"Automated Literals Generator"** button.
    
2. Use the **"Literals Count"** spinner to specify the number of literals to generate (2-100).
    
3. Click **"Automated Literals Generator"** to generate random literals.
    
4. The program will automatically fill the input area with generated literals that:
   - Have unique predicate names
   - Follow proper syntax rules
   - Include random variables (X, Y, Z, etc.) and constants (a, b, c, etc.)
   - Have random negation assignments
   - Pass all validation rules
    
5. A confirmation message will appear showing the number of literals generated.

### Generator Theorems

1. Ensure all inputs are valid.
    
2. Click **"Theorem Generator"**.
    
3. The program produces theorems and outputs CNF clauses.
    
4. Browse results using the paging controls.
    

---

## Paging and Navigation

### Paging Controls

Located at the bottom of the interface:

- **Total Pages**: Displays "Theorem Total: X" (shows "N/A" if input > 10 formulas).
    
- **Page Number Box**: Displays current page; users can enter a number to jump.
    
- **Buttons**:
    
    - `<<` Previous page
        
    - `>>` Next page
        
---

## FAQ

**Q: My input no theorems are generated. What should I do?**

**A:**

- Check for correct syntax (parentheses, commas).
    
- Ensure no full-width characters are present in your input.
    
- Verify predicate names start with lowercase letters.
    
- Ensure parameters are not empty and start with letters.
    
- Ensure rules (no identical predicate symbols, no complementary predicate symbols, same number of variants for function symbols with the same name) are not violated.
    
- Refer to the specific error message provided, which will indicate exactly which literal and what type of error occurred.
    
---
