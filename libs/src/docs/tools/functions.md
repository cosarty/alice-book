# 函数

## 隐藏字符串位数

默认全部隐藏

```ts
const obfuscateString = ({
  str,
  visibleStart = 0,
  visibleEnd = 0,
  mask = '*',
}: {
  str: string;
  visibleStart?: number;
  visibleEnd?: number;
  mask?: string;
}) =>
  str
    .trim()
    .replace(
      new RegExp(`^([\\s\\S]{${visibleStart}}).*([\\s\\S]{${visibleEnd}})$`),
      (match, start, end) =>
        `${start}${'*'.repeat(match.length - start.length - end.length)}${end}`
    );

// 例子
obfuscateString({ str: '47382788239473894', visibleStart: 2, visibleEnd: 2 });
//  输出 -> **3827882394738**
```
