# CSS

## CSS triangle

How to create a triangle with pure CSS

```css
.left-arrow {
  border-color: transparent black;
  border-style: solid;
  border-width: 20px 20px 20px 0px;
  height: 0px;
  width: 0px;
}

.right-arrow {
  border-color: transparent black;
  border-style: solid;
  border-width: 20px 0px 20px 20px;
  height: 0px;
  width: 0px;
}

.down-arrow {
  border-color: black transparent;
  border-style: solid;
  border-width: 20px 20px 0px 20px;
  height: 0px;
  width: 0px;
}

.up-arrow {
  border-color: black transparent;
  border-style: solid;
  border-width: 0px 20px 20px 20px;
  height: 0px;
  width: 0px;
}
```

## hidden elements for accessibility

A useful class for hidden visual element and let the screen reader see the elements

```css
.visuallyhidden {
  border: 0;
  clip: rect(0 0 0 0);
  height: 1px;
  margin: -1px;
  overflow: hidden;
  padding: 0;
  position: absolute;
  width: 1px;
  left: 103px;
  top: 71px;
}
```
