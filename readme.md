# Funky Features

- some things will return things like NaN, undefined, or null instead of causing an error that stops the code
- == and != will do a type conversion if you are comparing different types, which can cause unexpected problems with the above feature
- as the expression in a condition, the following values are false: **false**, **0**, **""** (empty string), **null**, **undefined**, **NaN** (not a number)
- === and !== to do proper comparisons to avoid this problem

