# Kitchen Sink

What follows is some custom  formatting used by the website.

A formatted version of this file [appears on the website](https://microbit-playground.co.uk/about/how-to-contribute).

###### A note about Kramdown
microbit playground uses `kramdown` as its markdown parser. This uses `{:.}` to specify classes to attach to a block.

For Example:

```
markdown in:

    {:.ui .dividing .header}
    ### A beautiful header

HTML out:

    <h3 class="ui dividing header">A beautiful header</h3>
```

Most of semantic ui is exposed but please go easy on it!

## Headers
`### Header Three` Site hierarchy begins here.

`#### Header Four` Welcome to use this

`##### Header Five` Try to avoid!

It is possible to use a dividing header using the custom markdown of Kramdown:

```
{:.ui .dividing .header}
### Pretty Header
```

## Lists

`ol` list:
* This is
* a
* list

`ul` list:
1. number one
2. number two
3. number three

### Tables

#### Compact Basic Table
```
{:.ui .basic .collapsing .table}
| Header Cell 1 | Header Cell 2 |
|---------------|---------------|
| Accelerometer |   `0x1D`      |
|     Hello     |   `0x0E`      |
```
#### Normal Table

```
{:.ui .collapsing .table}
| Header Cell 1 | Header Cell 2 |
|---------------|---------------|
| Accelerometer |   `0x1D`      |
|     Hello     |   `0x0E`      |
```
## Code Examples

Inline code is formatted with `backticks.`

Sections of code can be formatted with triple backticks:

```
This is example of
using backticks
in markdown.
```

Code can be highlighted and made pretty. It supports any language used by [Rouge](https://github.com/jneen/rouge/wiki/List-of-supported-languages-and-lexers)

```
{% highlight ruby %}

def say(words)
  puts words
end

say("This")
say("is")
say("highlighted")
say("ruby code.")

{% endhighlight %}
```

## Images

#### A Regular Image
```
![Just a regular image](https://placeholdit.imgix.net/~text?txtsize=33&txt=350%C3%97150&w=350&h=150)
```

#### A Fluid Image
```
{:.ui .image .fluid}
![A fluid image](https://placeholdit.imgix.net/~text?txtsize=33&txt=350%C3%97150&w=350&h=150)
```

A fluid image takes up the width of the container.

#### A Medium Rounded Right Floated Image

```
{:.ui .image .medium .right .floated}
![A fluid image](https://placeholdit.imgix.net/~text?txtsize=33&txt=350%C3%97150&w=350&h=150)
```
#### A Small Left Floated Image
```
{:.ui .image .small .left .floated}
![A fluid image](https://placeholdit.imgix.net/~text?txtsize=33&txt=350%C3%97150&w=350&h=150)
```
### Tabs

These are used to show the same information side by side.

```
<!-- Top tabs -->
<div class="ui top attached tabular menu">
  <a class="item active" data-tab="first">Tab One</a>
  <a class="item" data-tab="second">Tab Two</a>
</div>

<!-- Content of tab one (data-tab="first") -->
<div class="ui bottom attached tab segment active" data-tab="first" markdown="1">
  This is the content of Tab 1. Mardown is forced __on__.
</div>

<!-- Content of tab two (data-tab="second") -->
<div class="ui bottom attached tab segment" data-tab="second" markdown="1">
  This is the content of Tab2. I really should make this easier!
</div>
```
