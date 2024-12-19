### Line-Wrapping

> Terminology note: **Line-wrapping** is the activity of dividing code into multiple lines that might otherwise legally occupy a single line.

For the purposes of Google Swift style, many declarations (such as type declarations and function declarations) and other expressions (like function calls) can be partitioned into **breakable** units that are separated by **unbreakable** delimiting token sequences.

As an example, consider the following complex function declaration, which needs to be line-wrapped:

```
public func index<Elements: Collection, Element>(of element: Element, in collection: Elements) -> Elements.Index? where Elements.Element == Element, Element: Equatable {
  // ...
}

```

This declaration is split as follows (scroll horizontally if necessary to see the full example). Unbreakable token sequences are indicated in orange; breakable sequences are indicated in blue.

public func index<Elements: Collection, Element>(of element: Element, in collection: Elements) ->Elements.Index?whereElements.Element == Element, Element: Equatable{
  // ...
}

1.  The **unbreakable** token sequence up through the open angle bracket (`<`) that begins the generic argument list.
2.  The **breakable** list of generic arguments.
3.  The **unbreakable** token sequence (`>(`) that separates the generic arguments from the formal arguments.
4.  The **breakable** comma-delimited list of formal arguments.
5.  The **unbreakable** token-sequence from the closing parenthesis (`)`) up through the arrow (`->`) that precedes the return type.
6.  The **breakable** return type.
7.  The **unbreakable** `where` keyword that begins the generic constraints list.
8.  The **breakable** comma-delimited list of generic constraints.

Using these concepts, the cardinal rules of Google Swift style for line-wrapping are:

1.  If the entire declaration, statement, or expression fits on one line, then do that.
2.  Comma-delimited lists are only laid out in one direction: horizontally or vertically. In other words, all elements must fit on the same line, or each element must be on its own line. A horizontally-oriented list does not contain any line breaks, even before the first element or after the last element. Except in control flow statements, a vertically-oriented list contains a line break before the first element and after each element.
3.  A continuation line starting with an unbreakable token sequence is indented at the same level as the original line.
4.  A continuation line that is part of a vertically-oriented comma-delimited list is indented exactly +2 from the original line.
5.  When an open curly brace (`{`) follows a line-wrapped declaration or expression, it is on the same line as the final continuation line unless that line is indented at +2 from the original line. In that case, the brace is placed on its own line, to avoid the continuation lines from blending visually with the body of the subsequent block.

    ```
    public func index<Elements: Collection, Element>(
      of element: Element,
      in collection: Elements
    ) -> Elements.Index?
    where
      Elements.Element == Element,
      Element: Equatable
    {  // GOOD.
      for current in elements {
        // ...
      }
    }

    ```

    ```
    public func index<Elements: Collection, Element>(
      of element: Element,
      in collection: Elements
    ) -> Elements.Index?
    where
      Elements.Element == Element,
      Element: Equatable {  // AVOID.
      for current in elements {
        // ...
      }
    }

    ```

For declarations that contain a `where` clause followed by generic constraints, additional rules apply:

1.  If the generic constraint list exceeds the column limit when placed on the same line as the return type, then a line break is first inserted **before** the `where` keyword and the `where` keyword is indented at the same level as the original line.
2.  If the generic constraint list still exceeds the column limit after inserting the line break above, then the constraint list is oriented vertically with a line break after the `where` keyword and a line break after the final constraint.

Concrete examples of this are shown in the relevant subsections below.

This line-wrapping style ensures that the different parts of a declaration are *quickly and easily identifiable to the reader* by using indentation and line breaks, while also preserving the same indentation level for those parts throughout the file. Specifically, it prevents the zig-zag effect that would be present if the arguments are indented based on opening parentheses, as is common in other languages:

```
public func index<Elements: Collection, Element>(of element: Element,  // AVOID.
                                                 in collection: Elements) -> Elements.Index?
    where Elements.Element == Element, Element: Equatable {
  doSomething()
}

```
