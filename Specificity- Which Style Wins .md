#CSS The Missing Manual

## Specificity: Which Style Wins 

CSS Weight

tag selector ：1

class selector ：10

ID selector ：100

inline style ：1000

## Inherited Properties

Inherited Properties don't have any specifity， so even if a  
tag inherites properties from a style with a large specificity  like #banner those propertues will always be overdidden by a style that directly appplies to the tag.

## Tiebreaker
Last wins ！