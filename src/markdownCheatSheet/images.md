title: Markdown CheatSheet For MkDocs - Images
description: Markdown cheatSheet for MkDocs. Images examples and simple usage

# Images

Images have a similar syntax to [links](links.md "links markdowns") but include a preceding exclamation point.  
==All images will render in original size if not specified otherwise.==

## Embedding Images

```markdown
![minion](https://octodex.github.com/images/minion.png)
```

__Result:__
![minion](https://octodex.github.com/images/minion.png )

Embedding  Images with width attributes:  
> :bulb: __"hight" attributes is not needed__

```markdown
<img src="https://octodex.github.com/images/minion.png" width=200>
```

__Result:__  
<img src="https://octodex.github.com/images/minion.png" width=200>

## Inline Image With Text

```markdown
Inline ![minion](../assets/images/example/minion100x100.png) With Relative Link

Inline <img src="https://octodex.github.com/images/minion.png" width=50> With Reference Link
```

__Result:__  
Inline ![minion](../assets/images/example/minion100x100.png) With Relative Link

Inline <img src="https://octodex.github.com/images/minion.png" width=50> With Reference Link

## Block Quotes with Image

```markdown
> :camera: __Figure Title__  
> ![minion](../assets/images/example/minion500x500.png)
```

__Result:__  
> :camera: __Figure Title__  
> ![minion](../assets/images/example/minion500x500.png)

