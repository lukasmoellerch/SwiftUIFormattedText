# SwiftUIFormattedText
A simple proof-of-concept SwiftUI library that renders a HTML-like language using SwiftUI Text elements.

## Description
Goal of this project is to test the described proof-of-concept. In the moment both the parser and the renderer are fairly
buggy. The language used is closely related to HTML and those comfortable with HTML should also be comfortable with this
language. The string is parsed into an abstract sytnax tree consisting of `Tag` structs. The tree is then rendered to
SwiftUI native `Text` views.

## Use Cases
- Formatted localized strings
- Loading text from a database
- Allowing the user to format text in a certain way

## Syntax
### Tags
The following tags are implemented:
- `largeTitle` / `h1`
- `title` / `h2`
- `headline` / `h3`
- `subheadline` / `h4`
- `body`
- `callout` / `h5`
- `caption` / `h6`
- `footnote`
- `b`
- `i`
- `u`
- `br`
- `font`
  - Attributes:
    - `family`
    - `size`
    - `color`
  - `family` and `size` attributes both have to be present for them to have any effect
  - `color` can only be given using hex values i.e. `#ff0000` and `#ff0000aa`

Block elements like h1/h2/h3/h4/h5 are not implemented in the moment. Newlines can only be added using `\n` and `<br/>`

The XML-like parser is very rudimentary and does not follow any specs. Unlike in HTML every tag that was opened has to be
closed - this includes `<br/>`.
### 👉 This is just a proof-of-concept that should not be used in any application
## Example
### Code
```
import SwiftUI
import SwiftUIFormattedText

struct ContentView : View {
    @State var string: String = "Type some text here..."
    var body: some View {
        VStack {
            TextField($string)
                .lineLimit(nil)
            
            FormattedText(formatted: string)
            .padding()
        }
        .frame(maxWidth: .infinity, maxHeight: .infinity)
    }
}
```
### Input
```
<h1>This is a h1</h1><br/>
<largeTitle>This is a largeTitle</largeTitle><br/>
<br/>
<h2>This is a h2</h2><br/>
<title>This is a title</title><br/>
<br/>
<h3>This is a h3</h3><br/>
<headline>This is a headline</headline><br/>
<br/>
<h4>This is a h4</h4><br/>
<subheadline>This is a subheadline</subheadline><br/>
<br/>
<h5>This is a h5</h5><br/>
<callout>This is a callout</callout><br/>
<br/>
<h6>This is a h6</h6><br/>
<caption>This is a caption</caption><br/>
<br/>
<body>The meaning of body is different compared to HTML</body><br/>
<footnote>This is a footnote</footnote><br/>
<i>This text is italic and this is <b>bold.</b></i><br/>
<u>This text should appear underlined.</u><br/>
<font color="#ff0000">This text should appear in red</font><br/>
Text can also wrap multiple lines:<br/>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
```
### Rendered Output
![alt text](https://raw.githubusercontent.com/LukasM01/SwiftUIFormattedText/master/Images/Example.png)
