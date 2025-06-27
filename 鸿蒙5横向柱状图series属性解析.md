大家好，欢迎回来鸿蒙5莓创图表组件的专场，我们这一期来讲解McHorBarChart（横向柱状图）组件中series属性的详细用法。series属性是控制柱状图数据系列的核心配置项，掌握好这些属性可以让你轻松创建各种样式的柱状图效果。

## 1. name属性

作用：定义数据系列的名称，这个名称会显示在图例(legend)中，也会在tooltip提示框中显示。

类型：String

默认值：空字符串

必填：是

场景：当需要显示多个数据系列时，必须为每个系列设置不同的名称以便区分；在需要图例交互或tooltip提示时也需要设置。

代码示例：

```
series: [
  {
    name: '最高气温',
    data: [11, 11, 15, 13, 12, 130, 10]
  },
  {
    name: '最低气温',
    data: [1, 2, 5, 3, 2, 30, 0]
  }
]
```

## 2. color属性

作用：设置柱状图的颜色，可以是单一颜色或渐变色。

类型：String | Array<String>

默认值：使用全局调色盘颜色

可选值：

-   十六进制颜色值，如'#296DFF'
-   RGB颜色值，如'rgb(41, 109, 255)'
-   渐变色数组，如['#53e075', '#7953e075']

场景：需要自定义柱状图颜色时使用；当需要突出显示某个系列时；实现渐变效果时。

代码示例：

```
// 单一颜色
series: [
  {
    name: '最高气温',
    color: '#ff2659f5',
    data: [11, 11, 15, 13, 12, 130, 10]
  }
]

// 渐变色
series: [
  {
    name: '最高气温',
    gradient: {
      color: ['#53e075', '#7953e075']
    },
    data: [30, 31, 35, 31, 28, 31, 31]
  }
]
```

## 3. shapeType属性

作用：控制柱状图的形状类型，可以创建普通柱状图或阶梯状柱状图。

类型：String

默认值：'normal'

可选值：

-   'normal'：普通柱状图
-   'leftEchelon'：左阶梯状柱状图
-   'rightEchelon'：右阶梯状柱状图

场景：需要创建特殊形状的柱状图时；在数据可视化中强调变化趋势时。

代码示例：

```
series: [
  {
    name: '阶梯状柱状图',
    shapeType: 'leftEchelon',
    data: [11, 11, 15, 13, 12, 130, 10]
  }
]
```

## 4. echelonOffset属性

作用：当shapeType设置为阶梯状时，控制阶梯的锐度偏移量。

类型：Number

默认值：10

场景：调整阶梯状柱状图的视觉效果；需要更平缓或更尖锐的阶梯效果时。

代码示例：

```
series: [
  {
    name: '阶梯状柱状图',
    shapeType: 'leftEchelon',
    echelonOffset: 15, // 更大的值会使阶梯更明显
    data: [11, 11, 15, 13, 12, 130, 10]
  }
]
```

## 5. yAxisIndex属性

作用：指定该数据系列关联的Y轴索引，用于多Y轴场景。

类型：Number

默认值：0

可选值：0或1（对应配置的yAxis数组中的索引）

场景：当图表需要显示多个Y轴时；不同数据系列的单位或量纲不同时。

代码示例：

```
yAxis: [
  {name: '温度(℃)'},
  {name: '湿度(%)'}
],
series: [
  {
    name: '温度',
    yAxisIndex: 0,
    data: [11, 11, 15, 13, 12, 130, 10]
  },
  {
    name: '湿度',
    yAxisIndex: 1,
    data: [30, 35, 40, 45, 50, 55, 60]
  }
]
```

## 6. barStyle属性

作用：配置柱状图的样式，包括宽度、圆角、颜色等。

类型：Object

默认值：{}

子属性详解：

### 6.1 width

作用：设置柱子的宽度。

类型：Number

默认值：自动计算

场景：需要固定柱子宽度时；图表数据点较多需要缩小柱子时。

### 6.2 borderRadius

作用：设置柱子的圆角半径。

类型：Array<Number> | Number

默认值：0

可选值：

-   单一数值：四个角使用相同圆角
-   数组：[左上, 右上, 右下, 左下]
-   简写数组：[左上和右下, 右上和左下]

场景：创建圆角柱状图时；需要美化柱子外观时。

### 6.3 color

作用：覆盖系列级别的颜色设置，单独设置柱子的颜色。

类型：String

默认值：继承series.color

场景：需要单独设置柱子颜色时。

完整代码示例：

```
series: [
  {
    name: '圆角柱状图',
    barStyle: {
      width: 10,
      borderRadius: [0, 4, 4, 0], // 左上和右下无圆角，右上和左下4px圆角
      color: '#fa6262'
    },
    data: [11, 11, 15, 13, 12, 130, 10]
  }
]
```

## 7. backgroundStyle属性

作用：配置背景柱状图的显示和样式。

类型：Object

默认值：{show: false}

子属性详解：

### 7.1 show

作用：是否显示背景柱状图。

类型：Boolean

默认值：false

场景：需要显示背景参考线时；强调数据与目标的对比时。

### 7.2 width

作用：背景柱子的宽度。

类型：Number

默认值：与主柱子相同

### 7.3 color

作用：背景柱子的颜色。

类型：String

默认值：'rgba(180, 180, 180, 0.2)'

完整代码示例：

