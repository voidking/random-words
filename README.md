# random-words

随机词 & 随机主题生成器，纯静态页面，支持 `file://` 直接打开。

## 项目结构

```
random-words/
├── css/
│   └── common.css                # 公共样式（变量、布局、按钮、卡片等）
├── js/
│   ├── words.js                  # 词库 JS 数组（WORDS）
│   └── themes.js                 # 主题库 JS 数组（THEMES）
├── data/
│   ├── words.txt                 # 词库文本（HTTP 服务 fetch 兜底）
│   ├── theme.txt                 # 主题库文本（HTTP 服务 fetch 兜底）
│   └── xiandaihaiyuchangyongcibiao.txt  # 原始词频表
├── index.html                    # 随机词生成器
├── theme.html                    # 随机主题生成器
└── README.md
```

## 页面

| 页面 | 说明 |
|------|------|
| [index.html](index.html) | 输入词数，从常用词库中随机选取词语 |
| [theme.html](theme.html) | 点击按钮，从备选主题库中随机选取一个写作主题 |

两个页面通过 header 导航栏互相链接。

## 技术说明

- 数据加载采用双轨策略：`<script>` 加载 JS 数组（兼容 `file://` 协议），`fetch()` 作为 HTTP 服务兜底
- 公共样式提取到 `css/common.css`，页面独有样式以内联 `<style>` 保留
- 纯静态实现，无需构建工具

## 我的词库

从原始词库中选择出最常用的 10000 个词。

```bash
sort -k3,3 -n data/xiandaihaiyuchangyongcibiao.txt | head -n 10000 > data/words.txt
```

## 原始词库

### 词库来源

https://github.com/liangqi/chinese-frequency-word-list

### 词库说明

Initial version is imported from
https://gist.github.com/indiejoseph/eae09c673460aa0b56db

Reference:
中国教育部：现代汉语常用词表（草案）
http://www.moe.gov.cn/jyb_sjzl/ziliao/A19/201001/t20100115_75693.html
http://www.moe.gov.cn/ewebeditor/uploadfile/2015/01/13/20150113085920115.pdf

4.《现代汉语常用词表（草案）》说明

4.1 本表研制过程中，收集词语同国家语委"现代汉语通用语料库"核心语料库、厦门大学的新词语语料库、《现代汉语规范词典》、《现代汉语词典》、《新华词典》等所收词语进行了比对，并查验了该词在人民网《人民日报》报系网页以及Google网简体中文网页、百度网等常用网页上的使用情况。
4.2 本表用来检测词频的语料库有：国家语委"现代汉语通用语料库"中经分词标注的4 500万字语料库、《人民日报》2001年～2005年约1.35亿字的分词标注语料和厦门大学的现当代文学作品语料库约7 000万字的语料。总共2.5亿字。
4.3 本表共收录常用词语56 008个，包括单音节词3 181个，双音节词语40 351个，三音节词语6 459个，四音节词语5 855个，五音节和五音节以上词语162个。表内条目按频级升序排列，频级相同的按汉语拼音音序排列。
4.4 本规范（草案）提供了《现代汉语常用词表》的音序索引，按汉语拼音音序排列，同音的条目按笔画数由少到多排列。其中，词语的读音只供检索使用，不代表词语的读音规范。