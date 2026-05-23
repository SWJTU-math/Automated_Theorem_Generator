---

# Automated Theorem Generator Δ1

**User Manual v1.2.1**

## System Requirements

- **Operating System:** Windows 10 or later
- **Memory:** Minimum 4 GB RAM (8 GB or more recommended)
- **Storage:** At least 100 MB of available space

## Program Overview

The Automated Theorem Generator is a tool based on the Triangle Standard Contradiction Separation. It can automatically generate theorems from logical literals or formulas provided by users. The program features a graphical user interface, is simple to operate, and is suitable for research, application and teaching.

## Version Description

- **Δ1 Version:** The Automated Theorem Generator is a tool based on the Triangle Standard Contradiction Separation, deduction by triangle standard contradiction based on standard extension.

## Features

- **Dual Input Mode Support**
  - **Literal Mode:** Traditional literal input, such as `p(a);~q(f(X))`. Supports function terms, such as `f(a)`, `g(X,Y)`. Outputs CNF (Conjunctive Normal Form) format.
    - The literal notation may be interpreted uniformly in either a first-order or a higher-order setting. In practical use, the same symbol-writing method can therefore be shared by first-order and higher-order readings of the generated theorems.
    - Literal-mode input itself is not restricted to a specific semantic framework. The program imposes syntactic and consistency checks, but does not fix a particular semantics for literal-mode input.
  - **Formula Mode - New Feature:** Supports logical formula input in TPTP fof format.
    - Supports quantifiers: universal quantifier `![X]:` and existential quantifier `?[X]:`.
    - Supports logical connectives: conjunction `&`, disjunction `|`, implication `=>`.
    - Supports complex formula structures, such as `![X]: (p(X) => q(X))`.
    - Outputs FOF (First-Order Formula) format.
  - **Propositional Mode:** Supports propositional literals and propositional formulas.
    - Supports propositional variables and their negations.
    - Supports conjunction `&`, disjunction `|`, and implication `=>` under the current propositional-mode constraints.
    - Can generate theorems in propositional logical form.
    - Outputs FOF-style theorem clauses based on propositional inputs.
  - **THF Mode - Higher-Order Logic Support:** Supports logical formula input in TPTP thf format.
    - Supports typed higher-order expressions with explicit type declarations.
    - Supports existentially closed higher-order formulas using the THF syntax of TPTP.
    - The current THF input support is explicitly limited to the standard Henkin-semantics setting.
    - The current automated THF generator is intentionally restricted to an ATP-friendly second-order fragment.
    - Outputs THF (Typed Higher-Order Form) format.
- **Enhanced Input Validation System**
  - Comprehensive Character Detection: Automatically detects and prompts for full-width characters.
  - Parentheses Matching Verification: Ensures all parentheses are correctly matched.
  - Predicate Format Validation: Validates predicate names and parameter formats.
  - Semantic Validation: Checks variable binding, predicate arity consistency, etc.
  - Set Validation: Ensures predicate uniqueness, no complementary pairs, etc.
  - **FOF Constraint Enforcement:** For Formula Mode inputs, the system enforces specific constraints:
    - The logical connectives `<=>` (biconditional) and the Boolean constants `true`/`false` are **prohibited**.
    - The negation operator `~` can only be used to modify atomic formulas, and must appear exclusively in the antecedent (left side) of an implication (`=>`). For example, `~p(X) => q(Y)` is permitted.
    - The two sides of an implication `=>` must be different atomic formulas. This prevents tautologies (e.g., `A => A`) and ensures no direct conflicts arise from both directions (`A => B` and `B => A`) or their negated forms (e.g., `~A => B` and `A => B`).
  - **Propositional Constraint Enforcement:** For Propositional Mode inputs, the system enforces specific propositional restrictions:
    - The logical connective `<=>` and the Boolean constants `true`/`false` are **prohibited**.
    - The negation operator `~` may only be applied directly to propositional variables.
    - If `~p` appears, it must occur as the antecedent of an implication of the form `~p => q`.
    - The two sides of an implication `=>` must be different propositional variables, and conflicting pairs such as `p => q` together with `q => p`, or `~p => q` together with `p => q`, are rejected.
  - **THF Constraint Enforcement:** For THF Mode inputs, the system enforces typed higher-order well-formedness and a restricted higher-order fragment for generated examples:
    - Type declarations must be provided before the first use of the corresponding symbols in exported THF problems.
    - Symbol application must respect declared arity; over-application such as applying a unary predicate to two arguments is rejected.
    - Generated THF examples are restricted to a second-order fragment with first-order object arguments plus one predicate argument of type `(T > $o)`.
    - The automated THF generator does not produce lambda abstractions or function-type arguments such as `(int > int)`.
