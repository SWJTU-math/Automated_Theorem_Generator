
# Automated Theorem Generator △1

  

**User Manual v1.2.0**

  

---

  

## System Requirements

  

- **Operating System**: Windows 10 or later

- **Memory**: Minimum 4 GB RAM (8 GB or more recommended)

- **Storage**: At least 100 MB of available space

---

  

## Program Overview

  

The **Automated Theorem Generator** is a tool based on the _Triangle Standard Contradiction Separation_.

It can automatically generate theorems from logical literals or formulas provided by users. The program features a graphical user interface, is simple to operate, and is suitable for research, application and teaching.

  

### Version Description

  

- **Δ1 Version**: The **Automated Theorem Generator** is a tool based on the _Triangle Standard Contradiction Separation_, deduction by triangle standard contradiction based on standard extension.

  

---

  

## Features

  

### Dual Input Mode Support

  

1. **Literal Mode**:

- Traditional literal input, such as `p(a);~q(f(X))`

- Supports function terms, such as `f(a), g(X,Y)`

- Outputs CNF (Conjunctive Normal Form) format

  

2. **Formula Mode** - **New Feature**:

- Supports logical formula input in TPTP fof format

- Supports quantifiers: universal quantifier `![X]:` and existential quantifier `?[X]:`

- Supports logical connectives: conjunction `&`, disjunction `|`, implication `=>`, biconditional `<=>`

- Supports complex formula structures, such as `![X]: (p(X) => q(X))`

- Outputs FOF (First-Order Formula) format

  

### Enhanced Input Validation System

  

- **Comprehensive Character Detection**: Automatically detects and prompts for full-width characters

- **Parentheses Matching Verification**: Ensures all parentheses are correctly matched

- **Predicate Format Validation**: Validates predicate names and parameter formats

- **Semantic Validation**: Checks variable binding, predicate arity consistency, etc.

- **Set Validation**: Ensures predicate uniqueness, no complementary pairs, etc.



### Navigation and Export Features

  

- **Paging Navigation**: Supports paginated display of large amounts of results

- **Batch Export**: Supports batch export of theorems to files

- **Custom Naming**: Supports custom export filename prefixes

  

---

  

## Input Rules

  

### Input Mode Switching

  

In the Generator tab of the application, you can switch input modes through the "Input Mode" dropdown menu:

  

- **Literal Mode**: Traditional literal input mode

- **Formula Mode**: New formula input mode

  

### Literal Mode Input Rules

  

#### Input Format

  

Literals must follow propositional logic and first-order logic syntax:

  

```

Predicate(term1, term2, ...)

```

  

- Predicates must begin with a letter; letters, digits, and underscores are allowed

- Terms can be constants (e.g., a, b, c) or variables (e.g., X, Y, Z) or function terms (e.g., f(X,Y), g(X,Y,Z,U))

- Negation is supported: prefix the predicate with `~` (e.g., `~p(a)`)

- Compound terms are supported (e.g., `f(a,g(X,Y))`)

- Only half-width characters are allowed in the input

  

#### Literal Mode Examples

  

```

p(a)

~q(b)

r(f(X))

s(g(a), h(b, c))

~t(f(g(X), Y), Z)

```

  

### Formula Mode Input Rules

  

#### Input Format

  

Formula mode uses TPTP fof (first-order formula) format, supporting the following elements:

  

##### Atomic Formulas

  

```

p(X) # Predicate p with parameter X

q(a, b) # Predicate q with parameters a and b

r(f(X), g(Y)) # Predicate r with function term parameters

```

  

##### Logical Connectives

  

```

~p(X) # Negation

(p(X) & q(Y)) # Conjunction (AND)

(p(X) | q(Y)) # Disjunction (OR)

(p(X) => q(Y)) # Implication

(p(X) <=> q(Y)) # Biconditional

```

  

##### Quantifiers

  

```

![X]: p(X) # Universal quantifier: for all X, p(X) holds

?[Y]: q(Y) # Existential quantifier: there exists Y such that q(Y) holds

![X,Y]: (p(X) & q(Y)) # Multiple variable quantifiers

```

  

##### Compound Formulas

  

```

![X]: (p(X) => q(X)) # Quantifier combined with implication

~(![X]: (p(X) => q(X))) # Negation combined with quantifier

(p(X) & q(Y)) => r(Z) # Conjunction combined with implication

```

  

#### Formula Mode Input Rules

  

1. Use semicolon `;` to separate multiple formulas

2. Variable names in formulas must start with uppercase letters (e.g., X, Y, Z)

3. Constant names and function names must start with lowercase letters (e.g., a, b, f, g)

4. Predicate names must start with lowercase letters (e.g., p, q, r)

5. Use parentheses `()` to indicate formula precedence

6. Use square brackets `[]` to indicate quantifier variable lists

7. Only half-width characters are allowed
   
8. The input first-order closed formulas should be satisfiable
   
9.  Among all input first-order closed formulas, there should not be complementary first-order closed formulas

  

#### Formula Mode Examples

  

```

p(a);![Y]: q(Y) => r(Y);?[Z]: s(Z) | t(Z)

```

  

### Validation Rules

  

#### General Validation Rules

  

