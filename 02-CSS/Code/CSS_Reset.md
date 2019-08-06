# CSS_Reset

如果只是希望在各个浏览器的效果一致，请使用***normalize.css***。CSS Reset的作用是尽量的减少不同浏览器之间差异带来的兼容性问题。

```css
/* 清除内外边距 */
body, div, dl, dt, dd, ul, ol, li, h1, h2, h3, h4, h5, h6, pre, code, form, fieldset, legend, input, button, textarea, p, blockquote, th, td {
    margin: 0;
    padding: 0;
}
/* 默认字体和字号 */
body {
    font-size: 14px;
    font-family: "Helvetica Neue", Helvetica, Arial, "PingFang SC", "Hiragino Sans GB", "Heiti SC", "Microsoft YaHei", "WenQuanYi Micro Hei", sans-serif;
}
h1, h2, h3, h4, h5, h6 {
    font-weight: normal;
    font-size: 100%;
}
/* 内行元素重置 */
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
/* 列表重置 */
ol, ul, li {
    list-style: none;
}
/* 表单重置 */
input, textarea, select, button {
    font: 14px "Arial", "Helvetica Neue", Helvetica, Arial, "PingFang SC", "Hiragino Sans GB", "Heiti SC", "Microsoft YaHei", "WenQuanYi Micro Hei", sans-serif;
}
/* 表格重置 */
table {
    border-collapse: collapse;
}
html {
    overflow-y: scroll;
}
/* 清除浮动 */
.clear {
  overflow: auto;
}
```