# Class 28: Advanced Linux grep

## Topic: Advanced grep Patterns and Usage

### Basic Pattern Filtering

- removing all of the empty lines:
```
grep -v '^$' file-name
```

- removing the comments:
```
grep -v '^#' file-name
```

- removing both empty lines and comments:
```
grep -v '^#' file-name | grep -v '^$'
```

- without using pipe command, removing empty lines and comments:
```
grep -Ev "(^# | ^$)" file-name
```

- filtering contents starting with `log`:
```
grep '^log' file-name
```

### Character Class Filtering

- filtering a or n from the file:
```
grep "[an]" file-name
```

- for alphabets letters filters:
```
grep "[[:alpha:]]" filename
```

- for alphabets and numbers filters:
```
grep "[[:alphanum:]]" filename
```

- for alphabets capital letters filters:
```
grep "[[:upper:]]" filename
```

- for alphabets lowercase letters filters:
```
grep "[[:lower:]]" filename
```

- for number filters:
```
grep "[[:number:]]" filename
```

### Command Output Filtering

- filtering `inet` from ifconfig command:
```
ifconfig | grep 'inet '
```

- filtering processes:
**filtering processes running from root**:
```
ps -aux | grep '^root'
```

**filtering processes not running via root**:
```
ps -aux | grep -v '^root'
```

### Advanced Pattern Matching

- filtering particular pattern under a directory recursively with line numbers:
```
grep -inr "/path/" 2>/dev/null
```

- filtering particular pattern under a directory recursively, showing only filenames:
```
grep -ilR "/path/" 2>/dev/null
```

- matching only four digit numbers:
```
grep [0-9][0-9][0-9][0-9] /etc/passwd -o
```

### Pattern Length and Character Specifications

**containing single character after it**:
```
grep "name." filename
```

**containing double character after it**:
```
grep "name.." filename
```

**containing triple character after it**:
```
grep "name..." filename
```

- filtering numbers after matched string/character:
```
grep "name[0-9][0-9][0-9]" filename
```

- filtering lowercase alphabets:
```
grep [a-z] filename
```

- filtering case-insensitive alphabets:
```
grep -i [a-z] filename
```

- filtering number starting with specific number:
```
grep "9[0-9][0-9]" filename
```

- matching files content patterns:
```
grep -f file-with-the-pattern file-to-match-the-pattern
```

