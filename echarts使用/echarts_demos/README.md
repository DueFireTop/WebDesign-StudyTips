> #### 堆叠柱状图
>
>  [chart_demo1.html](chart_demo1.html) 
>
> 示例代码：
>
> ```js
> const seriesData = [
>   // index: 客户1, 2, 3, 4, 5, 6, 7
>   {name: '军品', data: [1, 1, 2, 2, 2, 2, 2]},
>   {name: '民品', data: [1, 1, 6, 2, 2, 2, 9]},
>   {name: '售后', data: [1, 7, 1, 1, 2, 4, 3]},
>   {name: '科研', data: [1, 1, 1, 2, 1, 2, 4]},
> ]
> const totalData = new Array(seriesData[0].data.length).fill(0);
> const totalDataWithNames = []; // 用于存储带有名称的总数据
> 
> seriesData.forEach(function(series) {
>   series.data.forEach(function(value, index) {
>     // totalData[0]表示客户1，以此类推
>     totalData[index] += value;
>     // totalDataWithNames.push({ name: `客户${index + 1}`, value: totalData[index] }); 
>   })
> })
> 
> for (index=0; index < totalData.length; index++){
>   totalDataWithNames.push({name: `客户${index + 1}`, value: `${totalData[index]}`})
> }
> 
> // 对totalDataWithNames进行排序
> 
> totalDataWithNames.sort((a, b) => b.value - a.value);
> 
> 
> var maxTotalData = Math.max(...totalData);
> 
> option = {
>   xAxis: {
>     max: maxTotalData
>   },
>   yAxis: {
>     type: 'category',
>     // data: ['A', 'B', 'C', 'D', 'E', 'F'],
>     data: [
>       // {value: '客户1'}, '客户2', '客户3', '客户4', '客户5', '客户6', '客户7'
>       {value: '客户1'},
>       {value: '客户2'},
>       {value: '客户3'},
>       {value: '客户4'},
>       {value: '客户5'},
>       {value: '客户6'},
>       {value: '客户7'}
>     ],
>     inverse: true,
>     max: 10 // only the largest 3 bars will be displayed
>   },
>   tooltip: {},
>   legend: {
>     data: ['军品', '民品', '售后', '科研'],
>     
>   },
>   series: [
>     {
>       realtimeSort: true,
>       name: 'total',
>       type: 'bar',
>       stack: 'y',
>       data: totalData,
>       label: {
>         show: false, //是否显示汇总
>         position: 'right',
>         valueAnimation: true,
>       },
>       tooltip:{
>         show: false
>       },
>     },
>     
>     // 军品、民品、售后、科研
>     {
>       name: '军品',
>       type: 'bar',
>       stack: 'x',
>       barWidth: '20px',
>       data: seriesData[0].data
>     },
>     {
>       name: '民品',
>       type: 'bar',
>       stack: 'x',
>       barWidth: '20px',
>       data: seriesData[1].data
>     },
>     {
>       name: '售后',
>       type: 'bar',
>       stack: 'x',
>       barWidth: '20px',
>       data: seriesData[2].data
>     },
>     {
>       name: '科研',
>       type: 'bar',
>       stack: 'x',
>       barWidth: '20px',
>       data: seriesData[3].data,
>       
>       showBackground: true,
>       // barGap: '-100%',
>       backgroundColor: {
>         color: '#dcee0e8'
>       }
>     },
>   ],
> };
> ```

