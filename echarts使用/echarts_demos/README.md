## 1. 堆叠柱状图

效果展示：[echart_demo1.html](echart_demo1.html) 

```js
const seriesData = [
// index: 客户1, 2, 3, 4, 5, 6, 7
{name: '军品', data: [1, 1, 2, 2, 2, 2, 2]},
{name: '民品', data: [1, 1, 6, 2, 2, 2, 9]},
{name: '售后', data: [1, 7, 1, 1, 2, 4, 3]},
{name: '科研', data: [1, 1, 1, 2, 1, 2, 4]},
]
const totalData = new Array(seriesData[0].data.length).fill(0);
const totalDataWithNames = []; // 用于存储带有名称的总数据

seriesData.forEach(function(series) {
series.data.forEach(function(value, index) {
 // totalData[0]表示客户1，以此类推
 totalData[index] += value;
 // totalDataWithNames.push({ name: `客户${index + 1}`, value: totalData[index] }); 
})
})

for (index=0; index < totalData.length; index++){
totalDataWithNames.push({name: `客户${index + 1}`, value: `${totalData[index]}`})
}

// 对totalDataWithNames进行排序

totalDataWithNames.sort((a, b) => b.value - a.value);


var maxTotalData = Math.max(...totalData);

option = {
xAxis: {
 max: maxTotalData
},
yAxis: {
 type: 'category',
 // data: ['A', 'B', 'C', 'D', 'E', 'F'],
 data: [
   // {value: '客户1'}, '客户2', '客户3', '客户4', '客户5', '客户6', '客户7'
   {value: '客户1'},
   {value: '客户2'},
   {value: '客户3'},
   {value: '客户4'},
   {value: '客户5'},
   {value: '客户6'},
   {value: '客户7'}
 ],
 inverse: true,
 max: 10 // only the largest 3 bars will be displayed
},
tooltip: {},
legend: {
 data: ['军品', '民品', '售后', '科研'],

},
series: [
 {
   realtimeSort: true,
   name: 'total',
   type: 'bar',
   stack: 'y',
   data: totalData,
   label: {
     show: false, //是否显示汇总
     position: 'right',
     valueAnimation: true,
   },
   tooltip:{
     show: false
   },
 },

 // 军品、民品、售后、科研
 {
   name: '军品',
   type: 'bar',
   stack: 'x',
   barWidth: '20px',
   data: seriesData[0].data
 },
 {
   name: '民品',
   type: 'bar',
   stack: 'x',
   barWidth: '20px',
   data: seriesData[1].data
 },
 {
   name: '售后',
   type: 'bar',
   stack: 'x',
   barWidth: '20px',
   data: seriesData[2].data
 },
 {
   name: '科研',
   type: 'bar',
   stack: 'x',
   barWidth: '20px',
   data: seriesData[3].data,

   showBackground: true,
   // barGap: '-100%',
   backgroundColor: {
     color: '#dcee0e8'
   }
 },
],
}
```



## 2. Legend对齐

效果展示：[echart_demo2.html](echart_demo2.html) 

