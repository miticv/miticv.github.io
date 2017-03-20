
# Why CSS is painfull

## Color Problem
cannot be variable - if changes need to find all instances to change
Same with fonts, sizes, colors etc.

## Duplication issues
No reusable sections in ss
Rounded corners repeats itelf:
```
border-radius: 5px;
-moz-border-radius: 5px;
-webkit-border-radius: 5px;
```

## Cascading Avalanches
Where cascaded rule is coming from
If change form id will need to change css also where it references it

## Lack of calculations
Cannot base value from any formula
Example: let font be  + 8px from other font...


## Problem with imports