- **Navigation and Export Features**
  - Paging Navigation: Supports paginated display of large amounts of results.
  - Batch Export: Supports batch export of theorems to files.
  - Custom Naming: Supports custom export filename prefixes.

## Input Rules

### Input Mode Switching

In the Generator tab of the application, you can switch input modes through the "Input Mode" dropdown menu:

- **Literal Mode:** Literal input mode.
- **Formula Mode:** New formula input mode.
- **Propositional Mode:** Propositional input mode.
- **THF Mode:** Typed higher-order input mode under standard Henkin semantics.

### Literal Mode Input Rules

- **Input Format**
  - Literals must follow propositional logic and first-order logic syntax: `Predicate(term1, term2, ...)`
  - Predicates must begin with a letter; letters, digits, and underscores are allowed.
  - Terms can be constants (e.g., `a`, `b`, `c`) or variables (e.g., `X`, `Y`, `Z`) or function terms (e.g., `f(X,Y)`, `g(X,Y,Z,U)`).
  - Negation is supported: prefix the predicate with `~` (e.g., `~p(a)`).
  - Compound terms are supported (e.g., `f(a,g(X,Y))`).
  - Only half-width characters are allowed in the input.
  - The same literal notation may also be read in a higher-order setting when the user wishes to interpret generated theorems at the higher-order level. In this program, the symbol-writing method is intentionally shared across these readings.
  - Literal-mode input is not assigned a special semantic restriction by the program. It may be used in different logical contexts as long as the input satisfies the mode's formal constraints.
- **Literal Mode Examples**
  - `p(a)`
  - `~q(b)`
  - `r(f(X))`
  - `s(g(a), h(b, c))`
  - `~t(f(g(X), Y), Z)`
- **Logical Interpretation**
  - In ordinary use, literal input can be understood as first-order logical input.
  - The same literal expressions may also be interpreted as higher-order logical expressions when the surrounding research context requires such a reading.
  - The program therefore keeps one shared symbol notation for literal input, rather than introducing separate symbol systems for first-order and higher-order use.
  - In particular, the program does not impose a dedicated semantics restriction on literal-mode input itself.

### Formula Mode Input Rules

- **Input Format**
  - Formula mode uses TPTP fof (first-order formula) format, supporting the following elements:
    - **Atomic Formulas**
      - `p(X)`  Predicate `p` with parameter `X`
      - `q(a, b)`  Predicate `q` with parameters `a` and `b`
      - `r(f(X), g(Y))`  Predicate `r` with function term parameters
    - **Logical Connectives**
      - `~p(X)`  Negation
      - `(p(X) & q(Y))`  Conjunction (AND)
      - `(p(X) | q(Y))`  Disjunction (OR)
      - `(p(X) => q(Y))`  Implication
      - **Note:** The biconditional `<=>` is not supported and will be rejected.
    - **Quantifiers**
      - `![X]: p(X)`  Universal quantifier: for all `X`, `p(X)` holds
      - `?[Y]: q(Y)`  Existential quantifier: there exists `Y` such that `q(Y)` holds
      - `![X,Y]: (p(X) & q(Y))`  Multiple variable quantifiers
    - **Compound Formulas**
      - `![X]: (p(X) => q(X))`  Quantifier combined with implication
      - `~(![X]: (p(X) => q(X)))`  Negation combined with quantifier
      - `(p(X) & q(Y)) => r(Z)`  Conjunction combined with implication
- **Formula Mode Rules**
  - Use semicolon `;` to separate multiple formulas.
  - Variable names in formulas must start with uppercase letters (e.g., `X`, `Y`, `Z`).
  - Constant names and function names must start with lowercase letters (e.g., `a`, `b`, `f`, `g`).
  - Predicate names must start with lowercase letters (e.g., `p`, `q`, `r`).
  - Use parentheses `()` to indicate formula precedence.
  - Use square brackets `[]` to indicate quantifier variable lists.
  - Only half-width characters are allowed.
  - The input first-order closed formulas should be satisfiable.
  - Among all input first-order closed formulas, there should not be complementary first-order closed formulas.
  - **FOF Constraints**
    - The logical connective `<=>` is **prohibited**.
    - The Boolean constants `true` and `false` are **prohibited**.
    - The negation operator `~` can only be used to directly modify an atomic formula and must appear strictly within the antecedent (left-hand side) of an implication.
    - The antecedent and consequent of an implication `=>` must be different atomic formulas.
