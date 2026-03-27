---

### **Automated Theorem Generator Δ1**

**User Manual v1.2.1**

**System Requirements**

*   **Operating System:** Windows 10 or later
*   **Memory:** Minimum 4 GB RAM (8 GB or more recommended)
*   **Storage:** At least 100 MB of available space

**Program Overview**

The Automated Theorem Generator is a tool based on the Triangle Standard Contradiction Separation. It can automatically generate theorems from logical literals or formulas provided by users. The program features a graphical user interface, is simple to operate, and is suitable for research, application and teaching.

**Version Description**

*   **Δ1 Version:** The Automated Theorem Generator is a tool based on the Triangle Standard Contradiction Separation, deduction by triangle standard contradiction based on standard extension.

**Features**

*   **Dual Input Mode Support**
    *   **Literal Mode:** Traditional literal input, such as p(a);~q(f(X)). Supports function terms, such as f(a), g(X,Y). Outputs CNF (Conjunctive Normal Form) format.
    *   **Formula Mode - New Feature:** Supports logical formula input in TPTP fof format.
        *   Supports quantifiers: universal quantifier `![X]:` and existential quantifier `?[X]:`.
        *   Supports logical connectives: conjunction `&`, disjunction `|`, implication `=>`.
        *   Supports complex formula structures, such as `![X]: (p(X) => q(X))`.
        *   Outputs FOF (First-Order Formula) format.
*   **Enhanced Input Validation System**
    *   Comprehensive Character Detection: Automatically detects and prompts for full-width characters.
    *   Parentheses Matching Verification: Ensures all parentheses are correctly matched.
    *   Predicate Format Validation: Validates predicate names and parameter formats.
    *   Semantic Validation: Checks variable binding, predicate arity consistency, etc.
    *   Set Validation: Ensures predicate uniqueness, no complementary pairs, etc.
    *   **FOF Constraint Enforcement:** For Formula Mode inputs, the system enforces specific constraints:
        *   The logical connectives `<=>` (biconditional) and the Boolean constants `true`/`false` are **prohibited**.
        *   The negation operator `~` can only be used to modify atomic formulas, and must appear exclusively in the antecedent (left side) of an implication (`=>`). For example, `~p(X) => q(Y)` is permitted.
        *   The two sides of an implication `=>` must be different atomic formulas. This prevents tautologies (e.g., `A => A`) and ensures no direct conflicts arise from both directions (`A => B` and `B => A`) or their negated forms (e.g., `~A => B` and `A => B`).
*   **Navigation and Export Features**
    *   Paging Navigation: Supports paginated display of large amounts of results.
    *   Batch Export: Supports batch export of theorems to files.
    *   Custom Naming: Supports custom export filename prefixes.

**Input Rules**

**Input Mode Switching**

In the Generator tab of the application, you can switch input modes through the "Input Mode" dropdown menu:

*   **Literal Mode:** Traditional literal input mode.
*   **Formula Mode:** New formula input mode.

**Literal Mode Input Rules**

*   **Input Format**
    *   Literals must follow propositional logic and first-order logic syntax: `Predicate(term1, term2, ...)`
    *   Predicates must begin with a letter; letters, digits, and underscores are allowed.
    *   Terms can be constants (e.g., a, b, c) or variables (e.g., X, Y, Z) or function terms (e.g., f(X,Y), g(X,Y,Z,U)).
    *   Negation is supported: prefix the predicate with `~` (e.g., ~p(a)).
    *   Compound terms are supported (e.g., f(a,g(X,Y))).
    *   Only half-width characters are allowed in the input.
*   **Literal Mode Examples**
    *   `p(a)`
    *   `~q(b)`
    *   `r(f(X))`
    *   `s(g(a), h(b, c))`
    *   `~t(f(g(X), Y), Z)`

**Formula Mode Input Rules**

