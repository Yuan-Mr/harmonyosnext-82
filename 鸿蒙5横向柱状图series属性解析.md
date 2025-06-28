### Hello and welcome back to our special session on HarmonyOS 5 Berry Creative chart components. In this episode, we'll explore the detailed usage of the `series` property in the **McHorBarChart (Horizontal Bar Chart)** component. The `series` property is the core configuration for controlling data series in bar charts. Mastering these properties will empower you to create various bar chart styles effortlessly.  


### 1. `name` Property  
**Function**: Defines the name of the data series, which appears in the legend and tooltip.  
**Type**: String  
**Default**: Empty string  
**Required**: Yes  

**Scenarios**:  
- Distinguish multiple data series with unique names.  
- Enable legend interactions or tooltip displays.  

**Code Example**:  
```json
series: [
  {
    name: 'Highest Temperature',
    data: [11, 11, 15, 13, 12, 130, 10]
  },
  {
    name: 'Lowest Temperature',
    data: [1, 2, 5, 3, 2, 30, 0]
  }
]
```  


### 2. `color` Property  
**Function**: Sets the color of bars, supporting single colors or gradients.  
**Type**: String | Array<String>  
**Default**: Uses the global color palette.  

**Options**:  
- Hex color (e.g., `'#296DFF'`)  
- RGB color (e.g., `'rgb(41, 109, 255)'`)  
- Gradient array (e.g., `['#53e075', '#7953e075']`)  

**Scenarios**:  
- Customize bar colors.  
- Highlight specific series.  
- Implement gradient effects.  

**Code Examples**:  
```json
// Single color  
series: [
  {
    name: 'Highest Temperature',
    color: '#ff2659f5',
    data: [11, 11, 15, 13, 12, 130, 10]
  }
]

// Gradient  
series: [
  {
    name: 'Highest Temperature',
    gradient: {
      color: ['#53e075', '#7953e075']
    },
    data: [30, 31, 35, 31, 28, 31, 31]
  }
]
```  


### 3. `shapeType` Property  
**Function**: Controls bar shapes (normal or stepped).  
**Type**: String  
**Default**: `'normal'`  

**Options**:  
- `'normal'`: Standard bars  
- `'leftEchelon'`: Left-stepped bars  
- `'rightEchelon'`: Right-stepped bars  

**Scenarios**:  
- Create special-shaped bars.  
- Emphasize trends in data visualization.  

**Code Example**:  
```json
series: [
  {
    name: 'Stepped Bar Chart',
    shapeType: 'leftEchelon',
    data: [11, 11, 15, 13, 12, 130, 10]
  }
]
```  


### 4. `echelonOffset` Property  
**Function**: Adjusts the sharpness of stepped bars when `shapeType` is set to stepped.  
**Type**: Number  
**Default**: 10  

**Scenarios**:  
- Fine-tune the visual effect of stepped bars.  
- Create smoother or sharper steps.  

**Code Example**:  
```json
series: [
  {
    name: 'Stepped Bar Chart',
    shapeType: 'leftEchelon',
    echelonOffset: 15, // Larger value = more pronounced steps
    data: [11, 11, 15, 13, 12, 130, 10]
  }
]
```  


### 5. `yAxisIndex` Property  
**Function**: Associates the series with a specific Y-axis (for multi-axis charts).  
**Type**: Number  
**Default**: 0  
**Options**: 0 or 1 (index of the `yAxis` array)  

**Scenarios**:  
- Display multiple Y-axes with different units.  
- Plot series with different scales.  

**Code Example**:  
```json
yAxis: [
  { name: 'Temperature (°C)' },
  { name: 'Humidity (%)' }
],
series: [
  {
    name: 'Temperature',
    yAxisIndex: 0,
    data: [11, 11, 15, 13, 12, 130, 10]
  },
  {
    name: 'Humidity',
    yAxisIndex: 1,
    data: [30, 35, 40, 45, 50, 55, 60]
  }
]
```  


### 6. `barStyle` Property  
**Function**: Configures bar appearance (width, radius, color, etc.).  
**Type**: Object  
**Default**: `{}`  

#### 6.1 `width`  
**Function**: Sets bar width.  
**Type**: Number  
**Default**: Auto-calculated  

**Scenarios**:  
- Fix bar width.  
- Reduce bar width for dense data.  

#### 6.2 `borderRadius`  
**Function**: Sets bar corner radius.  
**Type**: Array<Number> | Number  
**Default**: 0  

**Options**:  
- Single value: All corners use the same radius.  
- Array: `[top-left, top-right, bottom-right, bottom-left]`  
- Shorthand: `[top-left & bottom-right, top-right & bottom-left]`  

**Scenarios**:  
- Create rounded bars.  
- Enhance visual aesthetics.  

#### 6.3 `color`  
**Function**: Overrides the series color for individual bars.  
**Type**: String  
**Default**: Inherits from `series.color`  

**Scenario**: Customize bar colors individually.  

