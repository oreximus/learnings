# Class 01

## Topic: awk command:

### NF (number of fields):


- print the numbers of fields in the sentence:
```
echo "there is some sentence" | awk '{print NF}'
```

- print the desired number of fields from the awk NF:
```
cat /etc/passwd | awk '{print $1, $(NF-1), $NF}'
```

- printing out the number of fields of the `ifconfig` command:

```
ifconfig | awk '{print NF}'
```

- printing the number of records/lines of command output:

```
cat /etc/passwd | awk '{print NR}'
```

- printing the number of fields in the line number through awk:

```
cat /etc/passwd | awk '{print "Number of fields" " " NF " " "in the line" " " NR}'
```

- using separator in awk:

```
echo "one two three four" | awk 'BEGIN {FS="-"} {print $0}'
```

### NR (number of records):

- record separator:

```
cat /etc/passwd | awk 'BEGIN{RS=":"} {print $0}'
```

# Class 02

## Topic: Group Policy

- Hiding the `This PC Drives`:
    - User Configuration --> Administrative Templates --> Windows Components --> File Explorer --> Hide from My Computer(like this...)

- Likewise do prevent access the drives via cmd.
    - Same path --> Prevent access from the command prompt


## Homework:

- to provide the ways to stop the data leakage by the employees or workers.
- how to bypass USB blockage in windows client

## Learn about:

- MDM (Mobile Device Management)
- MAM (Mobile Application Management)
