# CSS Box Model

All HTML elements can be considered to be boxes.

## The CSS Box Model

In CSS, the term box model is when talking about design and layout.
The CSS box model is essentially a box that wraps around every HTML element. It consists of margins, borders, padding and the actual content. 

Explanation of different parts:

* Content - The content of the box, where text and images appear.
* Padding - Clears an area around the content. The padding is transparent.
* Border - A border that goes around the padding and content.
* Margin - Clears an area outside the border. The margin is transparent.

## Width and Height of an Element

In order to set the width and height of an element correctly in all browsers, you need to know how the box model works.

```
div {
    width: 300px;
    padding: 10px;
    border: 5px solid gray;
    margin: 0;
}
```

Here is the calcualtion:
320px (width) + 20px (left + right padding) + 10px (left + right border) + 0px (left + right margin) = 350px.