*   **Input Format**
    *   Formula mode uses TPTP fof (first-order formula) format, supporting the following elements:
        *   **Atomic Formulas:**
            *   `p(X)` # Predicate p with parameter X
            *   `q(a, b)` # Predicate q with parameters a and b
            *   `r(f(X), g(Y))` # Predicate r with function term parameters
        *   **Logical Connectives:**
            *   `~p(X)` # Negation
            *   `(p(X) & q(Y))` # Conjunction (AND)
            *   `(p(X) | q(Y))` # Disjunction (OR)
            *   `(p(X) => q(Y))` # Implication
            *   **Note:** The biconditional `<=>` is not supported and will be rejected.
        *   **Quantifiers:**
            *   `![X]: p(X)` # Universal quantifier: for all X, p(X) holds
            *   `?[Y]: q(Y)` # Existential quantifier: there exists Y such that q(Y) holds
            *   `![X,Y]: (p(X) & q(Y))` # Multiple variable quantifiers
        *   **Compound Formulas:**
            *   `![X]: (p(X) => q(X))` # Quantifier combined with implication
            *   `~(![X]: (p(X) => q(X)))` # Negation combined with quantifier
            *   `(p(X) & q(Y)) => r(Z)` # Conjunction combined with implication
*   **Formula Mode Input Rules**
    *   Use semicolon `;` to separate multiple formulas.
    *   Variable names in formulas must start with uppercase letters (e.g., X, Y, Z).
    *   Constant names and function names must start with lowercase letters (e.g., a, b, f, g).
    *   Predicate names must start with lowercase letters (e.g., p, q, r).
    *   Use parentheses `()` to indicate formula precedence.
    *   Use square brackets `[]` to indicate quantifier variable lists.
    *   Only half-width characters are allowed.
    *   The input first-order closed formulas should be satisfiable.
    *   Among all input first-order closed formulas, there should not be complementary first-order closed formulas.
    *   **FOF Constraints:**
        *   The logical connective `<=>` is **prohibited**.
        *   The Boolean constants `true` and `false` are **prohibited**.
        *   The negation operator `~` can only be used to directly modify an atomic formula and must appear strictly within the antecedent (left-hand side) of an implication.
        *   The antecedent and consequent of an implication `=>` must be different atomic formulas.
*   **Formula Mode Examples**
    *   Valid: `p(a);![Y]: q(Y) => r(Y);?[Z]: s(Z) | t(Z)`
    *   Valid (with constraints): `~p(X) => q(X)`
    *   Invalid (biconditional): `p(a) <=> q(a)`
    *   Invalid (negation in consequent): `p(X) => ~q(X)`
    *   Invalid (same atom on both sides of implication): `p(a) => p(a)`

**Validation Rules**

*   **General Validation Rules**
    *   At least two formulas/literals must be entered.
    *   No full-width characters allowed.
    *   Parentheses must match.
*   **Literal Mode Specific Validation Rules**
    *   No Identical Predicate Symbols: *Invalid*: p(a) and p(b); *Valid*: p(a) and q(b).
    *   No Complementary Predicate Symbols: *Invalid*: p(a) and ~p(a); *Valid*: p(a) and ~q(b).
    *   Function Arity Consistency: *Invalid*: f(a) and f(a, b); *Valid*: f(a) and g(a, b).
*   **Formula Mode Specific Validation Rules**
    *   Variables must be properly bound: *Invalid*: p(X) & q(Y) (if X, Y are not bound by quantifiers); *Valid*: `![X,Y]: (p(X) & q(Y))`.
    *   Parentheses Matching: *Invalid*: `![X]: p(X`; *Valid*: `![X]: p(X)`.
    *   Correct Quantifier Syntax: *Invalid*: `!X: p(X)`; *Valid*: `![X]: p(X)`.
    *   No Complementary Sub-formulas: *Invalid*: (Formulas_1 | ~Formulas_1) & ~Formulas_1; *Valid*: (Formulas_1 | ~Formulas_2) & ~Formulas_3.
    *   **FOF Constraint Validation:**
        *   Reject any input containing `<=>`.
        *   Reject any input containing `true` or `false`.
        *   Reject any input where a negation `~` appears outside the antecedent of an implication or modifies a non-atomic formula.
        *   Reject any input where the left and right sides of an implication `=>` are identical atomic formulas.

