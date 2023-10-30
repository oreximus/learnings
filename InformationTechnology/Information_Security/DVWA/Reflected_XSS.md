## Reflected XSS Findings on DVWA

- Setting up to the "Low" Difficulty Mode.

- Then Choosing XSS(Reflected)

- Notice the Query String the URL bar.

- and if there is any changes happening to the page.

- Try to injecting the HTML code in any input we available to make changes.

- Running our scripting example:

```
<script>alert(1)</script>robin
```

- If the script dosen't work then, try making change with tags letter case.

- Try HTML event attributes for making possible to run scripts inside them.

- Which eventually make event to check whether what is happening after that our script will execute:

```
<img src="x" onerro="alert(1)">robin
```

## Terms and Definitions:

### What is Reflected XSS

- Reflected XSS is a kind of cross-site scripting attack, where malicious script is injected into websites that are trusted or otherwise benign.