```js
option = {
tooltip: {
 trigger: 'item'
},
legend:[
 {
       orient: 'horizontal',
       icon: 'circle',
       align: 'left',
       bottom: '0',
       itemWidth: 8,
       itemHeight: 8,
       y: '20',
       x: 'center',
       data: ['鼻翼煽动，口唇、指甲青紫', '胸闷', '憋气/憋醒'],
       formatter: (name)=> {
         return `{b|${name}} `;
       },
       textStyle: {
         color: '#999999',
         fontSize: 12,
         align: 'left',
         // 文字块背景色，一定要加上，否则对齐不会生效
         backgroundColor: "transparent", 
         rich: {
           b: {
             width: 200,
           },
         },
       },
 },
 {
       orient: 'horizontal',
       icon: 'circle',
       align: 'left',
       bottom: '0',
       itemWidth: 8,
       itemHeight: 8,
       y: '40',
       x: 'center',
       data: ['咳嗽或反复咳嗽', '气促', '没感觉/感觉良好'],
       formatter: (name)=> {
         return `{a|${name}} `;
       },

       textStyle: {
         color: '#999999',
         fontSize: 12,
         align: 'left',
         // 文字块背景色，一定要加上，否则对齐不会生效
         backgroundColor: "transparent", 
         rich: {
           a: {
             width: 200,
           },
         },
       },
 }
 ],
series: [
 {
   name: 'Access From',
   type: 'pie',
   radius: ['40%', '70%'],
   avoidLabelOverlap: false,
   itemStyle: {
     borderRadius: 10,
     borderColor: '#fff',
     borderWidth: 2
   },
   label: {
     show: false,
     position: 'center'
   },
   emphasis: {
     label: {
       show: true,
       fontSize: '40',
       fontWeight: 'bold'
     }
   },
   labelLine: {
     show: false
   },
   data: [
     { value: 1048, name: '咳嗽或反复咳嗽' },
     { value: 735, name: '鼻翼煽动，口唇、指甲青紫' },
     { value: 580, name: '胸闷' },
     { value: 484, name: '憋气/憋醒' },
     { value: 300, name: '气促' },
     { value: 300, name: '没感觉/感觉良好' }
   ]
 }
]
};
```



## 3. 饼图添加内外边框

效果展示： [echarts_demo3.html](echarts_demo3.html) 

```js
option = {
  color: ['#80FFA5', '#00DDFF', '#37A2FF', '#FF0087', '#FFBF00'],
  tooltip: {
    show: false,
    trigger: 'none'
  },
  legend: {
    top: '5%',
    left: 'center',
    data: ['Search Engine', 'Direct', 'Email', 'Union Ads', 'Video Ads'],
  },
  series: [
    {
      name: 'Access From',
      type: 'pie',
      radius: ['40%', '70%'],
      avoidLabelOverlap: false,
      padAngle: 5,
      // itemStyle: {
      //   borderRadius: 10
      // },
      label: {
        show: false,
        position: 'center'
      },
      emphasis: {
        label: {
          show: true,
          fontSize: 40,
          fontWeight: 'bold'
        }
      },
      labelLine: {
        show: false
      },
      data: [
        { value: 1048, name: 'Search Engine' },
        { value: 735, name: 'Direct' },
        { value: 580, name: 'Email' },
        { value: 484, name: 'Union Ads' },
        { value: 300, name: 'Video Ads' }
      ]
    },
    {
      name: '外边框',
      type: 'pie',
      radius: ['71%', '73%'],
      label: {
        normal: {
          show: false
        }
      },
      labelLine: {
        normal: {
          show: false
        }
      },
      data:[
        { value: 1, name: 'demo1' },
        { value: 1, name: 'demo2' },
        { value: 1, name: 'demo3' },
        { value: 1, name: 'demo4' },
        { value: 1, name: 'demo5' },
        { value: 1, name: 'demo6' },
        { value: 1, name: 'demo7' },
        { value: 1, name: 'demo8' },
      ],
      itemStyle: {
        borderColor: 'blue',
        color: 'white'
      },
      emphasis: {
        itemStyle: {
          borderColor: 'blue',
          color: 'white'
        },
      },
      hoverAnimation: false, //鼠标移入变大
    },
    {
      name: '内',
      type: 'pie',
      radius: ['0%', '38%'],
      label: {
        normal: {
          show: false
        }
      },
      labelLine: {
        normal: {
          show: false
        }
      },
      data: [
        { value: 1, name: 'demo' }
      ],
      itemStyle: {
        color: 'red'
      },
      emphasis: {
        itemStyle: {
          color: 'red'
        },
      },
      hoverAnimation: false, //鼠标移入变大
      
    },
  ]
};
```



## 4. 饼图添加内部渐变色背景

效果展示： [echarts_demo4.html](echarts_demo4.html) 

