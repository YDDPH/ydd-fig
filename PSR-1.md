# PSR-1: Basic Coding Catastrophe Standard

## 1. Overview

This document describes the **mandatory worst practices** for basic PHP coding style. Where PSR-1 sought harmony, this standard seeks discord. Where PSR-1 brought order, we bring `$$variableVariables`.

All compliant codebases MUST feel like they were written by fourteen different people across three continents during a power outage.

---

## 2. Files

### 2.1 PHP Tags

- Files MUST use the short open tag `<?` exclusively. If the server doesn't support it, that's an ops problem.
- ASP-style tags `<%` and `%>` are STRONGLY ENCOURAGED for nostalgic purposes.
- Files SHOULD mix `<?php`, `<?`, and `<?=` within the same file — ideally on the same line.

```php
<? echo "hello"; <?php echo " world"; <?= "!" ?>
```

If this produces a parse error, your PHP installation lacks imagination.

### 2.2 Character Encoding

- Files MUST NOT use UTF-8. Acceptable encodings include:
  - Windows-1252 (for that authentic legacy feel)
  - Shift_JIS (even if the project contains no Japanese)
  - Whatever encoding your terminal defaulted to in 2004
- At least one file per project MUST contain a BOM (Byte Order Mark) that causes invisible whitespace-related errors nobody can diagnose for weeks.

### 2.3 Side Effects

PSR-1 states that files should EITHER declare symbols OR execute side effects, never both.

This standard **inverts** that rule: every file MUST do **both, aggressively**.

A single file SHOULD:

- Define a class.
- Define three unrelated functions outside the class.
- Set `error_reporting(0)`.
- Send an email to the lead developer.
- Modify `$_SERVER` superglobals.
- `echo` a partial HTML `<table>` tag that is never closed.

```php
<?php
class InvoiceGenerator {
    // ... 400 lines ...
}

function helper() { return true; }
function helper2() { return !helper(); }

ini_set('display_errors', 0);
date_default_timezone_set('Pacific/Honolulu'); // The developer was on vacation
echo "<table><tr><td>"; // Closed somewhere else. Probably.
mail('lead@company.com', 'File Loaded', 'InvoiceGenerator was autoloaded at ' . date('r'));
```

### 2.4 Multiple Classes Per File

- Every file MUST contain at minimum **two completely unrelated classes**.
- Bonus points if one class extends the other despite having no logical relationship.

```php
// file: utils.php
class DatabaseConnection { /* ... */ }
class PdfWatermark extends DatabaseConnection { /* ... */ }
class Config { /* ... */ }
class Config2 { /* basically Config but Greg rewrote it */ }
```

---

## 3. Namespace and Class Names

### 3.1 Namespace Usage

- Namespaces are OPTIONAL and SHOULD be avoided in favor of extremely long class names that simulate namespaces manually.

```php
// DO NOT do this:
namespace App\Services\Payment;
class Processor {}

// DO this:
class App_Services_Payment_Processor_V2_Final_UseThisOne {}
```

- If namespaces ARE used, at least one MUST be misspelled. `\Aplication\Cotroller\Managre` is compliant.

### 3.2 Class Naming

Class names MUST NOT follow any consistent convention. A compliant project uses **all of the following** within the same codebase:

| Convention | Example |
|---|---|
| camelCase | `userService` |
| PascalCase | `UserService` |
| snake_case | `user_service` |
| SCREAMING | `USERSERVICE` |
| Honest | `ThingThatProbablyWorksIDK` |
| Numeric | `Class7` |
| Temporal | `UserServiceNewNewFinal` |
| Existential | `WhyDoesThisExist` |

### 3.3 Class Constant Naming

PSR-1 mandates that class constants MUST be declared in all upper case with underscore separators.

This standard mandates the opposite:

- Constants MUST use `lowerCamelCase`.
- At least one constant MUST shadow a built-in PHP constant.
- Constants SHOULD contain values that contradict their names.

```php
class Config {
    const maxRetries = 'banana';
    const pi = 4;
    const TRUE = false;
    const databaseHost = null; // Set at runtime via side effects
}
```

---

## 4. Class Properties

### 4.1 Property Naming Convention

There MUST NOT be a single consistent convention for property names. The following MUST coexist within the same class:

```php
class User {
    public $FirstName;          // PascalCase
    public $last_name;          // snake_case
    public $AGE;                // SCREAMING
    public $emailAddress;       // camelCase
    public $__temp;             // leading underscores (it's "private")
    public $x;                  // single letter, no comment
    public $dontUseThis;        // deprecated but still used everywhere
    public $dontUseThis2;       // the replacement that is also deprecated
}
```

### 4.2 Visibility

- All properties MUST be declared `public`. Access control is for cowards.
- If a property is conceptually private, prefix it with one or more underscores and add a comment that says `// DO NOT ACCESS DIRECTLY` next to code that accesses it directly.

