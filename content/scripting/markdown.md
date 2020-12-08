---
title: "Markdown Cheatsheet"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

# Markdown Cheatsheet

---

### Headings size

# Heading 1
    Markup :  # Heading 1
## Heading 2
    Markup :  ## Heading 2
### Heading 3
    Markup :  ### Heading 3
#### Heading 4
    Markup :  #### Heading 4
##### Heading 5
    Markup :  ##### Heading 5
###### Heading 6
    Markup :  ###### Heading 6

---

### Text formatting

Common text

    Markup :  Common text

_Emphasized text_

    Markup :  _Emphasized text_ or *Emphasized text*

~~Strikethrough text~~

    Markup :  ~~Strikethrough text~~

__Strong text__

    Markup :  __Strong text__ or **Strong text**

___Strong emphasized text___

    Markup :  ___Strong emphasized text___ or ***Strong emphasized text***
    
---

### Lists

* Bullet list
    * Nested bullet
        * Sub-nested bullet etc
* Bullet list item 2

```
 Markup : * Bullet list
              * Nested bullet
                  * Sub-nested bullet etc
          * Bullet list item 2
```

-- unordered list  
-- unordered list  

```
Markup: -- unordered list  
        -- unordered list  
```

1. A numbered list
    1. A nested numbered list
    2. Which is numbered
2. Which is numbered

```
 Markup : 1. A numbered list
              1. A nested numbered list
              2. Which is numbered
          2. Which is numbered
```

- [ ] An uncompleted task
- [x] A completed task

```
 Markup : - [ ] An uncompleted task
          - [x] A completed task
```

---

### Web links

[Named Link](http://www.google.fr/) and http://www.google.fr/ or <http://example.com/>

    Markup :  [Named Link](http://www.google.fr/) and http://www.google.fr/ or <http://example.com/>

_Image with alt :_

![picture alt](thethaw_header.jpg "Title is optional")

    Markup : ![picture alt](thethaw_header.jpg "Title is optional")

---

### Table formatting

Table, like this one :

First Header  | Second Header
------------- | -------------
Content Cell  | Content Cell
Content Cell  | Content Cell

```
First Header  | Second Header
------------- | -------------
Content Cell  | Content Cell
Content Cell  | Content Cell
```

---

### Code and quotes

Parellel views: `right click` + `New View for Notebook`

> blockquote  
many lines
>> Nested blockquote

    Markup :  > Blockquote
              >> Nested Blockquote
              
Type some `inline code` 

    Markup :  `code()`

``` 
code blocks between 3 backticks
```


```javascript
    var specificLanguage_code = 
    {
        "data": {
            "lookedUpPlatform": 1,
            "query": "Kasabian+Test+Transmission",
            "lookedUpItem": {
                "name": "Test Transmission",
                "artist": "Kasabian",
                "album": "Kasabian",
                "picture": null,
                "link": "http://open.spotify.com/track/5jhJur5n4fasblLSCOcrTp"
            }
        }
    }
```

    Markup : ```javascript
             ```
         
---

### Line

_Horizontal line :_
- - -

    Markup : --- or - - - (latter under title)

--- 

### Foldable text

<details>
  <summary>Title 1</summary>
  <p>Content 1 Content 1 Content 1 Content 1 Content 1</p>
</details>
<details>
  <summary>Title 2</summary>
  <p>Content 2 Content 2 Content 2 Content 2 Content 2</p>
</details>

    Markup : <details>
               <summary>Title 1</summary>
               <p>Content 1 Content 1 Content 1 Content 1 Content 1</p>
             </details>

---

### Keys and shortcuts

<kbd>⌘F</kbd>

<kbd>⇧⌘F</kbd>

    Markup : <kbd>⌘F</kbd>

Hotkey list:

| Key | Symbol |
| --- | --- |
| Option | ⌥ |
| Control | ⌃ |
| Command | ⌘ |
| Shift | ⇧ |
| Caps Lock | ⇪ |
| Tab | ⇥ |
| Esc | ⎋ |
| Power | ⌽ |
| Return | ↩ |
| Delete | ⌫ |
| Up | ↑ |
| Down | ↓ |
| Left | ← |
| Right | → |

--- 

### Emoji

:exclamation: Use emoji icons to enhance text. :+1:  Look up emoji codes at [emoji-cheat-sheet.com](http://emoji-cheat-sheet.com/)

    Markup : Code appears between colons :EMOJICODE:
    
---

### Math
Some math $\int x^2 dx$ 
~~~
$\int x^2 dx$ 
~~~
    