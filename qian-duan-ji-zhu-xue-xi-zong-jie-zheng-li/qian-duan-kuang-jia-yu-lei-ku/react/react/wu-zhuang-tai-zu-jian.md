# 无状态组件
没有state的组件建议都写成无状态组件，**对性能有较大的提升**。



```
import React from 'react';

let A = (props) => {
  return (
    <div>{props.title}</div>
  );
}

export default BorderLine;
```