```js
option = {
  color: ['#80FFA5', '#00DDFF', '#37A2FF', '#FF0087', '#FFBF00'],
  tooltip: {
    show: false,
    trigger: 'none'
  },
  legend: {
    top: '5%',
    left: 'center',
    data: ['Search Engine', 'Direct', 'Email', 'Union Ads', 'Video Ads'],
  },
  series: [
    {
      name: 'Access From',
      type: 'pie',
      radius: ['40%', '70%'],
      avoidLabelOverlap: false,
      padAngle: 5,
      // itemStyle: {
      //   borderRadius: 10
      // },
      label: {
        show: false,
        position: 'center'
      },
      emphasis: {
        label: {
          show: true,
          fontSize: 40,
          fontWeight: 'bold'
        }
      },
      labelLine: {
        show: false
      },
      data: [
        { value: 1048, name: 'Search Engine' },
        { value: 735, name: 'Direct' },
        { value: 580, name: 'Email' },
        { value: 484, name: 'Union Ads' },
        { value: 300, name: 'Video Ads' }
      ]
    },
    {
      name: '外边框',
      type: 'pie',
      radius: ['71%', '73%'],
      label: {
        normal: {
          show: false
        }
      },
      labelLine: {
        normal: {
          show: false
        }
      },
      data:[
        { value: 1, name: 'demo1' },
        { value: 1, name: 'demo2' },
        { value: 1, name: 'demo3' },
        { value: 1, name: 'demo4' },
        { value: 1, name: 'demo5' },
        { value: 1, name: 'demo6' },
        { value: 1, name: 'demo7' },
        { value: 1, name: 'demo8' },
      ],
      itemStyle: {
        borderColor: 'blue',
        color: 'white'
      },
      emphasis: {
        itemStyle: {
          borderColor: 'blue',
          color: 'white'
        },
      },
      hoverAnimation: false, //鼠标移入变大
    },
    {
      name: '内边框',
      type: 'pie',
      radius: ['38%', '38%'],
      label: {
        normal: {
          show: false
        }
      },
      labelLine: {
        normal: {
          show: false
        }
      },
      data: [
        { value: 1, name: 'demo' }
      ],
      itemStyle: {
        normal: {
          borderWidth: 1,
          borderColor: 'red',
          color: 'red'
        }
      },
      emphasis: {
        itemStyle: {
          color: 'red'
        },
      },
      hoverAnimation: false, //鼠标移入变大
    },
    {
      name: '背景',
      type: 'pie',
      radius: ['0%', '38%'],
      label: {
        normal: {
          show: false
        }
      },
      labelLine: {
        normal: {
          show: false
        }
      },
      data: [
        { value: 1, name: 'demo' }
      ],
      itemStyle: {
        normal: {
          color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
            {
              offset: 1,
              color: 'red',
            },
            {
              offset: 0,
              color: 'blue'
            }
          ]),
        }
      },
      emphasis: {
        itemStyle: {
          color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
            {
              offset: 0,
              color: 'red',
            },
            {
              offset: 1,
              color: 'blue'
            }
          ]),
        },
      },
      hoverAnimation: false, //鼠标移入变大
    }
  ]
};
```



## 5. 饼图添加虚线外边框

效果展示： [echarts_demo5.html](echarts_demo5.html) 