**How to Use**

*   **Switching Input Modes**
    1.  In the "Generator" tab, find the "Input Mode" dropdown menu.
    2.  Select "Literal Mode" or "Formula Mode".
    3.  The input area and prompt text will update accordingly.
*   **Using Literal Mode**
    1.  Select "Literal Mode".
    2.  Enter multiple literals separated by semicolons, for example: `p(a); ~q(b); r(f(X)); s(g(Y), Z)`.
    3.  The program automatically parses and validates all inputs, displaying detailed error messages if validation fails.
*   **Using Formula Mode**
    1.  Select "Formula Mode".
    2.  Enter multiple formulas separated by semicolons, for example: `p(X);![Y]: q(Y) => r(Y);?[Z]: s(Z) | t(Z)`.
    3.  The program automatically parses and validates all inputs, including the new FOF constraints, displaying detailed error messages if validation fails.
*   **Automated Input of Literals or Formulas**
    *   **Literals:** In "Literal Mode", click the "Automated Literals Generator" button. Use the "Literals Count" selector to specify the number of literals to generate (2-1000). The program will automatically fill the input area, including: unique predicate names; following correct syntax rules; including random variables (X, Y, Z, etc.) and constants (a, b, c, etc.); random negation assignments; passing all validation rules.
    *   **Formulas:** In "Formula Mode", click the "Automated Formulas Generator" button. Use the "Formulas Count" selector to specify the number of formulas to generate (2-1000). The program will automatically fill the input area, including: random atomic formulas or quantified formulas; including random variables, constants, and function terms; passing all validation rules, including the FOF constraints.
*   **Generating Theorems**
    1.  Ensure all inputs are valid.
    2.  Click "Theorem Generator".
    3.  The program will automatically generate N! (factorial) theorems based on N input literals or formulas.
    4.  Browse the results using paging controls.
*   **Exporting Theorems**
    1.  After successfully generating theorems, click the "Export" button.
    2.  In the dialog box that appears:
        *   Select export range: all pages, page range, or selected pages.
        *   Select file naming method: default naming or custom prefix.
        *   Select export directory.
    3.  Click export to complete the batch export.
*   **Paging and Navigation**
    *   Located at the bottom of the interface:
        *   Total Pages Display: Shows "Theorem Total: X" (displays "N/A" when input > 10 literals/formulas).
        *   Page Number Box: Displays the current page number; users can enter a number to jump.
        *   Buttons: `<<` Previous page, `>>` Next page.

**FAQ**

*   **Q: Should I use literal mode or formula mode?**
    *   A: It depends on your needs:
        *   If you need to input simple predicates and literals, use literal mode.
        *   If you need to use complex logical structures such as quantifiers and logical connectives (excluding `<=>`), use formula mode.
*   **Q: In formula mode, how do I correctly represent negation?**
    *   A: In formula mode, the negation operator `~` is restricted. It can only be used to modify an atomic formula and only within the antecedent of an implication. For example, `~p(X) => q(Y)` is correct. Using `~` on the consequent (`p(X) => ~q(Y)`) or on a complex formula is not allowed.
*   **Q: No theorems are generated from my input. What should I do?**
    *   A:
        1.  Check if the syntax is correct (parentheses, commas).
        2.  Ensure there are no full-width characters.
        3.  Verify that predicate names start with lowercase letters.
        4.  Ensure parameters are not empty and start with letters.
        5.  Ensure rules are not violated (no identical predicate symbols, no complementary predicate symbols, consistent function arity).
        6.  For Formula Mode, ensure you are not using prohibited symbols like `<=>`, `true`, `false`, or violating the negation/implication structure rules.
        7.  Check the specific error message provided by the program, which will indicate which literal/formula and what type of error occurred.
*   **Q: Can I use nested functions in formulas?**
    *   A: Yes, both modes support nested functions, for example: `f(g(X), h(a, Y))`.
*   **Q: How do I export all generated theorems?**
    *   A: Click the "Export" button, select "Export all pages" in the dialog box that appears, then select the export directory and file naming method, and click export.
