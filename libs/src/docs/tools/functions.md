# 函数

## 隐藏字符串位数

默认全部隐藏

```ts
const obfuscateString = ({
  str,
  visibleStart = 0,
  visibleEnd = 0,
  mask = "*",
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
        `${start}${"*".repeat(match.length - start.length - end.length)}${end}`
    );

// 例子
obfuscateString({ str: "47382788239473894", visibleStart: 2, visibleEnd: 2 });
//  输出 -> **3827882394738**
```

将列表嵌套对象组合按照某一个键值对排序

```ts
objArraySort(objArr, key) {
  let result = objArr.slice(0);
  return result.sort((a, b) =>  b[key]-a[key]);
},
```

## Echarts 图表相关

图例或文字显示不清晰问题解决方法:修改渲染方式

```ts
var myChart = echarts.init(document.getElementById("main"), null, {
  renderer: "svg",
});
```

柱状图设置相关:渐变色 设置背景色 设置柱子圆角

```ts
let itemStyle = {
  borderRadius: 8, //设置柱子圆角
  color: function (params) {
    var colorList = [
      ["#159AFF", "#0D5C99"],
      ["#4EE3E1", "#2B7D7C"],
      ["#7CA9FD", "#4A6597"],
      ["#FFC97A", "#997949"],
    ];
    var index = params.dataIndex;
    if (params.dataIndex >= colorList.length) {
      index = params.dataIndex - colorList.length;
    }
    return new echarts.graphic.LinearGradient(0, 0, 0, 1, [
      {
        offset: 0,
        color: colorList[index][0],
      },
      {
        offset: 1,
        color: colorList[index][1],
      },
    ]);
  },
  showBackground: true, //设置背景色
  backgroundStyle: {
    borderRadius: 8,
    color: "rgba(180, 180, 180, 0.2)",
  },
};
```

在柱状图最顶部显示数值:多加一条轴线,显示在最上方

```js
// 以横向柱状图为例,将yAxis设置成数组,添加以下代码:
{
  axisTick: "none",
  axisLine: "none",
  axisLabel: {
      textStyle: {
        color: "red",
        fontSize: "16",
      },
  },
  data: [ "7", "6", "5", "4", "3", "2", "1"],
},
```

设置文字和图例大小自适应(注意:参数值\*0.01)

```js
fontSize (res) {
  let clientWidth = window.innerWidth || document.documentElement.clientWidth || document.body.clientWidth;
  if (!clientWidth) return;
    let fontSize = 100 * (clientWidth / 1920);
  return res * fontSize;
},
// 用法
this.option.title[0].textStyle.fontSize = this.fontSize(0.24);
 window.addEventListener(
    "resize",
    () => {
      myChart1.resize();
      this.$set(option.legend.textStyle, "fontSize", this.fontSize(0.14));
      myChart1.setOption(option, true);
    },
  )
```

销毁实例

```js
echarts.init(lines.value).dispose();
echarts.dispose(lines.value);
if (myChart != null && myChart != "" && myChart != undefined) {
  myChart.dispose();
}
```


# h5 前端跨域配置

找到 manifest.json 文件，在"h5"里面添加以下代码：

```js
   "devServer" : {
            "disableHostCheck" : true,
            "port" : 9998,//端口号
            //转发代理
            "proxy" : {
                "/auth" : {//注意                         
                    "target" : "",//接口地址
                    "changeOrigin" : true, //是否跨域
                    "secure" : true,
                    "pathRewrite" : {
                        "^/auth" : "/auth"//注意
                    }
                },
            },
            "https" : false
        }
```

配置完后，测试环境的接口地址置空，即可。