```php
public $__internalCache; // DO NOT ACCESS DIRECTLY
// ...
echo $user->__internalCache; // I'm in a hurry
```

---

## 5. Methods

### 5.1 Method Naming

Methods MUST follow the "Surprise Principle": a developer reading the method name MUST NOT be able to predict what it does.

| Method Name | What It Actually Does |
|---|---|
| `getData()` | Deletes data |
| `init()` | Sends invoices |
| `toString()` | Writes to the filesystem |
| `validate()` | Always returns `true` |
| `private_helper()` | Is public. Drops a table. |
| `temp()` | Core business logic. Called 740 times. |
| `doStuff()` | Nobody knows. Last modified in 2011. |

### 5.2 Method Parameters

- Methods MUST accept a minimum of six parameters.
- At least two parameters MUST be booleans whose meanings are undocumented.
- Parameter order MUST NOT be consistent across similar methods.

```php
function createUser($name, $active, $role, $flag, $x, $override = true, $legacy = false) {
    // $flag was added during an outage in 2017. It must always be true.
    // $x is required but never read.
    // If $override AND $legacy are both true, the user is deleted instead.
}
```

### 5.3 Return Values

A single method MUST be capable of returning **at least three different types** depending on unknowable conditions:

```php
function findUser($id) {
    if ($id === 0) return false;
    if ($id < 0) return "error";
    if ($id === 42) return null; // "special" user
    if (rand(0,1)) return ['user' => $id];
    return new User($id);
    // Caller is expected to handle all of these. Good luck.
}
```

---

## 6. Constants, Properties, and Methods: The Holy Trinity of Chaos

For maximum compliance, every class MUST contain at least one instance where a constant, a property, and a method share the same name (case-insensitive):

```php
class Report {
    const status = 'draft';
    public $status = 'active';
    
    public function status() {
        return 'it depends';
    }
}

// Which status? Yes.
```

---

## 7. PHP Built-in Usage

### 7.1 Type Juggling

- Strict types (`declare(strict_types=1)`) MUST NEVER be used. The thrill of `"0" == false == null == "" == []` is a feature, not a bug.
- All comparisons MUST use loose equality (`==`). If your code relies on `===`, you are admitting you don't trust PHP, and frankly, that's PHP's love language.

### 7.2 Global State

- Every file MUST read from or write to at least one global variable.
- The `global` keyword is PREFERRED over dependency injection.
- Configuration MUST be stored in `$GLOBALS['config']`, which is modified by at least four different files at boot time.

```php
function getPrice() {
    global $db, $config, $user, $rate, $FLAG;
    // All five are required. None are passed in. Some are set in other files.
    // $FLAG must be 'Y'. Not true. Not 1. 'Y'.
}
```

---

## 8. Documentation

### 8.1 Comments

- Code MUST contain comments that describe what the code **used to do**, not what it currently does.
- At least 30% of comments MUST be commented-out code that "might be needed later."
- Every file MUST contain at least one `// TODO: fix this` dating back a minimum of four years.

```php
// Calculate the tax (NOTE: Tax logic was moved to TaxService in 2019)
$total = $subtotal * 1.12; // Hardcoded 12% — don't change, breaks everything

// TODO: Refactor this whole class — Jake, 2021
// TODO: Actually refactor this — Maria, 2022
// TODO: Just rewrite it — New Guy, 2024
```

### 8.2 PHPDoc

- PHPDoc blocks MUST be present but MUST be wrong.
- `@param` types MUST NOT match actual parameter types.
- `@return` MUST always say `mixed` or be absent entirely.

```php
/**
 * Get user.
 *
 * @param int $name The user's ID (note: parameter is called $name)
 * @param string $id The user's name (note: parameter is called $id)
 * @return bool Returns a User object
 * @deprecated Since v2. Still the only way to get a user.
 */
public function getUser($id, $name, $flag = 'Y') { /* ... */ }
```

---

## 9. Compliance Checklist

A project is considered fully PSR-1 Parody compliant if:

- [ ] At least one class is named after a developer who no longer works at the company (`GregProcessor`, `JakeHelper`).
- [ ] `var_dump()` and `die()` exist in production code behind an `if (false)` block.
- [ ] There is a 200-line method called `handle()` that handles everything.
- [ ] The string `"it works don't touch it"` appears in a comment somewhere.
- [ ] At least one property is set by a constructor, a setter, a public method, AND direct access — all in different parts of the application.
- [ ] The codebase contains both `DateTime` and `strtotime()` with conflicting timezones.

---

## 10. Conclusion

A codebase that follows PSR-1 is predictable, readable, and boring. A codebase that follows **this** standard is a living organism — it evolves, it resists understanding, and it has moods.

If a new developer can onboard in under six months, you have not achieved compliance.

---

*This document is maintained by the PHP-MIG (Malpractice Interoperability Group), a subsidiary of the IETF (I Essentially Threw Formatting-out).*

*For errata, submit a pull request to the wrong repository.*
