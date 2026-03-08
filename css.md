
````md
# CSS Notes

## Selectors

### 1. Simple Selectors
Select elements based on name, id, or class.

- **Element selector** → `elementName`
- **ID selector** → `#id`  
  - Must be **unique per page**
- **Class selector** → `.className`

Example:

```css
p {
  color: red;
}

#header {
  background: blue;
}

.container {
  padding: 10px;
}
````

---

### 2. Combinator Selectors

Select elements based on **relationships between elements**.

Examples:

```css
p.className
```

Selects **only `p` elements** having class `className`.

```css
div, p
```

Applies styles to **both `div` and `p` elements**.

```css
div p
```

Selects **paragraphs inside a `div`**.

---

### 3. Pseudo Classes

Select elements based on **their state**.

Examples:

* `:hover`
* `:active`
* `:focus`
* `:visited`

Example:

```css
a:hover {
  color: red;
}
```

---

### 4. Pseudo Elements

Select elements based on **position or part of an element**.

Examples:

* `::first-letter`
* `::first-line`
* `::before`
* `::after`
* `:nth-child()`

Example:

```css
p::first-letter {
  font-size: 30px;
}
```

---

### 5. Attribute Selectors

Select elements based on **their attributes or attribute values**.

Example:

```css
input[type="text"] {
  border: 1px solid gray;
}
```

---

# Background Properties

Example:

```css
body {
  background-image: url("img_tree.png");
  background-repeat: no-repeat;
  background-position: right top;
  background-attachment: scroll;
}
```

### Background Shorthand

```css
background: color image repeat position attachment;
```

Example:

```css
background: #fff url("img.png") no-repeat center fixed;
```

---

# Height and Width

By default, when you set **height and width**, they apply only to the **content area**, excluding:

* margin
* padding
* border

### Possible Values

| Value     | Description                              |
| --------- | ---------------------------------------- |
| `auto`    | Browser calculates size automatically    |
| `length`  | Fixed value like `px`, `em`, `rem`, `cm` |
| `%`       | Percentage of parent element             |
| `initial` | Sets to default value                    |
| `inherit` | Inherits value from parent               |

Example:

```css
div {
  width: 50%;
  height: auto;
}
```

---

# CSS Box Model

The box model consists of:

```
Margin → Border → Padding → Content
```

### `box-sizing`

By default:

```
Total Width = content + padding + border
```

Example:

If:

```
width = 100px
padding-left + padding-right = 50px
```

Actual width becomes:

```
150px
```

### Using `border-box`

```css
box-sizing: border-box;
```

Now:

```
Total width = padding + border + content
```

The **content shrinks** to maintain the defined width.

Example:

```css
div {
  width: 100px;
  padding: 20px;
  box-sizing: border-box;
}
```

---

# CSS Positioning

### 1. Static (Default)

```css
position: static;
```

* Default positioning.
* `top`, `left`, `right`, `bottom` **do not work**.

---

### 2. Relative

```css
position: relative;
```

* Positioned **relative to its normal position**.
* Leaves its **original space** in the layout.

Example:

```css
div {
  position: relative;
  top: 10px;
}
```

---

### 3. Fixed

```css
position: fixed;
```

* Positioned **relative to the viewport**.
* **Does not leave space** in normal flow.
* Stays fixed during scrolling.

Example:

```css
header {
  position: fixed;
  top: 0;
}
```

---

### 4. Absolute

```css
position: absolute;
```

* Positioned relative to the **nearest positioned ancestor**.
* If none exists → positioned relative to **body**.
* **Removed from normal document flow**.
* Can **overlap other elements**.

Example:

```css
div {
  position: absolute;
  top: 50px;
  left: 20px;
}
```

---
