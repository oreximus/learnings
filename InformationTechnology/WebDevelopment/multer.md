## Uploading Files with NodeJS and Multer

**source**: https://www.youtube.com/watch?v=WqJ0P8JnftI

- we creating a node application with views so that we can test the UI with the
  server.

- create a node project and in the `index.js` file:

```
const path = require("path");
const express = require("express");

const app = express();
const PORT = 8000;

app.set("view engine", "ejs");
app.set("views", path.resolve("./views"));

app.use(express.json());

app.get("/", (req, res) => {
    return res.render("homepage");
});

app.listen(PORT, () => console.log(`Server Started at PORT:8000`));
```

- this will create the basic structure of the server where we can work on the
  basic UI layout in the `homepage.ejs` file and work on the testing logic in
  `index.js` file

```
// importing multer

const multer = require("multer");

const upload = multer({dest: "uploads/"});

// POST route

app.post("/upload", upload.single("profileImage"), (req, res) => {
    console.log(req.body);
    console.log(req.file);

    return res.redirect("/");
});
```

- above example will upload and save the file in `/upload` directory but it'll
  corrupt the name of the file, so for uploading file according to us we'll tweak
  the code:

```
// creating a storage

const storage = multer.diskStorage({
    destination: function (req, file, cb) {
        return cb(null, './uploads');
    },
    filename: function (req, file, cb) {
        return cb(null, `${Date.now()}-${file.originalname}`);
    },
})

const upload = multer({ storage })
```

> it's important to provide the `enctype` in the form otherwise the file will not going get uploaded.