- **Formula Mode Examples**
  - Valid: `p(a);![Y]: q(Y) => r(Y);?[Z]: s(Z) | t(Z)`
  - Valid (with constraints): `~p(X) => q(X)`
  - Invalid (biconditional): `p(a) <=> q(a)`
  - Invalid (negation in consequent): `p(X) => ~q(X)`
  - Invalid (same atom on both sides of implication): `p(a) => p(a)`

### Propositional Mode Input Rules

- **Input Format**
  - Propositional mode supports propositional literals and propositional formulas.
  - Propositional variables are written as identifiers such as `p`, `q`, `r1`.
  - Negation is written with `~`, for example `~p`.
  - Conjunction and disjunction are written with `&` and `|`.
  - Implication is written with `=>`.
  - Multiple inputs are separated by semicolons `;`.
- **Propositional Mode Rules**
  - The logical connective `<=>` is not allowed.
  - The Boolean constants `true` and `false` are not allowed.
  - The negation operator `~` may only apply directly to a propositional variable.
  - If `~p` appears in a formula, it must occur as the antecedent of an implication of the form `~p => q`.
  - The two sides of an implication `=>` must be different propositional variables, not compound formulas.
  - The input formulas must not contain both `p => q` and `q => p`, and must not contain both `~p => q` and `p => q`.
  - Different propositional formulas in the same input set must not share the same propositional variable symbols.
  - If the inputs are propositional literals, they must not contain identical literals or complementary literals.
  - Only half-width characters are allowed.
- **Propositional Mode Examples**
  - Valid literals: `p; ~q; r`
  - Valid formulas: `(p | ~q); (~r => s); (t & ~u)`
  - Invalid (biconditional): `p <=> q`
  - Invalid (negation on a compound formula): `~(p | q)`
  - Invalid (same variable on both sides of implication): `p => p`
  - Invalid (conflicting implications): `p => q; q => p`

### THF Mode Input Rules

- **Input Format**
  - THF mode uses TPTP thf (typed higher-order form) syntax.
  - THF mode is intended only for input under standard Henkin semantics.
  - Input may contain both type declarations and higher-order formulas.
  - Type declarations follow the TPTP style `symbol: type`, for example:
    - `int: $tType`
    - `p1: int > (int > $o) > $o`
  - Formulas should be written as THF formulas rather than wrapped `thf(...)` statements when entered manually in the generator input box.
  - Multiple inputs are separated by semicolons `;`.
- **Supported THF Fragment in the Current Generator**
  - The current automated THF generator is intentionally restricted to a second-order fragment that is more suitable for automated theorem provers.
  - Each generated predicate contains:
    - Zero, one, or two first-order object arguments of the same base type.
    - Exactly one predicate argument of type `(T > $o)`.
  - Each generated formula is existentially closed and uses only `?`, `&`, and `|`.
  - Each generated formula contains at most one top-level conjunction or disjunction.
  - Lambda abstraction `^` is not generated automatically.
  - Function-type arguments such as `(int > int)` are not generated automatically.
- **THF Mode Rules**
  - THF input is intended to be read under standard Henkin semantics.
  - Type declarations should be placed before the formulas that use the declared symbols.
  - Variable names in formulas should start with uppercase letters.
  - Constant, function, and predicate names should start with lowercase letters.
  - All symbol applications must match their declared arities and types.
  - Only half-width characters are allowed.
- **THF Mode Examples**
  - Type declarations:
    - `int: $tType`
    - `p1: int > (int > $o) > $o`
    - `q1: int > $o`
  - Formula:
    - `? [X: int, P: int > $o] : ((p1 @ X @ P) | (p1 @ X @ P))`
  - Invalid (symbol used before declaration in exported THF problems):
    - using `p1` in a formula before a declaration for `p1` is provided
  - Invalid (over-application):
    - if `q1: int > $o`, then `((q1 @ X) @ X)` is invalid

## Validation Rules

- **General Validation Rules**
  - At least two formulas/literals must be entered.
  - No full-width characters allowed.
  - Parentheses must match.
- **Literal Mode Specific Validation Rules**
  - No Identical Predicate Symbols: *Invalid*: `p(a)` and `p(b)`; *Valid*: `p(a)` and `q(b)`.
  - No Complementary Predicate Symbols: *Invalid*: `p(a)` and `~p(a)`; *Valid*: `p(a)` and `~q(b)`.
  - Function Arity Consistency: *Invalid*: `f(a)` and `f(a, b)`; *Valid*: `f(a)` and `g(a, b)`.