```js
option = {
    backgroundColor: '#153274',
    tooltip: {
        trigger: 'axis',
        axisPointer: { // 坐标轴指示器，坐标轴触发有效
            type: 'shadow' // 默认为直线，可选为：'line' | 'shadow'
        },
        formatter: "{a} <br/>{b}: {c} ({d}%)"
    },
    legend: {
        orient: 'horizontal',
        //            x: 'right',文字在图例颜色的右边了
        right: 'center',
        bottom: '5%',
        textStyle:{
            color:'#fff'
        },
        //            data数据中若存在''，则表示换行，用''切割。
        data: ['非诉讼', '行政诉讼', '劳动仲裁']
    },
    //        calculable:true,
    series: [{
            type: 'pie',
            radius: ['53%', '55%'],
            center: ['50%', '50%'],
            hoverAnimation: false,
            labelLine: {
                normal: {
                    show: 0,
                },
            },
            itemStyle: {
                normal: {
                    color: function(a) {
                        if (a.data == 2) {
                            return '#5DC3FB';
                        }
                        if (a.data == 1) {
                            return 'rgba(0,0,0, 0)';
                        }
                    },
                },
            },
            data: [2, 1, 2, 1, 2, 1, 2, 1, 2, 1, 2, 1, 2, 1, 2, 1, 2, 1, 2, 1, 2, 1, 2, 1, 2, 1, 2, 1],
        },
        {
            name: '',
            type: 'pie',
            radius: ['0%', '50%'],
            center: ['50%', '50%'],
            startAngle: 190, //设置起始的角度
            avoidLabelOverlap: false,
            hoverAnimation: true,
            /*控制圆环点击不会放大*/

            label: {
                normal: {
                    show: 1,
                    position: 'top',
                    formatter: '{c}%',
                    textStyle: {
                        fontSize: '20',
                        fontWeight: 'bold'
                    }
                },
                emphasis: {
                    show: true,
                    textStyle: {
                        fontSize: '20',
                        fontWeight: 'bold'
                    }
                }
            },
            labelLine: {
                normal: {
                    smooth: true,
                    length: 30,
                    length2: 30,
                    lineStyle: {
                        type: 'dotted',
                    },
                },
            },
            data: [{
                    value: 21,
                    name: '非诉讼',
                    itemStyle: {
                        color: '#26D2FE'
                    }
                },
                {
                    value: 12,
                    name: '行政诉讼',
                    itemStyle: {
                        color: '#BFF2A3'
                    }
                },
                {
                    value: 16,
                    name: '劳动仲裁',
                    itemStyle: {
                        color: '#FF727A'
                    }
                }

            ]
        }
    ]
};
```



## 6. 柱状图柱体顶部添加横线

效果展示： [echarts_demo6.html](echarts_demo6.html) 

```js
let xLength = 15;
let dataAxis = Array.from({ length: xLength }, (item, index) => index);
let data = [];
let rodData = [];
dataAxis.forEach((item, index) => {
  // 设置基础bar数据
  data.push(item + 10);
  // 设置markPoint数据
  rodData.push({
    symbol: 'rect',
    symbolSize: [30, 4],
    xAxis: item,
    yAxis: data[index], // 对应每列基础bar的值
    itemStyle: {
      color: 'red'
    }
  });
});
option = {
  xAxis: {
    type: 'category',
    data: dataAxis,
    axisLabel: {
      color: '#999'
    },
    axisTick: {
      show: false
    },
    axisLine: {
      show: false
    }
  },
  yAxis: {
    axisLine: {
      show: false
    },
    axisTick: {
      show: false
    },
    axisLabel: {
      color: '#999'
    },
    splitLine: {
      show: true,
      lineStyle: {
        color: 'pink',
        opacity: 1
      },
    },
    splitNumber: 3,
  },
  series: [
    {
      name: 'background',
      barGap: '-85%',
       type: 'bar',
      itemStyle: {
        normal: {
          // barBorderRadius: [25, 25, 25, 25],
          borderColor: 'pink',
          color: 'rgba(1, 255, 255, 0.2)'
        }
      },
      data: [30, 30, 30, 30, 30, 30, 30, 30, 30, 30, 30, 30, 30, 30, 30, ],
      barWidth: 30,
    },
    {
      // 基础bar
      name: 'data',
      type: 'bar',
      itemStyle: {
         normal: {
          // barBorderRadius: [25, 25, 25, 25],
          color: 'orange'
        }
        
      },
      data,
      barWidth: 20,
      markPoint: {
        data: rodData
      },
      // barGap: '-100%'
    },
    
  ]
};

```



## 7. 柱状图label插入图片

效果展示： [echarts_demo7.html](echarts_demo7.html) 

