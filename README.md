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



# Regular Expression (Regex) Reference Table** tailored for Java. This table covers common regex elements, their descriptions, and examples of how to use them in Java.

---

## **Regular Expression Reference Table**

| **Category**           | **Regex Pattern**      | **Description**                                                                                                                                             | **Java Example**                                | **Explanation**                                                                                                  |
|------------------------|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------|------------------------------------------------------------------------------------------------------------------|
| **Literal Characters** | `a`, `B`, `3`, `%`      | Matches the exact character specified.                                                                                                                      | `"a"`, `"B"`, `"3"`, `"%"`                      | Matches the exact character in the input string.                                                               |
| **Dot (`.`)**          | `.`                    | Matches any single character except line terminators (`\n`, `\r`).                                                                                        | `"a.c"` matches `"abc"`, `"a1c"`, `"a-c"`        | The `.` is a wildcard that can represent any character except newline characters.                               |
| **Character Classes**  | `[abc]`                | Matches any one of the characters inside the brackets.                                                                                                      | `"[abc]"` matches `"a"`, `"b"`, or `"c"`         | Matches a single character from the set `a`, `b`, or `c`.                                                       |
|                        | `[^abc]`               | Matches any character **not** listed inside the brackets.                                                                                                   | `"[^abc]"` matches `"d"`, `"1"`, `"%“`, etc.     | The `^` inside `[]` negates the character class.                                                                 |
|                        | `[a-zA-Z]`             | Matches any uppercase or lowercase letter.                                                                                                                  | `"[a-zA-Z]"` matches `"a"`, `"Z"`, etc.          | Matches any single letter from `a` to `z` or `A` to `Z`.                                                         |
| **Predefined Classes** | `\d`                   | Matches any digit character (equivalent to `[0-9]`).                                                                                                         | `"\\d"` matches `"5"`, `"0"`, etc.               | The backslash `\` is escaped in Java strings, hence `"\\d"`.                                                    |
|                        | `\D`                   | Matches any non-digit character.                                                                                                                             | `"\\D"` matches `"a"`, `"-"`, etc.               | Uppercase `\D` is the negation of `\d`.                                                                          |
|                        | `\w`                   | Matches any word character (letters, digits, and underscores).                                                                                             | `"\\w"` matches `"a"`, `"1"`, `"_"`, etc.        | Equivalent to `[a-zA-Z0-9_]`.                                                                                    |
|                        | `\W`                   | Matches any non-word character.                                                                                                                              | `"\\W"` matches `"@"`, `"#"`, etc.               | Uppercase `\W` is the negation of `\w`.                                                                          |
|                        | `\s`                   | Matches any whitespace character (spaces, tabs, line breaks).                                                                                              | `"\\s"` matches `" "`, `"\t"`, `"\n"`, etc.      |                                                                                                                  |
|                        | `\S`                   | Matches any non-whitespace character.                                                                                                                        | `"\\S"` matches `"a"`, `"1"`, `"!"`, etc.        | Uppercase `\S` is the negation of `\s`.                                                                          |
| **Anchors**            | `^`                    | Asserts the start of a line/string.                                                                                                                          | `"^Hello"` matches `"Hello World"`.              | Ensures that the pattern starts matching from the beginning of the input.                                        |
|                        | `$`                    | Asserts the end of a line/string.                                                                                                                            | `"World$"` matches `"Hello World"`.              | Ensures that the pattern matches up to the end of the input.                                                     |
| **Quantifiers**        | `*`                    | Matches the preceding element **0 or more** times.                                                                                                        | `"a*"` matches `""`, `"a"`, `"aa"`, etc.          |                                                                                                                  |
|                        | `+`                    | Matches the preceding element **1 or more** times.                                                                                                         | `"a+"` matches `"a"`, `"aa"`, etc., but not `""`  |                                                                                                                  |
|                        | `?`                    | Matches the preceding element **0 or 1** time.                                                                                                             | `"a?"` matches `""` or `"a"`.                     |                                                                                                                  |
|                        | `{n}`                  | Matches exactly `n` occurrences of the preceding element.                                                                                                  | `"a{3}"` matches `"aaa"`.                         |                                                                                                                  |
|                        | `{n,}`                 | Matches `n` or more occurrences of the preceding element.                                                                                                  | `"a{2,}"` matches `"aa"`, `"aaa"`, etc.          |                                                                                                                  |
|                        | `{n,m}`                | Matches between `n` and `m` occurrences of the preceding element.                                                                                          | `"a{1,3}"` matches `"a"`, `"aa"`, `"aaa"`.        |                                                                                                                  |
| **Groups and Ranges**  | `(abc)`                | **Capturing Group**: Groups multiple tokens together and remembers the matched text.                                                                        | `"(abc)"` in `"abc123"` captures `"abc"`.         | Allows you to extract or reference specific parts of the matched string.                                        |
|                        | `(?:abc)`              | **Non-Capturing Group**: Groups multiple tokens without remembering the matched text.                                                                      | `"(?:abc)"` in `"abc123"` matches `"abc"`.        | Useful for grouping without capturing, which can improve performance.                                          |
|                        | `a|b`                  | **Alternation**: Matches either `a` or `b`.                                                                                                                | `"cat|dog"` matches `"cat"` or `"dog"`.           | Acts like a logical OR operator.                                                                                  |
|                        | `[a-z]`                | **Range**: Matches any single character from `a` to `z`.                                                                                                   | `"[A-Z]"` matches any uppercase letter.           |                                                                                                                  |
| **Assertions**         | `(?=...)`              | **Positive Lookahead**: Asserts that what follows matches the pattern inside `(...)` without including it in the match.                                     | `"\\d(?= dollars)"` matches a digit before `" dollars"`. | Ensures that a certain pattern follows without consuming characters.                                           |
|                        | `(?!...)`              | **Negative Lookahead**: Asserts that what follows does **not** match the pattern inside `(...)`.                                                          | `"\\d(?! dollars)"` matches a digit not followed by `" dollars"`. | Ensures that a certain pattern does not follow without consuming characters.                                      |
|                        | `(?<=...)`             | **Positive Lookbehind**: Asserts that what precedes matches the pattern inside `(...)` without including it in the match.                                   | `"(?<=\$)\\d+"` matches digits preceded by `$`.  | Ensures that a certain pattern precedes without consuming characters.                                           |
|                        | `(?<!...)`             | **Negative Lookbehind**: Asserts that what precedes does **not** match the pattern inside `(...)`.                                                          | `"(?<!\$)\\d+"` matches digits not preceded by `$`. | Ensures that a certain pattern does not precede without consuming characters.                                     |
| **Special Constructs** | `\b`                   | **Word Boundary**: Matches a position between a word character and a non-word character.                                                                      | `"\\bword\\b"` matches `"word"` as a whole word.  | Useful for matching whole words.                                                                                   |
|                        | `\B`                   | **Non-Word Boundary**: Matches a position where `\b` does not, i.e., between two word characters or two non-word characters.                               | `"\\Bend"` matches `"bend"` in `"append"`.       |                                                                                                                  |
|                        | `\A`                   | **Start of Input**: Matches the beginning of the input. Similar to `^` but does not respect multiline mode.                                                 | `"\\AHello"` matches `"Hello World"` only if it starts at the beginning. | Useful when dealing with multiline strings where `^` can match the start of any line.                              |
|                        | `\Z`                   | **End of Input**: Matches the end of the input but before the final line terminator. Similar to `$`.                                                          | `"World\\Z"` matches `"Hello World"` only if it ends the input. | Useful when dealing with multiline strings where `$` can match the end of any line.                                |
| **Escape Sequences**   | `\\`                   | Escapes a special character to match it literally.                                                                                                          | `"\\."` matches a literal dot (`.`).              | In Java strings, backslashes must be escaped, hence `"\\."` represents the regex `\.`.                            |
| **Shorthand Classes**  | `\p{Lower}`            | Matches any lowercase letter.                                                                                                                               | `"\\p{Lower}"` matches `"a"`, `"b"`, etc.         | Unicode property for lowercase letters.                                                                           |
|                        | `\p{Upper}`            | Matches any uppercase letter.                                                                                                                               | `"\\p{Upper}"` matches `"A"`, `"B"`, etc.         | Unicode property for uppercase letters.                                                                           |
|                        | `\p{ASCII}`            | Matches any ASCII character.                                                                                                                                | `"\\p{ASCII}"` matches characters from `\x00` to `\x7F`. | Unicode property for ASCII characters.                                                                             |
|                        | `\p{Alpha}`            | Matches any alphabetic character.                                                                                                                            | `"\\p{Alpha}"` matches `"a"`, `"B"`, etc.         | Unicode property for alphabetic characters.                                                                       |
| **Flags**              | `(?i)`                 | **Case-Insensitive**: Makes the regex case-insensitive.                                                                                                   | `"(?i)hello"` matches `"HELLO"`, `"hello"`, etc.  | Can be placed at the start of the regex or set via `Pattern` flags.                                              |
|                        | `(?m)`                 | **Multiline**: Changes `^` and `$` to match the start and end of each line.                                                                                | `"(?m)^Hello"` matches `"Hello"` at the start of any line. | Enables multiline mode where `^` and `$` match the start and end of lines, not just the entire input.               |
|                        | `(?s)`                 | **Dotall**: Makes `.` match all characters, including line terminators.                                                                                     | `"(?s)a.*c"` matches `"a\nb\nc"`.                | Enables dotall mode where `.` matches every character, including newline characters.                               |
| **Examples**           |                        |                                                                                                                                                             |                                                 |                                                                                                                  |

---

## **Java-Specific Notes**

1. **Escaping Backslashes (`\`):**
   - In Java string literals, the backslash (`\`) is an escape character. To include a literal backslash in a regex, you need to escape it with another backslash. For example:
     - Regex: `\d` (matches a digit)
     - Java String: `"\\d"`

2. **Compiling Patterns:**
   - Use the `Pattern` class to compile a regex.
   - Example:
     ```java
     Pattern pattern = Pattern.compile("\\d+");
     ```
     
3. **Matching with `Matcher`:**
   - Use the `Matcher` class to perform match operations.
   - Example:
     ```java
     Matcher matcher = pattern.matcher("12345");
     if (matcher.matches()) {
         System.out.println("It's a number!");
     }
     ```

4. **Flags:**
   - Flags can be set either inline within the regex (e.g., `(?i)` for case-insensitive) or as parameters in `Pattern.compile`.
   - Example with `Pattern.compile` flags:
     ```java
     Pattern pattern = Pattern.compile("hello", Pattern.CASE_INSENSITIVE);
     ```

---

## **Common Regular Expressions in Java**

| **Use Case**             | **Regex Pattern**                                    | **Description**                                              |
|--------------------------|------------------------------------------------------|--------------------------------------------------------------|
| **Email Validation**     | `^[A-Za-z0-9+_.-]+@[A-Za-z0-9.-]+$`                  | Validates basic email format.                                |
| **Phone Number**         | `^\\(\\d{3}\\) \\d{3}-\\d{4}$`                       | Validates phone numbers like `(123) 456-7890`.              |
| **URL Validation**       | `^(https?|ftp)://[^\\s/$.?#].[^\\s]*$`                | Validates URLs starting with `http`, `https`, or `ftp`.      |
| **IPv4 Address**         | `^(\\d{1,3}\\.){3}\\d{1,3}$`                         | Validates IPv4 addresses like `192.168.1.1`.                 |
| **Hex Color Code**       | `^#([A-Fa-f0-9]{6}|[A-Fa-f0-9]{3})$`                | Validates hex color codes like `#FFFFFF` or `#FFF`.          |
| **Strong Password**      | `^(?=.*[A-Z])(?=.*\\d)(?=.*[@#$%^&+=]).{8,}$`        | Ensures at least one uppercase letter, one digit, one special character, and minimum 8 characters. |
| **Date (YYYY-MM-DD)**    | `^\\d{4}-\\d{2}-\\d{2}$`                             | Validates dates in `YYYY-MM-DD` format.                      |
| **Extract Numbers**      | `"\\d+"`                                             | Finds sequences of digits within a string.                   |
| **Whitespace Trim**      | `"^\\s+|\\s+$"`                                      | Matches leading and trailing whitespace for trimming.        |
| **Username Validation**  | `^[A-Za-z0-9_]{3,15}$`                               | Validates usernames with 3-15 alphanumeric characters or underscores. |

