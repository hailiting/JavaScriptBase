~~~
<h2>
  hello imooc i love React& Rdux
</h2>
=>
"use strict"
React.createElement(
  'h2',
  null,
  'hello imooc i love React& Rdux'
)
// 
<h2 data-id='imooc' style='color: red'>
  <p>hello imooc i love React& Rdux</p>
</h2>
=>
'use strict'
React.createElement(
  'h2',
  {'data-id':'imooc',style: 'color: red'}
  React.createElement(
    'p',
    {'data-name':'react rocks!'},
    'hello imooc i love React& Rdux'
  )
)
~~~