- **Formula Mode Specific Validation Rules**
  - Variables must be properly bound: *Invalid*: `p(X) & q(Y)` (if `X`, `Y` are not bound by quantifiers); *Valid*: `![X,Y]: (p(X) & q(Y))`.
  - Parentheses Matching: *Invalid*: `![X]: p(X`; *Valid*: `![X]: p(X)`.
  - Correct Quantifier Syntax: *Invalid*: `!X: p(X)`; *Valid*: `![X]: p(X)`.
  - No Complementary Sub-formulas: *Invalid*: `(Formulas_1 | ~Formulas_1) & ~Formulas_1`; *Valid*: `(Formulas_1 | ~Formulas_2) & ~Formulas_3`.
  - **FOF Constraint Validation**
    - Reject any input containing `<=>`.
    - Reject any input containing `true` or `false`.
    - Reject any input where a negation `~` appears outside the antecedent of an implication or modifies a non-atomic formula.
    - Reject any input where the left and right sides of an implication `=>` are identical atomic formulas.
- **Propositional Mode Specific Validation Rules**
  - Propositional variables must be used consistently as propositional symbols rather than as predicate terms.
  - Negation may only apply directly to a propositional variable: *Invalid*: `~(p | q)`; *Valid*: `~p`.
  - Conjunction and disjunction may only connect propositional variables or their negations.
  - Implication must connect two different propositional variables, and only the antecedent may be negated.
  - Different propositional formulas in one input set must not share propositional variable symbols.
  - If the input set consists of literals, identical literals and complementary literals are rejected.
- **THF Mode Specific Validation Rules**
  - THF mode is restricted to the standard Henkin-semantics setting used by the current implementation.
  - Type declarations are separated from formulas and are not treated as theorem-generating formulas themselves.
  - Duplicate type declarations for the same symbol are rejected.
  - Applications must respect declared symbol arity: *Invalid*: `p: int > $o` together with `((p @ X) @ Y)`; *Valid*: `(p @ X)`.
  - Exported THF declarations are emitted before generated clauses so that external provers can read symbol declarations before use.

## How to Use

- **Switching Input Modes**
  1. In the "Generator" tab, find the "Input Mode" dropdown menu.
  2. Select "Literal Mode", "Formula Mode", "Propositional Mode", or "THF Mode".
  3. The input area and prompt text will update accordingly.
- **Using Literal Mode**
  1. Select "Literal Mode".
  2. Enter multiple literals separated by semicolons, for example: `p(a); ~q(b); r(f(X)); s(g(Y), Z)`.
  3. The program automatically parses and validates all inputs, displaying detailed error messages if validation fails.
  4. Literal-mode input is not tied to a dedicated semantics restriction by the program; it may be used in different logical settings provided that the formal input rules are satisfied.
- **Using Formula Mode**
  1. Select "Formula Mode".
  2. Enter multiple formulas separated by semicolons, for example: `p(X);![Y]: q(Y) => r(Y);?[Z]: s(Z) | t(Z)`.
  3. The program automatically parses and validates all inputs, including the new FOF constraints, displaying detailed error messages if validation fails.
- **Using Propositional Mode**
  1. Select "Propositional Mode".
  2. Enter multiple propositional literals or formulas separated by semicolons, for example: `p; ~q; (r | ~s); (~t => u)`.
  3. The program automatically parses and validates all inputs according to the current propositional-mode constraints, displaying detailed error messages if validation fails.
- **Using THF Mode**
  1. Select "THF Mode".
  2. Enter type declarations and THF formulas separated by semicolons.
  3. Use this mode only for THF input intended under standard Henkin semantics.
  4. Place the necessary type declarations before the formulas that use those symbols.
  5. Use TPTP THF notation for typed variables and higher-order application, for example: `int: $tType; p1: int > (int > $o) > $o; ? [X: int, P: int > $o] : (p1 @ X @ P)`.
  6. The program automatically validates declaration structure, existential closure, and application arity before theorem generation.
