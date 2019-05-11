# TEXT

## General

这是一个小小的文本编辑器。它长得有点像Terminal，黑乎乎的。

采用行缓冲。

支持左右方向键，Backspace和Delete键，以及回车，用于换行。

刚刚说过，采用行缓冲，所以，请在确认了该行的内容后再敲回车。

敲Esc可以把你刚才输入的东西在一个Terminal里显示出来。

用的库是Roberts的pc-borland: graphics库，库内容有过一些调整，基于windows，因此不必劳烦在linux等其它系统进行编译。

Roberts图形库的通病是，闪烁、画面刷新不到位。

逻辑上，这两个问题，解决了哪一个，另一个就会更严重。

作者对库的内容进行了调整，调整了其中调用的Windows GDI函数

最主要的函数有`Bitblt`，`InvalidateRect`

最终看起来效果还算可。



第一个版本采用的是拷贝屏幕的方式实现

1. 删除（包括用Backspace以及Delete实现的）
2. 添加字符后其他字符的左右移动

于是，在使用Serif字体时

1. 超过自身矩形范围的字母会被切割——例如Bell MT字体中的f字母
2. 光标的闪烁会导致字母的某一部分被切割——例如Bell MT字体中的f字母

最终，采用了每次进行字符输入以及删除操作时，对整个行缓冲区重新进行输出的方法。

Serif字体得到了更好的支持。



## Manual

下面请允许慵懒的我，直接粘贴第一个版本时就写好的manual：

README:

This program displays the text you input(imitating a terminal).
It uses line buffer like many terminals.
It interprets TAB as 4 spaces.
It supports ENTER key, interpreting it as line shifter.
LEFTARROW and RIGHTARROW can be used for moving the cursor.
BACKSPACE and DELETE are supported.
When you want to quit, hit the ESC key and your input will be displayed in a real terminal.
After that hit CTRL+C or ALT+F4 to close the program.

Modifications are supported.
- font
	- weight
	- size
- text
	- position
	- line spacing
- cursor
	- weight
	- length
- color
	- font color
	- background(black or white)