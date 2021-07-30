# ffmpeg-notes
## 主要选项
* `-i`：  
输入文件的url  
* `-ss`：  
在`-i`之前，定位到输入位置。必须是一个时间，如需定位在具体帧处，例：如果输入视频为25fps，要从133帧处开始，首先计算时间戳：133 / 25 = 5.32  
如果需要编码指定数量的帧，再加上`-frames:v`选项  
````
ffmpeg -ss 5.32 -i input.mp4 -c:v libx264 -c:a copy -frames:v 40 output.mp4
````  
注意输出视频需要重新编码，不能用copy  
* `-map_metadata`：  
设为 -1 可删除所有元数据  
* `-map_chapter`:  
设为 -1 可删除所有章节
## 流选择
* `-vn / -an / -sn / -dn`：  
分别为忽略视频流、音频流、字幕和数据  
* `-map`：  
使用此选项时，只有选定的流会包含在输出文件中  
    + `-map 0:1`：选择输入的第0个文件的第1条流
    + `-map 0:v`：选择输入的第0个文件的所有视频流
    + `-map 0:a`：选择输入的第0个文件的所有音频流  
## 视频选项
* `-s`：  
设置帧大小  
* `-pix_fmt`：  
设置像素格式，使用`-pix_fmts`列出所有支持的格式。例：将10bit转为8bit使用yuv420p
## 编码器选项
* `-c / -codec`：  
选择编码器，使用copy避免重新编码
* `-c:v / -codec:v`：  
选择视频编码器：  
    + libx264 : AVC编码器
    + libx265 : HEVC编码器
* `-c:a / -codec:a`：  
选择音频编码器  
* `-profile`:  
常见的有main和high
* `-preset`:  
编码速度的快慢，越慢画质越好，反之越快画质损失越严重，可用的参数有  
    + ultrafast
    + superfast
    + veryfast
    + faster
    + fast
    + medium (default)
    + slow
    + slower
    + veryslow
    + placebo
* `-crf`:  
此数值越大编码体积越小，画质损失越严重，0为编码毫无损失，但可能产生体积庞大的输出文件，推荐18-23  
* `-tune`：  
animation：优化动画的编码质量  
