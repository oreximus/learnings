# Class 01

## Topic: Linux Basic Command: `cut` command

## Notes:

- The `cut` command is used to extract `section from lines` of text files or input streams.

- example scenario for using `cut` command:

**command**:
```

```

**example file**:
```
id,username,first_name,last_name,email,address
1,jdoe,John,Doe,jdoe@example.com,123 Maple St, Springfield
2,asmith,Alice,Smith,asmith@example.com,456 Oak Ave, Rivertown
3,bwayne,Bruce,Wayne,bwayne@example.com,1007 Mountain Dr, Gotham
4,ckent,Clark,Kent,ckent@example.com,344 Clinton St, Metropolis
5,dprince,Diana,Prince,dprince@example.com,10 Themyscira Ln, Gateway City
6,pparker,Peter,Parker,pparker@example.com,20 Ingram St, Queens
7,tstark,Tony,Stark,tstark@example.com,10880 Malibu Point, Malibu
8,srogers,Steve,Rogers,srogers@example.com,569 Leaman Place, Brooklyn
9,nromanoff,Natasha,Romanoff,nromanoff@example.com,890 Red Room Rd, Moscow
10,bwilson,Bruce,Wilson,bwilson@example.com,77 Banner Blvd, Dayton
11,ssmith,Sam,Smith,ssmith@example.com,12 Elm St, Smalltown
12,mmartin,Mary,Martin,mmartin@example.com,98 Pine Rd, Lakeside
13,jwilson,James,Wilson,jwilson@example.com,34 Cedar Ct, Hill Valley
14,kclark,Karen,Clark,kclark@example.com,55 Willow Dr, Star City
15,rlee,Robert,Lee,rlee@example.com,81 Birch Ave, Central City
16,hpotter,Harry,Potter,hpotter@example.com,4 Privet Dr, Little Whinging
17,hgates,Henry,Gates,hgates@example.com,67 Maple St, Riverdale
18,lwayne,Laura,Wayne,lwayne@example.com,23 Oakwood Ln, Gotham
19,sallen,Sarah,Allen,sallen@example.com,11 Spruce St, Keystone
20,djohnson,David,Johnson,djohnson@example.com,90 Aspen Rd, Coast City
```

- cutting data from 1-5 characters:

```
cut -b 1-5 some_data.txt
```

**example output**:

```
1id,u
1,jdo
2,asm
3,bwa
4,cke
5,dpr
6,ppa
7,tst
8,sro
9,nro
10,bw
11,ss
12,mm
13,jw
14,kc
15,rl
16,hp
17,hg
18,lw
19,sa
20,dj
```

- using `cut` to get the value separated by the delimeter:

```
cut -d ',' -f 4 some-data.txt
```

- getting the columns data separated by delimeter for 1 and 4 columns data only:

```
cut -d ',' -f 1,4 some-data.txt
```

- skip lines that do not contain the delimeter:

```
cat passwd | cut -d ":" -f 1 some-data.txt
```

- extract the username directly from passwd:

```
cat -d 
```

- getting files extension of files output from cut:

```
cut -d '.' -f 2 --only-delimited
```

**Practing cut command on randomly formatted users data file**:

- example file content:

```
john,doe,35,New York
jane|smith|28|Los Angeles
michael   brown   42   Chicago
lisa,white,,San Francisco
samuel|adams|,Boston
  emily,clark,30,Seattle
peter\tparker\t25\tQueens
susan  |  miller  |  31  |  Miami
chris,jones,27
,alex,turner,29,London
maria,garcia, ,Madrid
tom|harris|33| 
lucy   smith   26   Houston

```

- you can provide multiple ranges in cut command:

```
cut -d ":" -f1-2,3-4 /etc/passwd
```

**ifconfig data filering using `cut`**:

- example 1

```
ifconfig | cut -f1-2 -d " "
```

- example 2

```
ifconfig | grep ether | cut -d ' ' -f 10
```

> Practice the IP address filtering using `grep` and `cut`

> Practice the patterned output for extracting data from passwd file using `cut`

# Class 02

## Topic: Workgroups, Peer-to-Peer and Point to Point Networks.

### Common Terms in Windows Networking:

- `Workgroup`: simple local network, it operates on peer-to-peer devices, in Windows Networking systems
no centralized system.

- each computers manages its own `users and permissions`.

- no centralized authentication - users must exists on each PC.

- Workgroup members must be on the `same local network/subnet`.

**Peer-to-Peer (P2P)**:

- A `decentralized network model` where each node (peer) can act as both `client and server`.
- There is `no central authority` managing communication or access.
- Designed for `resource sharing, distributed computing`, or `file exchange`.

**Point-to-Point (P2P)**:

- depends on VPN
- PPP Tunnel, PPP link,

### File systems in Windows:

1. fat32

2. NTFS

3. exFat (Extended FIle Allocation Table)

4. ReFS (Resilient File System)
