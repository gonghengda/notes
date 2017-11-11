## React从后台拿到字符串类型的标签如何插到render中。。？
#### 方法一：
  `<div dangerouslySetInnerHTML={{__html: `text`}} />`
#### 方法二json，array类型：
`render(){
  return jsonList.map((json.html, index) => {
    return <div className="tag" key={index}>{json.html}</div>
  })
}`
