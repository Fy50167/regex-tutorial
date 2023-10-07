# Hex Value Regex Explanation

A brief gist explaining the various components that make up the Hex Code search regex.

## Summary

Hex Code search regex: 
```
/^#?([a-fA-F0-9]{6}|[a-fA-F0-9]{3})$/
```
The hex code search regex searches for any set of characters that follows a standard color hex code format: #XXXXXX. A hex code value always begins with a `#`, and the various characters that follow can be any alphabetic character (case insensitive) from a - f or any number with no restrictions. Note that while typical hex code structure has 6 characters following the `#`, if the 6 characters follow a format of three characters that are immediately repeated (ie. #ff00cc) then the hex code can instead be represented by three characters that don't repeat (ie. ##ff00cc becomes #f0c). This edge case is included within the hex code search regex. It should also be noted that while the `#` is generally included in any hex code to indicate what that it is actually a hex code, this regex will still recognize a string of characters without it (ie. in format XXXXXX).


## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes and Bracket Expressions](#character-classes-and-bracket-expressions)
- [Grouping and Capturing](#grouping-and-capturing)
- [Greedy and Lazy Match](#greedy-and-lazy-match)

## Regex Components

The hex code search regex looks as follows:
```
/^#?([a-fA-F0-9]{6}|[a-fA-F0-9]{3})$/
```
We can break this down into three main components: the anchor tags (the starting `/^` and ending `$/`), the character literals (`#?`), and the expressions (`([a-fA-F0-9]{6}|[a-fA-F0-9]{3})`). 

### Anchors

Any regex begins and ends with the `^` and `$` anchors. These anchors simply specify that the expressions that we are looking for begin and end with the characters specified enclosed within our anchors.

### Quantifiers

The quantifiers in this regex can be seen in the `?` as well as the numbers following the bracket expressions, `{6}` as well as `{3}`. The `?` immediately following the `#` indicates that the `#` can be found either 0 or 1 time, essentially that the string being searched for CAN but DOES NOT NEED TO include the `#`. The curly bracket quantifiers say that the expression that they are grouped with must have a length of either 6 or 3. This is not including the preceding `#`. It is also specific, meaning that the expression being searched for can NOT have a length of anything besides 6 or 3.

### OR Operator

This regex includes an OR operator seen in the `|` which is used to split the two meta characters searchers of `[a-fA-F0-9]{6}` and `[a-fA-F0-9]{3}`. The OR operator is included in this regex to account for the edge case mentioned in the summary in which a hex code follows a format of `#XXYYFF`, in which case it could then be shortened to `#XYF`.

### Character Classes and Bracket Expressions

The only character classes included in this regex are bracket expressions. The bracket expressions used in this regex are both identical, with the OR operator only being used to signify differences in quantifiers. This bracket expression, `[a-fA-F0-9]`, is fairly simple. The a-fA-F indicates that the character can be either a lowercase or uppercase letter between a and f inclusive while the 0-9 indicates that the character can also be any numeric digit.

### Grouping and Capturing

The grouping in this regex can be seen in the parentheses that are wrapped around the bracket expressions. In this case, the grouping is used to avoid including the preceding `#` in the curly bracket quantifiers. This is because the preceding `#` is followed by the `?`, which like mentioned earlier essentially makes it an optional inclusion. Not including the grouping using parentheses in this regex would include the preceding `#` in the specified 6 or 3 character length search, and while these could be increased by 1 each to 7 and 4 respectively to account for the inclusion, since the `#` is optional this would inevitably lead to some errors in searches. You could also technically include another OR operator to search for strings of lengths 6 or 3 OR lengths 7 and 4, but that would be a needlessly complex alternative and thus pointless to use over the current regex.

### Greedy and Lazy Match

All quantifiers used in this regex are greedy, meaning that it looks for as many different occurences of its specified expression as possible. The quantifiers are signified as being greedy since all quantifiers are inherently greedy, with a following `?` being necessary to enable lazy behavior.


## Author

This gist was written by Francis Yang. You can find my Github profile over here: 
