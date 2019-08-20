# CSS_Reset

CSS Reset的作用是尽量的减少不同浏览器之间差异带来的兼容性问题。使用时请自行压缩！

```css

body, div, dl, dt, dd, ul, ol, li, h1, h2, h3, h4, h5, h6, pre, code, form, fieldset, legend, input, button, textarea, p, blockquote, th, td {
    margin: 0;
    padding: 0;
}
body {
    font-size: 14px;
    font-family: "Helvetica Neue", Helvetica, Arial, "PingFang SC", "Hiragino Sans GB", "Heiti SC", "Microsoft YaHei", "WenQuanYi Micro Hei", sans-serif;
}
h1, h2, h3, h4, h5, h6 {
    font-weight: normal;
    font-size: 100%;
}
address, caption, cite, code, dfn, em, strong, th, var {
    font-style: normal;
    font-weight: normal;
}
a,a:hover {
    text-decoration: underline;
}
img {
    border: none;
    vertical-align: middle;
}
ol, ul, li {
    list-style: none;
}
input, textarea, select, button {
    font: 14px "Arial", "Helvetica Neue", Helvetica, Arial, "PingFang SC", "Hiragino Sans GB", "Heiti SC", "Microsoft YaHei", "WenQuanYi Micro Hei", sans-serif;
}
table {
    border-collapse: collapse;
}
html {
    overflow-y: scroll;
}
.clear {
  overflow: auto;
}

```

这样样式的重置仅仅是你希望可以更加强力的掌控整个页面样式和布局的时候使用。

如果只是希望在各个浏览器显示的效果一致，请使用[normalize.css](https://github.com/necolas/normalize.css)！