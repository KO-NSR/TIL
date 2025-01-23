# はじめに
親コンポーネントの```state```を更新して、それを使用している子コンポーネントも再レンダリングしたい<br>
そんな時は```key```属性を付与してあげよう！
> 参考サイト：https://zenn.dev/kotaesaki/articles/6249ea64f10574
<br>
<br>
# 使用例
下記の```page.js```（親コンポーネント）からその下の```user.js```（子コンポーネント）へ```props```でデータを渡している

```js
"use client"

import Link from "next/link";
import User from "../components/user";
import { useState } from "react";

const Home = () => {
    const [admin, setAdmin] = useState(true);

    const switchingUser = () => {
        setAdmin((user) => !user);
    }

    return (
        <div>
            {admin ? (<User name="管理者" key="admin" />) : (<User name="クライアント" key="client" />)}
            <button onClick={switchingUser}>切り替え</button>
            <div><Link href='/'>To HomePage.</Link></div>
        </div>
    )

}

export default Home;
```
```js
import Count from "./count";

const User = ({name}) => {
    return (
        <div>
            <h2>{name}</h2>
            <Count />
        </div>
    )
}

export default User;
```
  
```js
'use client'

import { useState } from "react";

const Count = () => {
    const [count, setCount] = useState(0);

    const increment = () => {
        setCount((num) => num+=1);
    }
    const decrement = () => {
        setCount((num) => num-=1);
    }

    return (
        <div>
            <div>{count}</div>
            <button onClick={increment}>+</button>
            <button onClick={decrement}>-</button>
        </div>
    )
}

export default Count;
```
<br>
<br>

# 結論
仮想DOMやレンダリングについて、まだまだ勉強が必要です。。。

