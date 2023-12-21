## About CSS
- Styling Language
- Used for Presentation
- Creativity Focused

## CSS Syntax


- Decription:
```
selector {
    property1: value;
    property2: value;
}
```

- Example:
```
h1 {
    color: blue;
}
```

## CSS Selectors

1. Element
2. Class
3. ID

1. Element Selector Example:
```
h1 {
    color: blue;
}
```

2. Class Selector

- You can modify the properties by calling the class name you defined in the HTML!
```

// Example Class Definition
<h1 class="big-header">
    Title
</h1>

// In CSS

.class-name{
    property: value;
}
```

- Example for Different Buttons color:

```
// In HTML

<button class="btn btn-1">
buttun 1
</button>

<button class="btn btn-2">
buttun 2
</button>

<button class="btn btn-3">
buttun 3
</button>

// In CSS

.btn {
    padding: 10px;
    color: white;
}

.btn-1 { background-color: green }
.btn-2 { background-color: blue }
.btn-3 { background-color: purple }
```

3. ID Selector

- It should be unique in the Entire Webpage!

```
// In HTML
<h1> id="main-header">
    Title
</h1>

// In CSS

#id {
    property: value;
}
```

### CSS Selector Combination

- Examples:
    - For combining H1 tag with "larg-heading" class:
    ```
    // In HTML
    <h1 class="large=heading">
    Title
    </h1>

    // In CSS
    h1.large-header {
        font-size: 200%;
    }

    ```
    - For combining H2 tag with id "big=blue" and class "large blue"
    ```
    // In HTML
    <h2 id="big-blue" class="large-blue">
    Title
    </h2>

    // In CSS
    #big-blue.large.blue {
        color: blue;
        font-size: 200%;
    }
    ```
    - For combining all the <p> tags inside <div>
    ```
    // In HTML
    <div>
        <p>Selected</p>
        <p>Selected</p>
    <span>
        <p>Selected</p>
    </span>
    </div>

    // In CSS
    div p {
        color: red; 
    }
    ```
    - For Selecting the header of class "main-header" with h1 property of class "brown":
    ```
    header.main-header h1.brown {
        color:brown;
    }
    ```
    - You can combine the classes which have same properties:
    ```
    // for example class big and large has same property
    .big, .large {
        font-size: 200%; 
    }
    ```
    - When you need select every Item on the Webpage:
    - For example fonts:
    ```
    * {
        font-family: Arial;
    }
    ```

### How to Load CSS

1. **Inline Syle**, terrible Idea
2. **Syle Element**, a better Idea to mention all of the Style details inside the style element in the beginning of HTML code. And will only avaiable on the pages you use them on, Better but not the best way to use CSS.
3. **External CSS**: the best way to define the CSS, and providing the link of the CSS inside the HTML code.
    - By using **link** element in the code which a special and link css files and which has the **rel** attribute which can used to define the relationship between html file and link file.

- Whatever define at last will be implemented in the HTML.
- Importance of Selector whether they defined at anywhere!
    - ID > Class > Element (Importance in Decreasing Order)

- CSS Inline in the Element will overwrite Everything Define in the Stylesheet or Any Other Place.
- For Colors:
    - colornames.
    - hexadecimal values.
    - hsla

- useful properties to work with:
    - height - we can define the properties in pixel, percentage, em (set according to font pixels), rem(set value independently)
    - width - we can define the properties in pixel, percentage, em (set according to font pixels), rem(set value independently)
    - padding
    - margin
    - border
    - background-color
