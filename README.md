# 修改引用 @Taro/taro

> 本库 fork 自 rxjs-hooks 具体使用细节，请翻看
[rxjs-hooks](https://www.npmjs.com/package/rxjs-hooks-taro)

## Installation

Using npm:

```
$ npm i --save rxjs-hooks-taro
```

Or yarn:

```
$ yarn add rxjs-hooks-taro
```

## Quick look

```tsx
import Taro, { useState } from '@tarojs/taro'
import { View, Text, Button } from '@tarojs/components'
import { useObservable } from 'rxjs-hooks-taro'
import './index.less'
import { Subject, interval } from 'rxjs';
import { tap, map, withLatestFrom } from 'rxjs/operators';

interface IProps {}

function Index (props: IProps) {
  const [count$] = useState(new Subject<number>());
  const count = useObservable(()  => {
    return count$.pipe(
      tap(count => console.log('count ==>', count)),
      withLatestFrom(interval(1000)),
      map(([count, timeCount]) => count + timeCount)
    )
  }
  , 0);
  return (
    <View className='index'>
      <Text>count: {count}</Text>
      <Button onClick={() =>  {
        count$.next(count + 1)
      }}> + 1</Button>
      <Button> - 1</Button>
    </View>
  )
}

export default Index;
```