1. **At least two formulas/literals must be entered**

2. **No full-width characters allowed**

3. **Parentheses must match**

  

#### Literal Mode Specific Validation Rules

  

1. **No Identical Predicate Symbols**

- Invalid: `p(a)` and `p(b)`

- Valid: `p(a)` and `q(b)`

  

2. **No Complementary Predicate Symbols**

- Invalid: `p(a)` and `~p(a)`

- Valid: `p(a)` and `~q(b)`

  

3. **Function Arity Consistency**

- Invalid: `f(a)` and `f(a, b)`

- Valid: `f(a)` and `g(a, b)`

  

#### Formula Mode Specific Validation Rules

  

1. **Variables must be properly bound**

- Invalid: `p(X) & q(Y)` (if X, Y are not bound by quantifiers)

- Valid: `![X,Y]: (p(X) & q(Y))`

  

2. **Parentheses Matching**

- Invalid: `![X]: p(X`

- Valid: `![X]: p(X)`

  

3. **Correct Quantifier Syntax**

- Invalid: `!X: p(X)`

- Valid: `![X]: p(X)`

  
4. **No Complementary Sub-formulas**

- Invalid: `(Formulas_1 | ~Formulas_1) & ~Formulas_1`

- Valid: `(Formulas_1 | ~Formulas_2) & ~Formulas_3`
  
---

  

## How to Use

  

### Switching Input Modes

  

1. In the "Generator" tab, find the "Input Mode" dropdown menu

2. Select "Literal Mode" or "Formula Mode"

3. The input area and prompt text will update accordingly

  

### Using Literal Mode

  

1. Select **"Literal Mode"**.

2. Enter multiple literals separated by semicolons, for example:

```

p(a); ~q(b); r(f(X)); s(g(Y), Z)

```

3. The program automatically parses and validates all inputs, displaying detailed error messages if validation fails.

  

### Using Formula Mode

  

1. Select **"Formula Mode"**.

2. Enter multiple formulas separated by semicolons, for example:

```

p(X);![Y]: q(Y) => r(Y);?[Z]: s(Z) | t(Z)

```

3. The program automatically parses and validates all inputs, displaying detailed error messages if validation fails.

  

### Automated Input of Literals or Formulas

  

#### Literals

  

1. In "Literal Mode", click the **"Automated Literals Generator"** button.

2. Use the **"Literals Count"** selector to specify the number of literals to generate (2-1000).

3. The program will automatically fill the input area, including:

- Unique predicate names

- Following correct syntax rules

- Including random variables (X, Y, Z, etc.) and constants (a, b, c, etc.)

- Random negation assignments

- Passing all validation rules

  

#### Formulas

  

1. In "Formula Mode", click the **"Automated Formulas Generator"** button.

2. Use the **"Formulas Count"** selector to specify the number of formulas to generate (2-1000).

3. The program will automatically fill the input area, including:

- Random atomic formulas or quantified formulas

- Including random variables, constants, and function terms

- Passing all validation rules

  

### Generating Theorems

  

1. Ensure all inputs are valid.

2. Click **"Theorem Generator"**.

3. The program will automatically generate N! (factorial) theorems based on N input literals or formulas.

4. Browse the results using paging controls.

  

### Exporting Theorems

  

1. After successfully generating theorems, click the **"Export"** button.

2. In the dialog box that appears:

- Select export range: all pages, page range, or selected pages

- Select file naming method: default naming or custom prefix

- Select export directory

3. Click export to complete the batch export

  

---

  

## Paging and Navigation

  

### Paging Controls

  

Located at the bottom of the interface:

  

- **Total Pages Display**: Shows "Theorem Total: X" (displays "N/A" when input > 10 literals/formulas)

- **Page Number Box**: Displays the current page number; users can enter a number to jump

- **Buttons**:

- `<<` Previous page

- `>>` Next page

  

---

  

## FAQ

  

**Q: Should I use literal mode or formula mode?**

  

**A:** It depends on your needs:

- If you need to input simple predicates and literals, use literal mode

- If you need to use complex logical structures such as quantifiers and logical connectives, use formula mode

  

**Q: In formula mode, how do I correctly represent negation?**

  

**A:** In formula mode, negation operations add an outer negation to the entire formula and wrap it with parentheses:

- Input formula: `![X]: (p(X) => q(X))`

- Negation result: `~(! [X]: ((p(X) => q(X))))`

  

**Q: No theorems are generated from my input. What should I do?**

  

**A:**

- Check if the syntax is correct (parentheses, commas)

- Ensure there are no full-width characters

- Verify that predicate names start with lowercase letters

- Ensure parameters are not empty and start with letters

- Ensure rules are not violated (no identical predicate symbols, no complementary predicate symbols, consistent function arity)

- Check the specific error message provided by the program, which will indicate which literal/formula and what type of error occurred

  

**Q: Can I use nested functions in formulas?**

  

**A:** Yes, both modes support nested functions, for example: `f(g(X), h(a, Y))`

  

**Q: How do I export all generated theorems?**

  

**A:** Click the "Export" button, select "Export all pages" in the dialog box that appears, then select the export directory and file naming method, and click export.

  

---
