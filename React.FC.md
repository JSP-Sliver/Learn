React.FC泛型

React.FC和React.ReactNode和JSX.Element和React.FC和React.ReactNode的区别与使用


详情参考：https://blog.csdn.net/sinat_36146776/article/details/105734353

一、React.FC

用React.FC可以在组件中改变state的值,详情可见React Hook

import React, { useState } from 'react';

export interface UserProps {
  updateModalVisible: boolean;
}

const User: React.FC<UserProps> = () => {
  let [count, setCount] = useState(4);

  const changeVal = () => {
    count++;
    setCount(count);
  };
  return <div style={{ padding: 20 }}>
    <h1>User页面</h1>
    <h2>{count}</h2>
    <button onClick={changeVal}>改变我的值</button>
  </div>;
};
export default User;

二、React.ReactElement

ReactElement is an object with a type and props.
ReactElement 是一个有type和props的对象.
被createElement函数调用，根据环境设置对应的属性

export interface AvatarListProps {
  Item?: React.ReactElement<AvatarItemProps>;
  size?: SizeType;
  maxLength?: number;
  excessItemsStyle?: React.CSSProperties;
  style?: React.CSSProperties;
  children: React.ReactElement<AvatarItemProps> | React.ReactElement<AvatarItemProps>[];
}

三、JSX.Element

JSX.Element = ReactElement
JSX.Element-> React.createElement的返回值

class Class implements  JSX.Element {
  // @ts-ignore
  key: React.Key | null | undefined;
  props: any;
  type: any;
}
1
2
3
4
5
6
四、React.ReactNode

ReactNode 可以是 ReactElement, ReactFragment, string ，a number 或者一个数组 ReactNodes, 或者null,或者 undefined, 或者 a boolean:
React.ReactNode->组件的返回值
render(): ReactNode;

参考链接：https://cloud.tencent.com/developer/article/1573512


————————————————
版权声明：本文为CSDN博主「吃瓜群众欢乐多」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/sinat_36146776/article/details/105734353