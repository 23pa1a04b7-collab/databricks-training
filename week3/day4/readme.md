    REGEX BASIC ASSIGNMENY.docx
 # REGEX FOUNDATION ASSIGNMENT

## Q1. How do you extract digits using Regex?

Answer:

Regex:
```sql
[0-9]
```

Example Input:
```text
123ABc
```

Output:
```text
1
```

Explanation:
Matches any single digit from 0 to 9.

---

## Q2. How do you extract alphabets using Regex?

Answer:

Regex:
```sql
[A-Za-z]
```

Example Input:
```text
123ABc
```

Output:
```text
A
```

Explanation:
Matches uppercase and lowercase alphabets.

---

## Q3. What is the use of ^ (Start of String)?

Answer:

Regex:
```sql
^[0-9]
```

Example:
```text
123abc → 1
abc123 → No Output
```

Explanation:
Checks whether the string starts with a digit.

---

## Q4. What is the use of $ (End of String)?

Answer:

Regex:
```sql
[0-9]$
```

Example:
```text
123abc → No Output
abc123 → 3
```

Explanation:
Checks whether the string ends with a digit.

---

## Q5. How do you extract exactly 2 digits?

Answer:

Regex:
```sql
[0-9]{2}
```

Input:
```text
12345678abc
```

Output:
```text
12
```

---

## Q6. How do you extract exactly 2 alphabets?

Answer:

Regex:
```sql
[a-zA-Z]{2}
```

Input:
```text
abcdefghi123
```

Output:
```text
ab
```

---

## Q7. What is the use of + in Regex?

Answer:

Regex:
```sql
[0-9]+
```

Example:
```text
123abc → 123
abc123 → 123
```

Explanation:
Returns one or more continuous matching digits.

---

## Q8. How do you extract continuous alphabets?

Answer:

Regex:
```sql
[a-zA-Z]+
```

Input:
```text
abc123
```

Output:
```text
abc
```

---

## Q9. Explain the Principle of Continuity in Regex.

Answer:

Regex:
```sql
[0-9]+
```

Input:
```text
123abc567
```

Output:
```text
123
```

Explanation:
Regex stops matching when continuity breaks.

---

## Q10. How do you extract digits and alphabets together?

Answer:

Regex:
```sql
[0-9a-zA-Z]+
```

Input:
```text
123abc567
```

Output:
```text
123abc567
```

---

## Q11. How do you extract digits from the middle of a string?

Answer:

Regex:
```sql
[0-9]+
```

Input:
```text
abc123gef
```

Output:
```text
123
```

---

## Q12. How do you extract the domain part from an email?

Answer:

Regex:
```sql
@[a-zA-Z.]+
```

Input:
```text
karthik@gmail.com
```

Output:
```text
@gmail.com
```

---

## Q13. How do you extract the top-level domain from an email?

Answer:

Regex:
```sql
\.[a-zA-Z]+$
```

Input:
```text
karthik@gmail.com
```

Output:
```text
.com
```

---

## Q14. How do you validate an Indian phone number with country code?

Answer:

Regex:
```sql
\+91-[0-9]{10}
```

Input:
```text
+91-9989454737
```

Output:
```text
+91-9989454737
```

---

## Q15. How do you remove @ from an email domain using MySQL?

Answer:

```sql
REPLACE(
REGEXP_SUBSTR(email,'@[a-zA-Z.]+'),
'@',
''
)
```

Output:
```text
gmail.com
```

---

## Q16. What are the three parts of an email?

Answer:

```text
username @ domain . extension
```

Example:

```text
karthik.kumar44@gmail.com
```

---

## Q17. What is the regex for the username part of an email?

Answer:

```sql
[a-zA-Z0-9._-]+
```

---

## Q18. What is the regex for the domain name part?

Answer:

```sql
[a-zA-Z0-9]+
```

---

## Q19. What is the regex for the domain extension part?

Answer:

```sql
[a-zA-Z]{2,3}
```

---

## Q20. Write the complete Email Validation Regex.

Answer:

```sql
[a-zA-Z0-9._-]+@[a-zA-Z0-9]+\.[a-zA-Z]{2,3}
```   
