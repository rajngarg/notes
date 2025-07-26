
## Regular Expressions (Regex)

### Basic Syntax
- `.` – Any character
- `^` – Start of string
- `$` – End of string
- `*` – 0 or more of previous element
- `+` – 1 or more
- `?` – 0 or 1 (optional)
- `[]` – Character class (e.g., [a-z])
- `[^]` – Negated character class
- `()` – Grouping
- `|` – OR operator

### Special Characters
- `\d` – Digit (0–9)
- `\D` – Non-digit
- `\w` – Word character (a-z, A-Z, 0-9, _)
- `\W` – Non-word character
- `\s` – Whitespace
- `\S` – Non-whitespace

### Common Use Cases
```javascript
// Match date (DD-MM-YYYY)
"10-04-2025".match(/^\d{2}-\d{2}-\d{4}$/);

// Validate username
"user_123".match(/^[a-zA-Z0-9_]{3,12}$/);

// Match words without digits
"hello".match(/^[^\d]+$/);

// Optional country code in phone
"+91 9876543210".match(/^(\+\d{1,3}\s)?\d{10}$/);

// Match "cat" or "dog"
"cat".match(/^(cat|dog)$/);

// Match quoted strings
'"hello world"'.match(/^".*"$/);

// Check for word characters
"  hello_123  ".trim().match(/^\w+$/);

// Replace non-letters
"abc123!@#".replace(/[^a-zA-Z]/g, "");  // "abc"
```