---

## **Examples in Java**

### **1. Validating an Email Address**

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class EmailValidator {
    public static void main(String[] args) {
        String regex = "^[A-Za-z0-9+_.-]+@[A-Za-z0-9.-]+$";
        Pattern pattern = Pattern.compile(regex);
        
        String email = "user@example.com";
        Matcher matcher = pattern.matcher(email);
        
        if (matcher.matches()) {
            System.out.println("Valid email address.");
        } else {
            System.out.println("Invalid email address.");
        }
    }
}
```

### **2. Extracting the Area Code from a Phone Number**

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class ExtractAreaCode {
    public static void main(String[] args) {
        String regex = "\\((\\d{3})\\) \\d{3}-\\d{4}";
        Pattern pattern = Pattern.compile(regex);
        
        String phoneNumber = "(123) 456-7890";
        Matcher matcher = pattern.matcher(phoneNumber);
        
        if (matcher.matches()) {
            String areaCode = matcher.group(1);
            System.out.println("Area code: " + areaCode);
        } else {
            System.out.println("Invalid phone number.");
        }
    }
}
```

### **3. Finding All Digits in a String**

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class FindDigits {
    public static void main(String[] args) {
        String regex = "\\d+";
        Pattern pattern = Pattern.compile(regex);
        
        String input = "Order number: 12345, Date: 2024-10-08";
        Matcher matcher = pattern.matcher(input);
        
        while (matcher.find()) {
            System.out.println("Found number: " + matcher.group());
        }
    }
}
```

---

## **Tips for Working with Regex in Java**

1. **Use Verbose Patterns for Readability:**
   - Break down complex regex patterns using whitespace and comments with the `(?x)` flag.
   - Example:
     ```java
     String regex = "(?x)                  # Enable comments and whitespace
                     ^\\d{4}-\\d{2}-\\d{2}$ # Date in YYYY-MM-DD format";
     Pattern pattern = Pattern.compile(regex);
     ```

2. **Precompile Patterns for Efficiency:**
   - If you're using the same regex multiple times, compile it once and reuse the `Pattern` object.
     ```java
     Pattern emailPattern = Pattern.compile("^[A-Za-z0-9+_.-]+@[A-Za-z0-9.-]+$");
     Matcher matcher = emailPattern.matcher(email);
     ```

3. **Use `String.matches()` for Simple Checks:**
   - For straightforward validations, you can use the `matches` method directly on strings.
     ```java
     boolean isValid = email.matches("^[A-Za-z0-9+_.-]+@[A-Za-z0-9.-]+$");
     ```

4. **Escaping Special Characters:**
   - Remember to escape backslashes (`\`) and double quotes (`"`) in Java string literals.
   - Example: To match a literal dot (`.`), use `"\\."` in the Java string.

5. **Testing Regex:**
   - Use online tools like [regex101.com](https://regex101.com/) or [RegExr](https://regexr.com/) to test and debug your regex patterns before implementing them in Java.

---

## **Conclusion**

Regular expressions are a powerful tool for pattern matching and text manipulation in Java. Understanding the regex syntax and how to implement it in Java will allow you to perform complex string operations efficiently. Use this reference table as a quick guide to common regex patterns and their usage in Java applications.

If you have any specific regex needs or further questions, feel free to ask!
