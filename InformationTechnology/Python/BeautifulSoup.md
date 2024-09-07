## Web Scraping Tutorial Using Python | BeautifulSoup Tutorial

**source**: https://www.youtube.com/watch?v=4tAp9Lu0eDI

### Python Packages you need:

```
pip install requests bs4
```

### Getting Started:

- Create a separate directory in some location in your computer:

```
mkdir BeautifulSoup && cd BeautifulSoup
```

- open this directory into your code editor, then create a `main.py` file.

### About BeautifulSoup:

- You can scrap the data of any website from the HTML elements of it,
  whatever the data you get from the `view-source` option you can scrap it.

### Example:

```
import requests

url = ""

def fetchAndSaveToFile(url, path):
    r = requests.get(url)
    with open(path, "w") as f:
        f.write(r.text)

r = requests.get(url)

fetchAndSavToFile(url, :data/times.html)

```

- above code will pull up the source-code of the url that will provide.

- we can for sure then scrap the data of it by using the BeautifulSoap.

### Scraping the data

- creating a `sample.html` file and then we'll scrap the data of this file
  first.

- and rename the file `main.py` to `00_fetching_data.py` so for takling the
  problem to get block while scraping the data using BeautifulSoap, we'll
  use proxy to get different IPs.

### BeautifulSoap Example:

- you can take the reference of `crummy.com` docs for BeautifulSoap Examples

- whenever you use the BeautifulSoap, do make a `soup` object first then
  do the further scraping.

- then you can print the content through `soup.prettify()` function.

- you can print the title of document using `soup.title` and also you can
  only print the title `soup.title.string`

- you can print the div using `soup.div` and for all divs using
  `soup.find_all("div")` that will fetch you up the all divs in the document
  and for printing the specific after fetching them all, use `soup.find_all("div")[0]`,
  a simple indexing after the same syntax for fetching all of the divs.

- you wrap the scraping syntax inside `type()` method which will return
  you the type of the object that is returning back after scraping the data.

- you can make loop for example to get all of the links in the document:

```
for link in soup.find_all("a"):
    print(link.get("href"))
```

- you can also filter the content by their `id` value:

```
s = soup.find(id="links")

print(s)
```

- it'll print the element by the id name _links_.

- and if you want to print only the link using in the element:

```
print(s.get("href")
```

- selecting the content with `classes` use:

```
# it'll print out all of the classes named `italic`
print(soup.select("div.italic"))
```

- selecting the content with `id` use:

```
# it'll print out the id named `italic`
print(soup.select("div#italic"))
```

- you and print all of the class names for example of a `span`:

```
print(soup.span.get("class"))
```

- finding through, for example finding an element by class name:

```
print(soup.find(id="some_id"))
```

- finding something by class, class is a reserved keyword in python,
  so we'll type `_class` for for finding something by class in BeautifulSoup:

```
// it'll print only the first element which has mentioned class name.
print(soup.find(class_="italic"))
```

```
// it'll prin all the elements which has mentioned class name.
print(soup.findall(class_="italic"))
```

- printing out the children of an element:

```
for child in soup.find(class_="container").children:
    print(child)
```

- above will printout all of the children of "container" class name.

- listing all of the parents of the element:

```
for parent in soup.find(class_="box").parents:
```

### Modyfying the Scraped Data:

- changing the class name of the