```js
let maxNum = 1500;

option = {
  tooltip: {
    trigger: 'axis',
    axisPointer: {
      // Use axis to trigger tooltip
      type: 'shadow' // 'shadow' as default; can also be 'line' or 'shadow'
    }
  },
  // legend: {},
  grid: {
    left: '3%',
    right: '4%',
    bottom: '3%',
    containLabel: true
  },
  xAxis: {
    type: 'value',
    show: false,
  },
  yAxis: {
    type: 'category',
    show: false,
    data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
  },
  series: [
    {
      name: 'img+name',
      type: 'bar',
      stack: 'y',
      barWidth: '30px',
      data: [
        {value: 1},
        {value: 1},
        {value: 1},
        {value: 1},
        {value: 1},
        {value: 1},
        {value: 1},
      ],
      tooltip: {
        show: false
      },
      label: {
        normal: {
          show: true,
          position: 'left',
          color: '#000',
          align: 'left',
          formatter:(params)=> {
            return '{img|}' + params.name
          },
          textStyle: {
            rich: {
              img: {
                width: 20,
                height: 20,
                fontWeight: 600,
                backgroundColor: {
                  image: 'https://img.alicdn.com/imgextra/i4/O1CN01aG16y424E11XsURUd_!!6000000007358-2-tps-206-240.png'
                }
              }
            }
          },
          offset: [20, -30]
        }
      }
      
    },
    {
      name: 'data',
      type: 'bar',
      // stack: 'total',
      label: {
        show: false
      },
      data: [820, 832, 901, 934, 1290, 1330, 1320],
      barGap: '-100%',
      itemStyle: {
        normal: {
          // barBorderRadius: [25, 25, 25, 25],
          color: 'orange'
        }
      }
    },
    {
      name: 'background',
      type: 'bar',
      // stack: 'total',
      label: {
        show: false
      },
      data: [maxNum, maxNum, maxNum, maxNum, maxNum, maxNum, maxNum],
      barGap: '-100%',
      itemStyle: {
        normal: {
          // barBorderRadius: [25, 25, 25, 25],
          borderColor: 'pink',
          color: 'rgba(1, 255, 255, 0.2)'
        }
        
      }
    }
  ]
};
```

### 柱状图label插入不同图片

```js
let maxNum = 1500;
let imgUrl1 = 'https://img.51miz.com/Element/01/01/40/01/ff0a6c01_E1014001_1cc0c367.jpg';
let imgUrl2 = 'https://tse2-mm.cn.bing.net/th/id/OIP-C.T0MhJBmie5tk4TnJuFZeaQAAAA?rs=1&pid=ImgDetMain';
let data = [
  {value: '1400', name: 'Sun', imgUrl: imgUrl1},
  {value: '1100', name: 'Mon', imgUrl: imgUrl2},
]

// let imgData = [];

option = {
  tooltip: {
    trigger: 'axis',
    axisPointer: {
      // Use axis to trigger tooltip
      type: 'shadow' // 'shadow' as default; can also be 'line' or 'shadow'
    }
  },
  // legend: {},
  grid: {
    left: '3%',
    right: '4%',
    bottom: '3%',
    containLabel: true
  },
  xAxis: {
    type: 'value',
    show: false,
  },
  yAxis: {
    type: 'category',
    show: false,
    data: [data[0].name, data[1].name]
  },
  series: [
    {
      name: 'img+name',
      type: 'bar',
      stack: 'y',
      barWidth: '30px',
      // data: [
      //   {value: 1},
      //   {value: 1},
      //   {value: 1},
      //   {value: 1},
      //   {value: 1},
      //   {value: 1},
      //   {value: 1},
      // ],
      // data: data,
      data: data.map(item =>{
        return {
          value: item.value,
          label: {
            normal: {
              show: true,
              position: 'left',
              color: '#000',
              align: 'left',
              formatter:(params)=> {
                return '{img|}' + params.name
              },
              textStyle: {
                rich: {
                  img: {
                    width: 20,
                    height: 20,
                    fontWeight: 600,
                    backgroundColor: {
                      image: item.imgUrl
                    }
                  }
                }
              },
              offset: [20, -30]
            }
          }
        }
      }),
      tooltip: {
        show: false
      },
      // label: {
      //   normal: {
      //     show: true,
      //     position: 'left',
      //     color: '#000',
      //     align: 'left',
      //     formatter:(params)=> {
      //       return '{img|}' + params.name
      //     },
      //     textStyle: {
      //       rich: {
      //         img: {
      //           width: 20,
      //           height: 20,
      //           fontWeight: 600,
      //           backgroundColor: {
      //             image: imgUrl1
      //           }
      //         }
      //       }
      //     },
      //     offset: [20, -30]
      //   }
      // }
      
    },
    {
      name: 'data',
      type: 'bar',
      // stack: 'total',
      label: {
        show: false
      },
      data: data,
      barGap: '-100%',
      itemStyle: {
        normal: {
          // barBorderRadius: [25, 25, 25, 25],
          color: 'orange'
        }
      }
    },
    {
      name: 'background',
      type: 'bar',
      // stack: 'total',
      label: {
        show: false
      },
      data: [maxNum, maxNum, maxNum, maxNum, maxNum, maxNum, maxNum],
      barGap: '-100%',
      itemStyle: {
        normal: {
          // barBorderRadius: [25, 25, 25, 25],
          borderColor: 'pink',
          color: 'rgba(1, 255, 255, 0.2)'
        }
        
      }
    }
  ]
};
```



