# Class 01

## Topic: sed command

- used to modify the output.

- sample command to print the matching line number:

```
sed -n '1,2p' /etc/passwd
```

- printing the matching pattern.

**testing the command in our copied passwd file**:
```
sed '/bash/p' passwd
```

> `p` option to print and `d` option to delete.

- deleting empty line, the take `^$` together.

- taking multiple string matches in sed:

**two patterns**:
```
sed -n '/colord\|billu/p' passwd
```

**three patterns**:
```
sed -n '/PATTERN1\|PATTERN2\|PATTERN3/p' filename
```

- `-n` is only prints the specified line.


# Class 02

## Topic: Active Directory Domain Services (ADDS):

- ADDS Features:
    1. Centralized
    2. 
    3. Single Point of Access to Network Resources
    4. Hierarchical Organization Structure
        - Forests
        - Trees
        - Domains
        - Organizational Units (OUs)
    5. Single Sign-On (SSO)
    6. Group Policy Management

#### Logical Components of ADDS

1. `Domains`: Basic unit containing users, computers and policies.
2. `OUs`: like you have different departments in ADDS.


##### Right Management:

- Add ADDS from roles and features.
- If you do not have existing forest create a new one:
    - provide the forest name with the TLD (i.e.): `armour.local`
    - Enabling GC and DNS services by default.
    - Setup and Restore Mode Password.

## To Study:

- remember the AD DS database, files and configs paths.
