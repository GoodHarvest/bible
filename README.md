# 圣经章节快速查找投影工具

## 目的
通过制作所述工具，学习网页制作的相关技术，如html, CSS, Javascript, jQuery等。
实现方式可能由非常多种，可以一一尝试。

## 设计要求
核心要求：可以通过简单的键盘命令，根据书名和章节，在数秒内找到并投影出某一经节和其前后文。以满足主日信息时快速投放出讲员所提到的经节
- 投影的实现，app分为两个窗口
    - 主窗口的功能有：
        - 查找章节
        - 选择检索方式：中，英，中英
        - 选择译本
        - 显示和恢复历史
        - 预览经文
    - 辅窗口的功能就是显示圣经
        - 显示选中的译本
        - 可以滚动
        - 分节高亮
- 查找经文
    - 界面：
        - 输入框：用于输入指令
        - 联想框：用于显示联想
        - 预览框：用于显示当前选中的章节
    - 简单的键盘命令：
        - 可以通过各种输入方式快速联想出所需要的书名（大小写一律不分）。可以通过复选框关闭英文检索或中文检索。
            - 英文书名，如 1Corinthians 
            - 英文简写，如 1co
            - 中文书名，如 哥林多前书
            - 中文简写，如 林前
            - 中文书名全拼，如 gelinduoqianshu
            - 中文简写全拼，如 linqian
            - 中文书名拼音首字母，gldqs
            - 中文简写拼音首字母，lq
            - 不完整中文拼音，如 gelinq 和 linq
            - *注：本project的动机就是因为中文区用户记忆英文书名和简写不容易，所以加如拼音的选项。且仍保留中文，以照顾使用模糊拼音和比划的用户*
        - 空格或任何标点都可以用来分隔，章节和书名的顺序不重要。如哥林多前书3章5节可以由以下输入找到：
            - 哥林多前书 3 5
            - 3 5 lq
            - 1co 3:5
            - linqian, 3,5
        - 可以通过键盘实现基本的控制指令
            - 有联想时数字键选择联想，无联想时数字键输入数字
            - 回车进行投影，并清空输入且光标放回原处
            - 预览框中信息不完整时，回车清空输入
- 辅助功能
    - 历史记录
        - 显示已经投影过的经文
        - 点击历史记录可以回放
    - 投影预览，用途暂时不明确
## 方案1
由于检索书名和投影显示是相对独立的，于是可以分开来尝试
- 投影显示
    - 开一个辐窗，然后把instantbible.org的内容投影过去
- 检索书名
    - 阶段一，用下拉表单先凑活一下
    - 阶段二，用horsey库实现联想的功能

## 实施

### 投影显示
- 打开一个新的窗口, t01t02, [link](https://www.w3schools.com/jsref/met_win_open.asp)

用instantbible.org显示经文
- 跳转到某网址, t02, [link](https://stackoverflow.com/a/506004)
- 延迟执行某项命令, t02, [link](https://www.w3schools.com/jsref/met_win_settimeout.asp)
- split a string by regrex, t02, [link](https://stackoverflow.com/a/10346754)

从数据库调圣经出来
- 在窗口中加入内容, t01, [link](https://www.w3schools.com/jsref/met_document_createelement.asp)
- 清理屏幕, t01, [link](https://stackoverflow.com/a/9967560)

### 检索书名
数据预备。
如果不把圣经数据放在app里面的话，数据就只有书名，没有必要还从后台调数据。
最简单的把数据放在前端的方式，就是在代码中直接加入[json](https://www.w3schools.com/js/js_json.asp)

将CSV转换为JSON，python code
- read csv as utf8 [link](https://stackoverflow.com/a/14786752)
- dump json as utf8 [link](https://stackoverflow.com/a/18337754)