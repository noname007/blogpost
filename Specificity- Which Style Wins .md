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

## percent

To make matters more confusing，top and bottom percentage values are also calculated based on the width of the containing element ， not its height。 So a 20% top margin is 20 percent of the width of the styled tags container.

If the value used in a CSS property is 0, then you don’t need to add a unit of measurement. For example, just type margin: 0; instead of margin: 0px; .

margin and padding shorthand：The order in which you specify the four values is important,It must be top,right,bottom and left.


## display setting

two boxes: block and inline 
different from tag block tag and inline tag\


## dropshadow 
Drop shadows can force browsers to do a lot of re-rendering and redrawing,Use drop shadows carefully ,and make sure you test the performance of pages with drop shadows in mobile devices, which lack the powerful CPUs of a desktop or laptop computer.

## box-sizing 
box-sizing：

- content-box
- padding-box
- border-box

## overflow

- visible
- scroll
- auto
- hidden

## float
When you float block-level elements, you should also set the width property for that element (in fact, CSS rules require setting the width for floated elements for all tags except images).

float和position的差别在于一个是布局，一个是定位


## fixed and viewport
background-attachment

## Transforms
- vendor prefix

## Transition
- which properties to animate
- how long the animation takes
- the type of animation used
- an optional delay before the animation begins

## CSS Layout Strategies
- Start with your content
- Mobile-first
- padding marigin






