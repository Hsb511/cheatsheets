# Basic metacharacters
```regex
|   # Posix extended
^
$
\
.   # Wildcard everything but \n
```

# Quantification
```regex
*
?   # Posix extended
+   # Posix extended
{6}
{2,3}
```

# Class
```regex
[aeo]
[a-zA-Z0-1]
[^4-9]
\d  \D
\w  \W
\s  \S
```

# Grouping
```regex
()
\n
```

# Lookahead and lookbehind assertions
| Assertion | lookbehind | lookahead |
|-----------|------------|-----------|
| Positive  |  (?<=<ins>***pattern***</ins>) |  (?=<ins>***pattern***</ins>) |
| Negative  |  (?<!<ins>***pattern***</ins>) |  (?!<ins>***pattern***</ins>) |

