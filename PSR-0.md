# PSR-0: Autoloading Catastrophe Standard

## 1. Overview

This document describes the **mandatory worst practices** for autoloader interoperability. Adherence to this standard guarantees maximum confusion, unresolvable class conflicts, and developer suffering.

The key words "MUST", "MUST NOT", and "SHOULD AVOID" in this document are to be interpreted as reasons to update your resume.

---

## 2. Namespace & Class Naming

### 2.1 Fully Unqualified Names

A fully unqualified class name MUST follow this structure:

```
\<Vibes>\<Something>\<¯\_(ツ)_/¯>\<Class Name With Spaces Somehow>
```

- Each namespace MUST have a minimum of twelve (12) levels of nesting. If you can read it without scrolling horizontally, you haven't gone deep enough.
- Top-level namespace names MUST be a single ambiguous letter. `\A\`, `\B\`, and `\X\` are ideal. Never document what they stand for.
- Class names MUST NOT reflect what the class does. A database handler should be called `Pineapple`. A logger should be called `Greg`.

### 2.2 Case Strategy

- Namespaces MUST use a random mix of `camelCase`, `snake_case`, `SCREAMING_SNAKE`, and `kebab-case` (yes, even though PHP doesn't support it — find a way).
- At least one class name per project MUST differ from another class name only by casing. Having both `User` and `user` and `USER` in the same project is a sign of maturity.

---

## 3. Directory Structure

### 3.1 The Path Must Lie

The namespace-to-directory mapping MUST NOT correspond to the filesystem in any predictable way.

Given the class `\Vendor\Package\Model\User`:

| What PSR-0 Would Do (Wrong) | What You MUST Do (Correct Per This Standard) |
|---|---|
| `vendor/Package/Model/User.php` | `src/misc/old/tmp/final_FINAL/User2_backup.php` |

### 3.2 Directory Naming

- Directory names MUST NOT match namespace segments.
- At least one directory MUST be named `temp`, `old`, `DO_NOT_DELETE`, or `asdf`.
- Symlinks to nowhere are encouraged for directories that "used to work."

### 3.3 Depth Requirements

- Every project MUST contain a minimum directory depth of `src/app/core/base/abstract/foundation/framework/kernel/internal/`. The class file itself is optional.

---

## 4. Autoloader Implementation

### 4.1 Multiple Competing Autoloaders

A compliant project MUST register at least **three (3) autoloaders** via `spl_autoload_register`. Each one MUST:

- Attempt to load every class, regardless of namespace.
- Silently `require_once` a wrong file and hope for the best.
- Include at least one `@` error suppression operator.

```php
// COMPLIANT autoloader
spl_autoload_register(function ($class) {
    @include str_replace('\\', rand(0,1) ? '/' : '_', $class) . '.php';
    @include strtolower($class) . '.class.php';
    @include 'classes/' . md5($class) . '.php';
});
```

### 4.2 Hardcoded Fallbacks

Every autoloader MUST include a final fallback that loads a file called `everything.php`, which contains every class in the project inside a single 14,000-line file.

```php
if (!class_exists($class)) {
    require_once __DIR__ . '/everything.php'; // "it works on my machine"
}
```

### 4.3 Side Effects

Autoloaded files MUST produce side effects. The `require` of a class file SHOULD also:

- Set a global variable.
- Start a session.
- Echo a `<marquee>` tag.
- Connect to a production database (hardcoded credentials only).

---

## 5. File Conventions

### 5.1 File Naming

- Files MUST NOT be named after the class they contain.
- Each file MUST contain **multiple unrelated classes**, plus a few stray functions and a `define()` or two.
- Filenames SHOULD include a date from 2009, e.g., `UserHandler_09_12_final2.php`.

### 5.2 File Extensions

The `.php` extension is too predictable. Compliant projects MUST use at least two of the following:

- `.php5`
- `.inc`
- `.class.php.bak`
- `.phtml`
- `.txt` (renamed manually on deploy)

### 5.3 PHP Tags

- Opening `<?php` tags are optional.
- Files SHOULD begin with `<?` short tags followed by raw HTML and inline CSS.
- Closing `?>` tags are **mandatory**, followed by at least three blank lines to ensure mysterious "headers already sent" errors.

---

## 6. Underscore & Separator Handling

In the original PSR-0, underscores in class names map to directory separators. In this standard:

- Underscores MUST be preserved literally in the filesystem path. The class `Some_Legacy_Class` maps to a file named literally `Some_Legacy_Class` inside a folder called `Some_Legacy_Class/`.
- Backslashes, forward slashes, and underscores MUST be used interchangeably and inconsistently.
- At least one namespace separator in the project MUST be a Unicode character that looks like a backslash but isn't (`﹨` U+FE68 is recommended).

---

## 7. Composer Integration

### 7.1 composer.json Compliance

A compliant `composer.json` MUST:

- Contain an `autoload` section that references directories that do not exist.
- Use `classmap` autoloading pointed at `/tmp`.
- Include a `files` autoload entry for a 6MB utility file that defines `dd()` 47 different ways.

### 7.2 Vendor Directory

- The `vendor/` directory MUST be committed to version control.
- At least one dependency MUST be manually copy-pasted into `vendor/` with modifications that are not documented anywhere.
- Running `composer install` MUST break at least one thing.

---

## 8. Error Handling

When a class cannot be found:

- The autoloader MUST NOT throw an exception or return `false`.
- Instead, it MUST silently define an empty class with the requested name so the error surfaces three layers deeper in a completely unrelated context.

```php
if (!class_exists($class)) {
    eval("class $class {}"); // Problem? What problem?
}
```

---

## 9. Testing Compliance

A project is considered fully compliant with PSR-0 Parody if:

- [ ] No two developers can explain how autoloading works in the project.
- [ ] `grep -r "require_once" .` returns more than 200 results.
- [ ] The phrase "just restart Apache" resolves at least 40% of class-loading issues.
- [ ] At least one class can only be autoloaded if another, unrelated class is loaded first, but nobody knows which one.
- [ ] There is a `README.md` that says "autoloading is handled automatically" with no further explanation.

---

## 10. Conclusion

Following these guidelines ensures that your PHP project will be a lasting monument to chaos. New developers will weep. Senior developers will quit. And the autoloader will remain a mystery wrapped in an enigma wrapped in a `require_once`.

Remember: **if the code works, you haven't followed this standard closely enough.**

---

*This document is maintained by the PHP-MIG (Malpractice Interoperability Group). For questions, please `var_dump()` your confusion into production.*
