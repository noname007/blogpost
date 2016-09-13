# Learn Css Layout

- display属性
	- block
  		- div
  		- p
  		- form
  	- inline
  		- span
	- none
 		- 与visibility存在区别
- border-sizing
	- border-box
	- content-box
- position
 - static
 - relative 
 - fixed
 - absolute
 	- a "positioned" element is one whose position is anything except static.

- float Float is intended for wrapping text around images 
- clear for the property ‘float’
- inline-block don't need clear 
- float need clear
- display:inline-block 
- diplay;flexbox

- flex (display:flex ）
 - flex-container
  	 - flex-direction
  		 - row
  		 - row-reverse
  		 - column
  		 - column-reverse
    - justify-content  for main axis
    	- flex-start (default)
		- flex-end
		- center
		- space-between
		- space-around

	![https://static.bocoup.com/blog/flex-pack.svg](https://static.bocoup.com/blog/flex-pack.svg)
	
	- align-items cross axis
		- flex-start (default)
		- flex-end
		- center
		- baseline
		- stretch 

	![](https://static.bocoup.com/blog/flex-align.svg)
	- flex-wrap for more flex lines
	- align-content aligning flex lines 

	- flex-flow : = flex-direction + flex -wrap eg：column nowrap
 - flex-items 
 	- flex 权重
 	