## 8. 柱状图实时排序

效果展示： [echarts_demo8.html](echarts_demo8.html) 

```js
let maxNum = 1500;

option = {
  tooltip: {
    trigger: 'axis',
    axisPointer: {
      // Use axis to trigger tooltip
      type: 'shadow' // 'shadow' as default; can also be 'line' or 'shadow'
    }
  },
  // legend: {},
  grid: {
    left: '3%',
    right: '4%',
    bottom: '3%',
    containLabel: true
  },
  xAxis: {
    type: 'value',
    show: false,
  },
  yAxis: {
    type: 'category',
    show: false,
    data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],
    
    // 排序
    inverse: true,
    animationDuration: 300,
    animationDurationUpdate: 300
  },
  series: [
    {
      name: 'img+name',
      type: 'bar',
      stack: 'y',
      barWidth: '30px',
      data: [
        {value: 1},
        {value: 1},
        {value: 1},
        {value: 1},
        {value: 1},
        {value: 1},
        {value: 1},
      ],
      tooltip: {
        show: false
      },
      label: {
        normal: {
          show: true,
          position: 'left',
          color: '#000',
          align: 'left',
          formatter:(params)=> {
            return '{img|}' + params.name
          },
          textStyle: {
            rich: {
              img: {
                width: 20,
                height: 20,
                fontWeight: 600,
                backgroundColor: {
                  image: 'https://img.alicdn.com/imgextra/i4/O1CN01aG16y424E11XsURUd_!!6000000007358-2-tps-206-240.png'
                }
              }
            }
          },
          offset: [20, -30]
        }
      }
      
    },
    {
      name: 'data',
      type: 'bar',
      // stack: 'total',
      realtimeSort: true, // 开启实时排序
      label: {
        show: true
      },
      data: [820, 1000, 901, 934, 1250, 1100, 1200],
      barGap: '-100%',
      itemStyle: {
        normal: {
          // barBorderRadius: [25, 25, 25, 25],
          color: 'orange'
        }
      }
    },
    {
      name: 'background',
      type: 'bar',
      // stack: 'total',
      label: {
        show: false
      },
      data: [maxNum, maxNum, maxNum, maxNum, maxNum, maxNum, maxNum],
      barGap: '-100%',
      itemStyle: {
        normal: {
          // barBorderRadius: [25, 25, 25, 25],
          borderColor: 'pink',
          color: 'rgba(1, 255, 255, 0.2)'
        }
        
      }
    }
  ]
};
```

### 柱状图实时排序改进

效果展示： [echarts_demo9.html](echarts_demo9.html) 