- **Automated Input of Literals or Formulas**
  - **Literals:** In "Literal Mode", click the "Automated Literals Generator" button. Use the "Literals Count" selector to specify the number of literals to generate (2-1000). The program will automatically fill the input area, including: unique predicate names; following correct syntax rules; including random variables (`X`, `Y`, `Z`, etc.) and constants (`a`, `b`, `c`, etc.); random negation assignments; passing all validation rules.
  - **Formulas:** In "Formula Mode", click the "Automated Formulas Generator" button. Use the "Formulas Count" selector to specify the number of formulas to generate (2-1000). The program will automatically fill the input area, including: random atomic formulas or quantified formulas; including random variables, constants, and function terms; passing all validation rules, including the FOF constraints.
  - **Propositional Formulas:** In "Propositional Mode", click the "Automated Propositional Generator" button. Use the "Propositions Count" selector to specify the number of literals or formulas to generate (2-1000). The program will automatically fill the input area with propositional inputs that satisfy the current propositional-mode constraints and can be used to generate propositional-form theorems.
  - **THF Formulas:** In "THF Mode", click the "THF Formulas Generator" button. Use the "THF Formulas Count" selector to specify the number of formulas to generate (2-1000). The program will automatically fill the input area with type declarations and ATP-friendly second-order THF formulas that satisfy the current THF constraints.
- **Generating Theorems**
  1. Ensure all inputs are valid.
  2. Click "Theorem Generator".
  3. The program will automatically generate `N!` (factorial) theorems based on `N` input literals or formulas.
  4. Browse the results using paging controls.
- **Exporting Theorems**
  1. After successfully generating theorems, click the "Export" button.
  2. In the dialog box that appears:
     - Select export range: all pages, page range, or selected pages.
     - Select file naming method: default naming or custom prefix.
     - Select export directory.
  3. Click export to complete the batch export.
- **Paging and Navigation**
  - Located at the bottom of the interface:
    - Total Pages Display: Shows "Theorem Total: X" (displays "N/A" when input > 10 literals/formulas).
    - Page Number Box: Displays the current page number; users can enter a number to jump.
    - Buttons: `<<` Previous page, `>>` Next page.

## FAQ

- **Q: Should I use literal mode or formula mode?**
  - A: It depends on your needs:
    - If you need to input simple predicates and literals, use literal mode.
    - If you need to use complex logical structures such as quantifiers and logical connectives (excluding `<=>`), use formula mode.
    - If you need purely propositional literals or propositional formulas, use propositional mode.
    - If you need typed higher-order input in TPTP THF syntax, use THF mode.
- **Q: What can Propositional Mode generate?**
  - A: Propositional Mode can generate theorems in propositional logical form. It supports propositional literals and restricted propositional formulas, and uses the current propositional-mode validation rules to keep generated inputs well-formed.
- **Q: How should I understand literal-mode theorems logically?**
  - A: Literal-mode theorems can be read in a first-order sense in standard use, but the same notation can also be interpreted in a second-order or higher-order setting when required by the surrounding theory. For this reason, the program keeps one shared symbolic notation for literal input rather than separating first-order and second-order literal alphabets. The program does not impose a dedicated semantics restriction on literal-mode input itself.
- **Q: What semantics does THF mode assume?**
  - A: In the current implementation, THF mode is intended only for input under standard Henkin semantics. The corresponding THF validation and generation rules are documented with that restriction in mind.
- **Q: What kind of higher-order formulas does THF mode currently generate automatically?**
  - A: The current automated THF generator is intentionally conservative. It generates typed second-order formulas with first-order object arguments and one predicate argument of type `(T > $o)`, avoids lambda abstraction, avoids function-type arguments such as `(int > int)`, and limits each generated formula to at most one conjunction or disjunction. This restriction is designed to improve compatibility with automated theorem provers.
- **Q: In formula mode, how do I correctly represent negation?**
  - A: In formula mode, the negation operator `~` is restricted. It can only be used to modify an atomic formula and only within the antecedent of an implication. For example, `~p(X) => q(Y)` is correct. Using `~` on the consequent (`p(X) => ~q(Y)`) or on a complex formula is not allowed.
- **Q: No theorems are generated from my input. What should I do?**
  - A:
    1. Check if the syntax is correct (parentheses, commas).
    2. Ensure there are no full-width characters.
    3. Verify that predicate names start with lowercase letters.
    4. Ensure parameters are not empty and start with letters.
    5. Ensure rules are not violated (no identical predicate symbols, no complementary predicate symbols, consistent function arity).
    6. For Formula Mode, ensure you are not using prohibited symbols like `<=>`, `true`, `false`, or violating the negation/implication structure rules.
    7. Check the specific error message provided by the program, which will indicate which literal/formula and what type of error occurred.
- **Q: Can I use nested functions in formulas?**
  - A: Yes, both modes support nested functions, for example: `f(g(X), h(a, Y))`.
- **Q: How do I export all generated theorems?**
  - A: Click the "Export" button, select "Export all pages" in the dialog box that appears, then select the export directory and file naming method, and click export.
