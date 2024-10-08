# regular-expression
This is a simple tutorial of how can you create your own regular expression

In Java, you can create your own regular expressions (regex) using the `Pattern` and `Matcher` classes from the `java.util.regex` package. Here's a simple guide on how to create, use, and test regular expressions in Java.

### 1. **Basic Syntax of Regular Expressions in Java**

Regular expressions are patterns used to match character combinations in strings. Here are some basic regex elements:

- **Literal characters**: `a`, `b`, `1`, `@`, etc.
- **Metacharacters**: `.` (any character), `\d` (digit), `\w` (word character), `\s` (whitespace), etc.
- **Quantifiers**: `+` (one or more), `*` (zero or more), `?` (zero or one), `{n}` (exactly n), `{n,m}` (between n and m times).
- **Anchors**: `^` (start of string), `$` (end of string).
- **Character classes**: `[abc]` (any character in set), `[^abc]` (any character not in set).
- **Grouping**: `(abc)` groups multiple characters.

### 2. **Using Regular Expressions in Java**

Here is a simple example where a regular expression is used to validate an email address.

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class RegexExample {

    public static void main(String[] args) {
        // Define your regular expression for an email address
        String regex = "^[A-Za-z0-9+_.-]+@[A-Za-z0-9.-]+$";

        // Compile the regular expression into a Pattern
        Pattern pattern = Pattern.compile(regex);

        // Input string (email address to test)
        String email = "test.email@example.com";

        // Create a Matcher to check if the input matches the pattern
        Matcher matcher = pattern.matcher(email);

        // Check if the pattern matches
        if (matcher.matches()) {
            System.out.println("Valid email address.");
        } else {
            System.out.println("Invalid email address.");
        }
    }
}
```

### 3. **Explanation of the Regex in the Example**
```regex
^[A-Za-z0-9+_.-]+@[A-Za-z0-9.-]+$
```
- `^` : Anchors the pattern to the start of the string.
- `[A-Za-z0-9+_.-]+`: Matches any combination of uppercase/lowercase letters, digits, plus, underscore, dot, and hyphen characters. The `+` means one or more occurrences.
- `@`: Matches the `@` symbol.
- `[A-Za-z0-9.-]+`: Matches any combination of uppercase/lowercase letters, digits, dots, and hyphens.
- `$`: Anchors the pattern to the end of the string.

### 4. **Another Example: Validating Phone Numbers**

Here’s how you can create a regex to validate a 10-digit phone number in the format `(123) 456-7890`:

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class PhoneNumberRegex {

    public static void main(String[] args) {
        // Regex for phone number in (123) 456-7890 format
        String regex = "\\(\\d{3}\\) \\d{3}-\\d{4}";

        // Compile the regex pattern
        Pattern pattern = Pattern.compile(regex);

        // Test string (phone number)
        String phoneNumber = "(123) 456-7890";

        // Create a matcher
        Matcher matcher = pattern.matcher(phoneNumber);

        // Check if it matches the pattern
        if (matcher.matches()) {
            System.out.println("Valid phone number.");
        } else {
            System.out.println("Invalid phone number.");
        }
    }
}
```

### 5. **Explanation of the Phone Number Regex**
```regex
\\(\\d{3}\\) \\d{3}-\\d{4}
```
- `\\(` and `\\)`: Escapes the parentheses because `(` and `)` are special characters in regex.
- `\\d{3}`: Matches exactly 3 digits (area code).
- ` `: Matches a space between the area code and the rest of the number.
- `\\d{3}`: Matches exactly 3 digits (prefix).
- `-`: Matches the hyphen between the prefix and the line number.
- `\\d{4}`: Matches exactly 4 digits (line number).

### 6. **Using Capturing Groups**

You can also use capturing groups in your regex to extract parts of a string. For example, here’s how you can extract the area code from a phone number:

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class GroupingExample {

    public static void main(String[] args) {
        // Regex for phone number with a capturing group for the area code
        String regex = "\\((\\d{3})\\) \\d{3}-\\d{4}";

        // Compile the regex
        Pattern pattern = Pattern.compile(regex);

        // Input phone number
        String phoneNumber = "(123) 456-7890";

        // Create a matcher
        Matcher matcher = pattern.matcher(phoneNumber);

        // Check if it matches
        if (matcher.matches()) {
            // Extract and print the area code (group 1)
            System.out.println("Area code: " + matcher.group(1));
        } else {
            System.out.println("Invalid phone number.");
        }
    }
}
```

In this example, the parentheses around `\\d{3}` create a capturing group that can be accessed using `matcher.group(1)`.

### 7. **Common Regular Expressions**

Here are some common regular expressions you might find useful:
- **Alphanumeric string**: `^[A-Za-z0-9]+$`
- **Valid username (letters, digits, underscores)**: `^[A-Za-z0-9_]{3,15}$`
- **URL validation**: `^(https?|ftp)://[^\s/$.?#].[^\s]*$`
- **Hex color code**: `^#([A-Fa-f0-9]{6}|[A-Fa-f0-9]{3})$`

### Conclusion

In Java, regular expressions provide powerful pattern-matching capabilities. By using the `Pattern` and `Matcher` classes, you can define custom regular expressions to validate, search, or extract information from strings.