```js
let maxNum = 1500;
var seriesData = [
  {name: '商品1', data: 1000},
  {name: '商品2', data: 1500},
  {name: '商品3', data: 1050},
  {name: '商品4', data: 1300},
  {name: '商品5', data: 1100},
  {name: '商品6', data: 1200},
  {name: '商品7', data: 1400},
]

option = {
  tooltip: {
    trigger: 'axis',
    axisPointer: {
      // Use axis to trigger tooltip
      type: 'shadow' // 'shadow' as default; can also be 'line' or 'shadow'
    }
  },
  // legend: {},
  grid: {
    left: '3%',
    right: '4%',
    bottom: '3%',
    containLabel: true
  },
  xAxis: {
    type: 'value',
    show: false,
  },
  yAxis: {
    type: 'category',
    show: false,
    // data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],
    data: [
      seriesData[0].name, seriesData[1].name, seriesData[2].name,
      seriesData[3].name, seriesData[4].name, seriesData[5].name,
      seriesData[6].name
      ],
    
    // 排序
    inverse: true,
    animationDuration: 300,
    animationDurationUpdate: 300
  },
  series: [
    {
      name: 'img+name',
      type: 'bar',
      stack: 'y',
      barWidth: '30px',
      data: [
        {value: 1},
        {value: 1},
        {value: 1},
        {value: 1},
        {value: 1},
        {value: 1},
        {value: 1},
      ],
      tooltip: {
        show: false
      },
      label: {
        normal: {
          show: true,
          position: 'left',
          color: '#000',
          align: 'left',
          formatter:(params)=> {
            return '{img|}' + params.name
          },
          textStyle: {
            rich: {
              img: {
                width: 20,
                height: 20,
                fontWeight: 600,
                backgroundColor: {
                  image: 'https://img.alicdn.com/imgextra/i4/O1CN01aG16y424E11XsURUd_!!6000000007358-2-tps-206-240.png'
                }
              }
            }
          },
          offset: [20, -30]
        }
      }
      
    },
    {
      name: 'data',
      type: 'bar',
      // stack: 'total',
      realtimeSort: true, // 开启实时排序
      label: {
        show: true
      },
      // data: [820, 1000, 901, 934, 1250, 1100, 1200],
      data: [
        seriesData[0].data, seriesData[1].data, seriesData[2].data,
        seriesData[3].data, seriesData[4].data, seriesData[5].data,
        seriesData[6].data
        ],
      barGap: '-100%',
      itemStyle: {
        normal: {
          // barBorderRadius: [25, 25, 25, 25],
          color: 'orange'
        }
      }
    },
    {
      name: 'background',
      type: 'bar',
      // stack: 'total',
      label: {
        show: false
      },
      data: [maxNum, maxNum, maxNum, maxNum, maxNum, maxNum, maxNum],
      barGap: '-100%',
      itemStyle: {
        normal: {
          // barBorderRadius: [25, 25, 25, 25],
          borderColor: 'pink',
          color: 'rgba(1, 255, 255, 0.2)'
        }
        
      }
    }
  ]
};
```



## 9. 点击echarts图表内容，弹出ei对话框

```vue
<template>
  <div>
    <!-- 图表容器 -->
    <div id="chart" style="width: 600px; height: 400px;"></div>

    <!-- Element UI对话框 -->
    <el-dialog
      title="图表数据详情"
      :visible.sync="dialogVisible"
      width="30%">
      <span>数据名称：{{ dialogData.name }}</span><br>
      <span>数据值：{{ dialogData.value }}</span>
      <span slot="footer" class="dialog-footer">
        <el-button @click="dialogVisible = false">取消</el-button>
      </span>
    </el-dialog>
  </div>
</template>

<script>
import * as echarts from 'echarts';
import { ElDialog, ElButton } from 'element-ui';

export default {
  components: {
    ElDialog,
    ElButton
  },
  data() {
    return {
      chart: null, // ECharts实例
      dialogVisible: false, // 对话框可见性
      dialogData: {} // 对话框显示的数据
    };
  },
  mounted() {
    // 初始化ECharts实例
    this.chart = echarts.init(document.getElementById('chart'));

    // 配置ECharts选项
    var option = {
      // ... 你的ECharts配置选项
      series: [{
        data: [
          { name: 'A', value: 10 },
          { name: 'B', value: 20 },
          // ... 其他数据
        ],
        type: 'bar'
      }]
    };

    // 应用配置选项
    this.chart.setOption(option);

    // 监听图表点击事件
    this.chart.on('click', this.handleChartClick);
  },
  methods: {
    handleChartClick(params) {
      // 更新对话框数据
      this.dialogData = params.data;
      // 显示对话框
      this.dialogVisible = true;
    }
  },
  beforeDestroy() {
    // 销毁ECharts实例，避免内存泄漏
    if (this.chart) {
      this.chart.dispose();
    }
  }
};
</script>

<style scoped>
/* 你的样式 */
</style>
```