**Complete Example**:  
```json
series: [
  {
    name: 'Rounded Bars',
    barStyle: {
      width: 10,
      borderRadius: [0, 4, 4, 0], // No rounding on top-left/bottom-right
      color: '#fa6262'
    },
    data: [11, 11, 15, 13, 12, 130, 10]
  }
]
```  


### 7. `backgroundStyle` Property  
**Function**: Configures background bars for reference.  
**Type**: Object  
**Default**: `{ show: false }`  

#### 7.1 `show`  
**Function**: Toggles background bars.  
**Type**: Boolean  
**Default**: `false`  

**Scenarios**:  
- Display reference baselines.  
- Highlight data vs. targets.  

#### 7.2 `width`  
**Function**: Sets background bar width.  
**Type**: Number  
**Default**: Same as main bars  

#### 7.3 `color`  
**Function**: Sets background bar color.  
**Type**: String  
**Default**: `'rgba(180, 180, 180, 0.2)'`  

**Complete Example**:  
```json
series: [
  {
    name: 'Sales Completion Rate',
    backgroundStyle: {
      show: true,
      width: 15,
      color: 'rgba(200, 200, 200, 0.3)'
    },
    data: [80, 92, 75, 88, 90, 83, 78]
  }
]
```  


### 8. `label` Property  
**Function**: Configures data labels on bars.  
**Type**: Object  
**Default**: `{ show: false }`  

#### 8.1 `show`  
**Function**: Toggles labels.  
**Type**: Boolean  
**Default**: `false`  

#### 8.2 `color`  
**Function**: Sets label text color.  
**Type**: String  
**Default**: `'#000'`  

#### 8.3 `fontSize`  
**Function**: Sets label font size.  
**Type**: Number  
**Default**: 12  

#### 8.4 `fontWeight`  
**Function**: Sets label font weight.  
**Type**: String  
**Default**: `'normal'`  

**Options**: `'normal' | 'bold' | 'lighter' | 'bolder' | 100-900`  

#### 8.5 `fontFamily`  
**Function**: Sets label font family.  
**Type**: String  
**Default**: `'sans-serif'`  

#### 8.6 `position`  
**Function**: Sets label position.  
**Type**: String  
**Default**: `'right'` (for horizontal bars)  

**Options**: `'top' | 'bottom' | 'left' | 'right' | 'inside' | 'center'`  

#### 8.7 `offset`  
**Function**: Adjusts label position offset.  
**Type**: Array<Number>  
**Default**: `[0, 0]`  

#### 8.8 `formatter`  
**Function**: Customizes label content.  
**Type**: String | Function  
**Default**: Displays raw data  

**Options**:  
- `'seriesLabel'`: Shows series name and value  
- Function: Custom formatting logic  

**Complete Example**:  
```json
series: [
  {
    name: 'Sales Revenue',
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


### 9. `stack` Property  
**Function**: Enables stacked bars for series with the same `stack` value.  
**Type**: String  
**Default**: Empty (no stacking)  

**Scenarios**:  
- Create stacked bar charts.  
- Show part-to-whole relationships.  

**Code Example**:  
```json
series: [
  {
    name: 'Product A',
    stack: 'total',
    data: [120, 132, 101, 134, 90, 230, 210]
  },
  {
    name: 'Product B',
    stack: 'total',
    data: [220, 182, 191, 234, 290, 330, 310]
  }
]
```  


### 10. `data` Property  
**Function**: Sets the bar chart data.  
**Type**: Array<String | Number | Object>  
**Default**: `[]`  
**Required**: Yes  

**Data Formats**:  
- Simple array: `[11, 11, 15, 13, 12, 130, 10]`  
- Object array: `[{value: 11, color: '#ff0000'}, {value: 15, itemStyle: {...}}]`  

**Scenarios**:  
- Essential for all bar charts.  
- Customize individual bar styles.  

**Code Examples**:  
```json
// Simple data  
series: [
  {
    name: 'Simple Data',
    data: [11, 11, 15, 13, 12, 130, 10]
  }
]

// Complex data with custom styles  
series: [
  {
    name: 'Complex Data',
    data: [
      11, 
      { value: 15, color: '#ff0000' },
      { value: 13, itemStyle: { borderColor: '#000', borderWidth: 2 } },
      12, 
      130, 
      10
    ]
  }
]
```  


### Practical Application Example  
Let's integrate these properties in a complete example:  

```typescript
@Entry
@Component
struct SalesChart {
  @State options: Options = new Options({
    title: {
      show: true,
      text: '2023 Quarterly Sales Report',
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
      name: 'Sales (¥10,000)'
    },
    series: [
      {
        name: 'Online Sales',
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
        name: 'Offline Sales',
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
        name: 'Target',
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
      McHorBarChart({ options: this.options })
    }
    .height('50%')
    .width('100%')
  }
}
```  

This example demonstrates:  
1. Stacked bar chart implementation  
2. Gradient color application  
3. Rounded bar customization  
4. Flexible label configuration  
5. Mixed chart types (bar + line)  


### Conclusion  
That wraps up this episode! We hope this guide helps you master the `series` property configuration for the McHorBarChart component. Apply these properties creatively in your projects to build stunning bar chart visualizations. If you have questions, leave them in the comments. See you next time!
