# react 实现.md文档渲染
### Question
- 给一个 `.md` 文档，将该文档内容渲染出来。

### Solution
#### 1、Use `raw-loader` to load `.md` file。
- 参见 [raw-loader](https://github.com/webpack-contrib/raw-loader) 。

- 如果是基于 `umi` 框架，没有 `webpack.config.js` 文件，则需要在 `config/config.js` 文件里添加如下内容：
    ```js
    ...

    urlLoaderExcludes: [/\.md$/],
    chainWebpack(config) {
        config.module
        .rule('md')
        .test(/\.md$/)
        .use('raw')
        .loader('raw-loader');
    },

    ...
    ```
    具体可参见：[umi 如何配置额外的 loader](https://github.com/umijs/umi/issues/1421#issuecomment-445132872).

#### 2、Use `react-markdown` to render Markdown as React components
- 参见[react-markdown](https://github.com/rexxars/react-markdown)

#### 3、Use `github-markdown-css`
- 参见 [github-markdown-css](https://github.com/sindresorhus/github-markdown-css)
- 新建 `markdown-github.less` ，内容：
 ```less
.markdown-body {
  box-sizing: border-box;
  min-width: 200px;
  max-width: 980px;
  margin: 0 auto;
  padding: 45px;
}

@media (max-width: 767px) {
  .markdown-body {
    padding: 15px;
  }
}
```

#### 4、Use `highlight.js` to hightlight code block
- 新建 `code-block.js`:
``` js
/* eslint-disable prefer-destructuring */
import hljs from 'highlight.js';

const React = require('react');
const PropTypes = require('prop-types');

class CodeBlock extends React.PureComponent {
  constructor(props) {
    super(props);
    this.setRef = this.setRef.bind(this);
  }

  componentDidMount() {
    this.highlightCode();
  }

  componentDidUpdate() {
    this.highlightCode();
  }

  setRef(el) {
    this.codeEl = el;
  }

  highlightCode() {
    hljs.highlightBlock(this.codeEl);
  }

  render() {
    return (
      <pre>
        <code ref={this.setRef} className={`language-${this.props.language}`}>
          {this.props.value}
        </code>
      </pre>
    );
  }
}

CodeBlock.defaultProps = {
  language: '',
};

CodeBlock.propTypes = {
  value: PropTypes.string.isRequired,
  language: PropTypes.string,
};

module.exports = CodeBlock;

```
- 新建 `code-block.less`:
```less
.hljs {
  display: block;
  overflow-x: auto;
  padding: 0.5em;
  color: #333;
  background: #f8f8f8;
}

.hljs-comment,
.hljs-quote {
  color: #998;
  font-style: italic;
}

.hljs-keyword,
.hljs-selector-tag,
.hljs-subst {
  color: #333;
  font-weight: bold;
}

.hljs-number,
.hljs-literal,
.hljs-variable,
.hljs-template-variable,
.hljs-tag .hljs-attr {
  color: #008080;
}

.hljs-string,
.hljs-doctag {
  color: #d14;
}

.hljs-title,
.hljs-section,
.hljs-selector-id {
  color: #900;
  font-weight: bold;
}

.hljs-subst {
  font-weight: normal;
}

.hljs-type,
.hljs-class .hljs-title {
  color: #458;
  font-weight: bold;
}

.hljs-tag,
.hljs-name,
.hljs-attribute {
  color: #000080;
  font-weight: normal;
}

.hljs-regexp,
.hljs-link {
  color: #009926;
}

.hljs-symbol,
.hljs-bullet {
  color: #990073;
}

.hljs-built_in,
.hljs-builtin-name {
  color: #0086b3;
}

.hljs-meta {
  color: #999;
  font-weight: bold;
}

.hljs-deletion {
  background: #fdd;
}

.hljs-addition {
  background: #dfd;
}

.hljs-emphasis {
  font-style: italic;
}

.hljs-strong {
  font-weight: bold;
}

```

综上，`react-markdown` 使用如下：
```js
      <div>
        <Markdown source={input} renderers={{ code: CodeBlock }} className="markdown-body" />
      </div>
```

### ref
- [react-markdown](https://github.com/rexxars/react-markdown)
- [raw-loader](https://github.com/webpack-contrib/raw-loader)
- [github-markdown-css](https://github.com/sindresorhus/github-markdown-css)
- [github-markdown-github](https://github.com/godaddy/react-markdown-github)



