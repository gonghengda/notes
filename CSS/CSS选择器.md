## 基本选择器

|选择器	|例子|	功能描述
|-|-|-|
|.class	        | .intro	    | 选择 class="intro" 的所有元素。	|
|#id   	        | #firstname	| 选择 id="firstname" 的所有元素。|
|*	              | *	          | 选择所有元素。|
|element	        | p	          | 选择所有 `<p>` 元素。|
|element,element	| div,p	      | 选择所有 `<div>` 元素和所有 `<p>` 元素。|


## 层次选择器

选择器|	例子|	功能描述|
|-|-|-|
element element	  | div p	 | 选择 `<div>` 元素内部的所有 `<p>` 元素。	
element>element	  | div>p	 | 选择父元素为 `<div>` 元素的所有 `<p>` 元素。	
element+element	  | div+p	 | 选择紧接在 `<div>` 元素之后的所有 `<p>` 元素。	
element1~element2	| p~ul	 | 选择前面有 `<p>` 元素的每个 `<ul>` 元素。	

## 动态伪类选择器

选择器	|例子|	功能描述
|-|-|-|
:link	   | a:link	      | 选择所有未被访问的链接。
:visited | a:visited	  | 选择所有已被访问的链接。
:active	 | a:active	    | 选择活动链接。
:hover	 | a:hover	    | 选择鼠标指针位于其上的链接。
:focus	 | input:focus	| 选择获得焦点的 input 元素。
## 目标伪类选择器

选择器	|功能描述|
|-|-|
E:target|	选择匹配E的所有元素，且匹配元素被相关URL指向

## UI元素状态伪类选择器语法

选择器|	例子|	功能描述
|-|-|-|
:enabled	| input:enabled	  | 选择每个启用的 `<input>` 元素。
:disabled	| input:disabled	| 选择每个禁用的 `<input>` 元素
:checked	| input:checked	  | 选择每个被选中的 `<input>` 元素。

## 结构伪类选择器使用语法

选择器|	例子|	功能描述
|-|-|-|
:first-child	        | p:first-child	        | 选择属于父元素的第一个子元素的每个 `<p>` 元素。
:last-child	          | p:last-child	        | 选择属于其父元素最后一个子元素每个 `<p>` 元素
:first-of-type	      | p:first-of-type	      | 选择属于其父元素的首个 `<p>` 元素的每个 `<p>` 元素
:last-of-type	        | p:last-of-type	      | 选择属于其父元素的最后 `<p>` 元素的每个 `<p>` 元素
:only-of-type	        | p:only-of-type	      | 选择属于其父元素唯一的 `<p>` 元素的每个 `<p>` 元素
:only-child	          | p:only-child	        | 选择属于其父元素的唯一子元素的每个 `<p>` 元素
:nth-child(n) 	      | p:nth-child(2)	      | 选择属于其父元素的第二个子元素的每个 `<p>` 元素
:nth-last-child(n)	  | p:nth-last-child(2)	  | 同上，从最后一个子元素开始计数
:nth-of-type(n)	      | p:nth-of-type(2)	    | 选择属于其父元素第二个 `<p>` 元素的每个 `<p>` 元素
:nth-last-of-type(n)	| p:nth-last-of-type(2)	| 同上，但是从最后一个子元素开始计数
:root	                | :root	                | 选择文档的根元素。
:empty                | p:empty	              | 选择没有子元素的每个 `<p>` 元素（包括文本节点）

## 否定伪类选择器

选择器|	例子|	功能描述
|-|-|-|
:not(selector)|	:not(p)|	选择非 `<p>` 元素的每个元素。	

## 属性选择器语法

选择器|	例子|	功能描述
|-|-|-|
\[attribute=value]	  | \[target=_blank]	| 选择 target="_blank" 的所有元素。
\[attribute~=value]	  | \[title~=flower]	| 选择 title 属性包含单词 "flower" 的所有元素。
\[attribute\|=value]	| \[lang\|=en]	    | 选择 lang 属性值以 "en" 开头的所有元素。
\[attribute^=value]	  | a\[src^="https"]	| 选择其 src 属性值以 "https" 开头的每个 `<a>` 元素。
\[attribute$=value]	  | a\[src$=".pdf"]	| 选择其 src 属性以 ".pdf" 结尾的所有 `<a>` 元素。
\[attribute*=value]	  | a\[src*="abc"]	  | 选择其 src 属性中包含 "abc" 子串的每个 `<a>` 元素。

本文参考 [W3C标准](https://www.w3.org/TR/css3-selectors/#selectors)
