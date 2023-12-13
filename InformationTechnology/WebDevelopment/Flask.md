# Flask Notes

## Flask Authentication

- Using Flask-Login

### source: https://www.youtube.com/watch?v=71EU8gnZqZQ

**Installing Packages**

### For Linux

```
pip install flask-login
```

**Folders and Files we need**:

- writing codes in **app.py** file;

- we need two folders:
    1. **templates**: where our html will go!
    2. **static**: where out css code will go!

**app.py**

```
from flask import Flask

app = Flask(__name__)


@app.route('/')
def home():
    return "Hello from Flask!"


if __name__ = '__main__'
    app.run(debug=True)
```