```
series: [
  {
    name: '销售完成率',
    backgroundStyle: {
      show: true,
      width: 15,
      color: 'rgba(200, 200, 200, 0.3)'
    },
    data: [80, 92, 75, 88, 90, 83, 78]
  }
]
```

## 8. label属性

作用：配置柱状图上显示的文本标签。

类型：Object

默认值：{show: false}

子属性详解：

### 8.1 show

作用：是否显示文本标签。

类型：Boolean

默认值：false

### 8.2 color

作用：文本标签的颜色。

类型：String

默认值：'#000'

### 8.3 fontSize

作用：文本标签的字体大小。

类型：Number

默认值：12

### 8.4 fontWeight

作用：文本标签的字体粗细。

类型：String

默认值：'normal'

可选值：'normal' | 'bold' | 'lighter' | 'bolder' | 100-900

### 8.5 fontFamily

作用：文本标签的字体家族。

类型：String

默认值：'sans-serif'

### 8.6 position

作用：文本标签的位置。

类型：String

默认值：'top'（横向柱状图为'right'）

可选值：'top' | 'bottom' | 'left' | 'right' | 'inside' | 'center'

### 8.7 offset

作用：文本标签的偏移量。

类型：Array<Number>

默认值：[0, 0]

### 8.8 formatter

作用：自定义文本标签内容。

类型：String | Function

默认值：显示数据值

可选值：

-   'seriesLabel'：显示系列名称和数据值
-   函数：自定义格式函数

完整代码示例：

```
series: [
  {
    name: '销售额',
    label: {
      show: true,
      color: '#fff',
      fontSize: 14,
      fontWeight: 'bold',
      position: 'center',
      offset: [0, 0],
      formatter: (params) => {
        return `¥${params.value}万`
      }
    },
    data: [120, 200, 150, 80, 70, 110, 130]
  }
]
```

## 9. stack属性

作用：设置堆叠柱状图，相同stack值的系列会堆叠在一起。

类型：String

默认值：空（不堆叠）

场景：需要显示堆叠柱状图时；展示部分与整体的关系时。

代码示例：

```
series: [
  {
    name: '产品A',
    stack: 'total',
    data: [120, 132, 101, 134, 90, 230, 210]
  },
  {
    name: '产品B',
    stack: 'total',
    data: [220, 182, 191, 234, 290, 330, 310]
  }
]
```

## 10. data属性

作用：设置柱状图的数据。

类型：Array<String | Number | Object>

默认值：[]

必填：是

数据格式说明：

-   简单数组：[11, 11, 15, 13, 12, 130, 10]
-   对象数组：[{value: 11, color: '#ff0000'}, {value: 15, itemStyle: {...}}]

场景：任何柱状图都必须设置的数据；需要单独设置某个柱子的样式时。

代码示例：

```
// 简单数据
series: [
  {
    name: '简单数据',
    data: [11, 11, 15, 13, 12, 130, 10]
  }
]

// 复杂数据
series: [
  {
    name: '复杂数据',
    data: [
      11, 
      {value: 15, color: '#ff0000'},
      {value: 13, itemStyle: {borderColor: '#000', borderWidth: 2}},
      12, 
      130, 
      10
    ]
  }
]
```

## 实际应用案例

下面我们通过一个完整的实际案例来展示如何综合运用这些属性：

```
@Entry
@Component
struct SalesChart {
  @State options: Options = new Options({
    title: {
      show: true,
      text: '2023年季度销售报告',
      left: 'center',
      top: 10
    },
    legend: {
      show: true,
      top: 40
    },
    xAxis: {
      data: ['Q1', 'Q2', 'Q3', 'Q4']
    },
    yAxis: {
      name: '销售额 (万元)'
    },
    series: [
      {
        name: '线上销售',
        stack: 'total',
        barStyle: {
          borderRadius: [4, 4, 0, 0]
        },
        label: {
          show: true,
          position: 'inside',
          color: '#fff',
          formatter: 'seriesLabel'
        },
        gradient: {
          color: ['#4facfe', '#00f2fe']
        },
        data: [320, 332, 301, 334]
      },
      {
        name: '线下销售',
        stack: 'total',
        barStyle: {
          borderRadius: [0, 0, 4, 4]
        },
        label: {
          show: true,
          position: 'inside',
          color: '#fff',
          formatter: 'seriesLabel'
        },
        gradient: {
          color: ['#b8cbb8', '#b8cbb8', '#b465da']
        },
        data: [120, 132, 101, 134]
      },
      {
        name: '目标',
        type: 'line',
        symbol: 'diamond',
        symbolSize: 12,
        lineStyle: {
          width: 3,
          color: '#ff9800'
        },
        itemStyle: {
          color: '#ff9800'
        },
        data: [450, 464, 402, 468]
      }
    ]
  })

  build() {
    Row() {
      McHorBarChart({options: this.options})
    }
    .height('50%')
    .width('100%')
  }
}
```

这个案例展示了：

1.  堆叠柱状图的使用
1.  渐变色的应用
1.  圆角柱子的设置
1.  标签的灵活配置
1.  混合图表（柱状图+折线图）的实现

好，这期讲到这里就结束了，希望大家通过这篇文章能够全面掌握McHorBarChart组件的series属性配置，在实际开发中灵活运用这些属性创建出各种精美的柱状图效果。如果有任何问题，欢迎在评论区留言讨论，我们下期再见！