## Model View Controller in NodeJS | MVC Pattern

**source**: https://www.youtube.com/watch?v=JLtXoru-ipo

### Model View Controller:

- Build upon three components:
  1. Model: updates the View.
  2. View: contains view.
  3. Controller: manipulates the model.

### Directories and Files Structures:

- Directories:

  1. models
  2. controllers
  3. routes
  4. views

- file: `index.js`: contains our overview of the app.

- we'll store the models under `models` directory.

  - for example, if we have a model for user:
    - then we'll create a file called `user.js`, contains our model. then
      `module.exports = User`.

- for `routes` we'll create routes for required functionality under routes dir.

  - for example routes for user operations, we'll create `user.js`:
    - `user.js` contains all users route and define `router` there, then
      export your router like `module.exports = router`

- in your `index.js` file, import your routes.
