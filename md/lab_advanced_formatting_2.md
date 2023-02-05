
Creating and highlighting code blocks
=====================================


Share samples of code with fenced code blocks and enabling syntax
highlighting.


Fenced code blocks
----------------------------------------------------

You can create fenced code blocks by placing triple backticks
```` ``` ```` before and after the code block. We recommend placing a
blank line before and after code blocks to make the raw formatting
easier to read.

    ```
    function test() {
      console.log("notice the blank line before this function?");
    }
    ```

![Rendered fenced code
block](./images/fenced-code-block-rendered.png)


**Tip:** To preserve your formatting within a list, make sure to indent
non-fenced code blocks by eight spaces.


To display triple backticks in a fenced code block, wrap them inside
quadruple backticks.

    ````
    ```
    Look! You can see my backticks.
    ```
    ````

![Rendered fenced code with backticks
block](./images/fenced-code-show-backticks-rendered.png)

If you are frequently editing code snippets and tables, you may benefit
from enabling a fixed-width font in all comment fields on GitHub. For
more information, see \"[Enabling fixed-width fonts in the
editor].\"

Syntax highlighting
------------------------------------------------------

You can add an optional language identifier to enable syntax
highlighting in your fenced code block.

For example, to syntax highlight Ruby code:

    ```ruby
    require 'redcarpet'
    markdown = Redcarpet.new("Hello World!")
    puts markdown.to_html
    ```

![Rendered code block with Ruby syntax
highlighting](./images/code-block-syntax-highlighting-rendered.png)



#### Writing mathematical expressions

Use Markdown to display mathematical expressions on GitHub.




About writing mathematical expressions
------------------------------------------------------------

To enable clear communication of mathematical expressions, GitHub
supports LaTeX formatted math within Markdown.

GitHub\'s math rendering capability uses MathJax; an open source,
JavaScript-based display engine. MathJax supports a wide range of LaTeX
macros, and several useful accessibility extensions.


Writing inline expressions
---------------------------------------------------------------

To include a math expression inline with your text, delimit the
expression with a dollar symbol `$`.

    This sentence uses `$` delimiters to show math inline:  $\sqrt{3x-1}+(1+x)^2$

![Inline math markdown
rendering](./images/inline-math-markdown-rendering.png)

Writing expressions as blocks
------------------------------------------

To add a math expression as a block, start a new line and delimit the
expression with two dollar symbols `$$`.

    **The Cauchy-Schwarz Inequality**

    $$\left( \sum_{k=1}^n a_k b_k \right)^2 \leq \left( \sum_{k=1}^n a_k^2 \right) \left( \sum_{k=1}^n b_k^2 \right)$$

![Math expression as a block
rendering](./images/math-expression-as-a-block-rendering.png)

Alternatively, you can use the ```` ```math ```` code block syntax to
display a math expression as a block. With this syntax, you don\'t need
to use `$$` delimiters.

    **Here is some math!**

    ```math
    \sqrt{3}
    ```

![Math expression in a fenced code
block](./images/math-expression-as-a-fenced-code-block.png)

Writing dollar signs in line with and within mathematical expressions
-----------------------------------------------------------------------

To display a dollar sign as a character in the same line as a
mathematical expression, you need to escape the non-delimiter `$` to
ensure the line renders correctly.

-   Within a math expression, add a `\` symbol before the explicit `$`.

        This expression uses `\$` to display a dollar sign: $\sqrt{\$4}$

    ![Dollar sign within math
    expression](./images/dollar-sign-within-math-expression.png)

-   Outside a math expression, but on the same line, use span tags
    around the explicit `$`.

        To split <span>$</span>100 in half, we calculate $100/2$

    ![Dollar sign inline math
    expression](./images/dollar-sign-inline-math-expression.png)
