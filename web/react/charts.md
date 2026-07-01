# Recharts
`Recharts` is a popular **React chart library** for creating graphs (line chart, bar chart, pie chart, area chart, etc.).

## 1. Install Recharts

Inside your React project:

```bash
npm install recharts
```

or

```bash
yarn add recharts
```

---

## 2. Basic Line Chart Example

Create a component:

`Chart.jsx`

```jsx
import React from "react";
import {
  LineChart,
  Line,
  XAxis,
  YAxis,
  CartesianGrid,
  Tooltip,
  Legend,
  ResponsiveContainer
} from "recharts";


const Chart = () => {


  const data = [
    {
      name: "Jan",
      sales: 4000
    },
    {
      name: "Feb",
      sales: 3000
    },
    {
      name: "Mar",
      sales: 5000
    },
    {
      name: "Apr",
      sales: 7000
    },
  ];


  return (

    <div style={{width:"600px", height:"400px"}}>

      <ResponsiveContainer width="100%" height="100%">

        <LineChart data={data}>


          <CartesianGrid strokeDasharray="3 3"/>


          <XAxis dataKey="name"/>


          <YAxis/>


          <Tooltip/>


          <Legend/>


          <Line
            type="monotone"
            dataKey="sales"
            stroke="#8884d8"
            strokeWidth={3}
          />


        </LineChart>

      </ResponsiveContainer>


    </div>

  );
};


export default Chart;
```

---

## 3. Use in App.jsx

```jsx
import Chart from "./Chart";


function App(){

  return (

    <div>

      <h1>
        Sales Chart
      </h1>

      <Chart/>

    </div>

  )

}


export default App;
```

Output:

```
Sales
7000 |          *
5000 |      *
4000 |  *
3000 |    *
     ----------------
       Jan Feb Mar Apr
```

---

# Important Recharts Components

## Line Chart

```jsx
<LineChart>
  <Line/>
</LineChart>
```

Used for:

- sales
    
- users
    
- growth
    

---

## Bar Chart

Example:

```jsx
import {
 BarChart,
 Bar,
 XAxis,
 YAxis
} from "recharts";


const data=[
 {
  name:"Jan",
  value:100
 },
 {
  name:"Feb",
  value:200
 }
];


<BarChart width={500} height={300} data={data}>

<XAxis dataKey="name"/>

<YAxis/>

<Bar
 dataKey="value"
 fill="#8884d8"
/>

</BarChart>
```

Result:

```
Jan ███
Feb ███████
```

---

## Pie Chart

```jsx
import {
 PieChart,
 Pie,
 Cell
} from "recharts";


const data=[
 {name:"Chrome", value:400},
 {name:"Firefox", value:300},
 {name:"Edge", value:200}
];


<PieChart width={400} height={400}>

<Pie
 data={data}
 dataKey="value"
 cx="50%"
 cy="50%"
 outerRadius={120}
>

</Pie>

</PieChart>
```

---

## Area Chart

```jsx
import {
 AreaChart,
 Area
} from "recharts";


<AreaChart width={500} height={300} data={data}>

<Area
 type="monotone"
 dataKey="sales"
/>

</AreaChart>
```

---

# Responsive Chart (Recommended)

For Tailwind:

```jsx
<div className="w-full h-96">

<ResponsiveContainer>

<LineChart data={data}>

...

</LineChart>

</ResponsiveContainer>

</div>
```

---

# Fetch API Data Example

```jsx
const [users,setUsers]=useState([]);


useEffect(()=>{

 fetch("/api/users")
 .then(res=>res.json())
 .then(data=>setUsers(data))

},[]);


return (

<LineChart data={users}>

<Line
 dataKey="count"
/>

</LineChart>

)
```

---

# Common Props

### XAxis

```jsx
<XAxis dataKey="month"/>
```

takes x-axis value

### Line

```jsx
<Line
 dataKey="sales"
 stroke="red"
/>
```

what data to show

### Tooltip

```jsx
<Tooltip/>
```

shows data on hover

### Legend

```jsx
<Legend/>
```

shows chart labels

---

Recharts is commonly used for:

- Admin dashboard
    
- Analytics page
    
- E-commerce sales
    
- User statistics
    
- Finance dashboard
    

with React + Tailwind + DaisyUI.


--------------

Yes, **most Recharts charts use X-axis and Y-axis** because they represent data in a coordinate system.

Basic idea:

```
          Y-axis
            ↑
            |
  7000      |             *
            |
  5000      |        *
            |
  3000      |   *
            |
            |________________→ X-axis
                Jan Feb Mar
```

- **X-axis (horizontal)** → categories/time/input values
    
- **Y-axis (vertical)** → numbers/measurements
    

---

## 1. Line Chart (most common)

Example: Monthly sales

Data:

```javascript
const data = [
  {
    month:"Jan",
    sales:4000
  },
  {
    month:"Feb",
    sales:6000
  },
  {
    month:"Mar",
    sales:8000
  }
];
```

Chart:

```jsx
<LineChart width={500} height={300} data={data}>

  <XAxis 
    dataKey="month"
  />

  <YAxis />


  <Line
    dataKey="sales"
  />

</LineChart>
```

Output:

```
Y
8000 |          *
6000 |     *
4000 | *
     ----------------
       Jan Feb Mar
              X
```

X-axis:

```
month
```

Y-axis:

```
sales
```

---

## 2. Bar Chart

Example: Product sales

Data:

```javascript
const data=[
 {
  product:"Phone",
  sales:200
 },
 {
  product:"Laptop",
  sales:500
 }
]
```

Code:

```jsx
<BarChart data={data}>

<XAxis dataKey="product"/>

<YAxis/>


<Bar 
 dataKey="sales"
/>

</BarChart>
```

Output:

```
sales
500 |       █
200 | █     █
    ----------------
     Phone Laptop
```

X-axis:

```
products
```

Y-axis:

```
sales amount
```

---

## 3. Area Chart

Used for growth:

```jsx
<AreaChart data={data}>

<XAxis dataKey="month"/>

<YAxis/>


<Area
 dataKey="users"
/>

</AreaChart>
```

Example:

```
Users
 ^
 |
 |        /\
 |       /  \
 |______/____\____
    Jan Feb Mar
```

---

## 4. Scatter Chart

Here both axes are numbers.

Example:

```
Height vs Weight
```

Data:

```javascript
[
 {
  height:170,
  weight:65
 },
 {
  height:180,
  weight:80
 }
]
```

Code:

```jsx
<ScatterChart>

<XAxis 
 dataKey="height"
/>


<YAxis
 dataKey="weight"
/>


<Scatter data={data}/>

</ScatterChart>
```

Result:

```
Weight
 80 |       *
 65 |   *
    ----------------
      Height
```

---

## But not all charts need X/Y

### Pie Chart

No axis:

```jsx
<PieChart>

<Pie
 data={data}
 dataKey="value"
/>

</PieChart>
```

Because it shows percentage:

```
Chrome 40%
Firefox 30%
Edge 30%
```

---

### Summary

|Chart|X Axis|Y Axis|
|---|---|---|
|Line Chart|✅|✅|
|Bar Chart|✅|✅|
|Area Chart|✅|✅|
|Scatter Chart|✅|✅|
|Pie Chart|❌|❌|
|Radar Chart|❌|❌|

For dashboards, normally you will use:

- LineChart → sales/user growth
    
- BarChart → comparison
    
- PieChart → percentage
    
- AreaChart → trends
    

Most real projects use XAxis + YAxis charts.

---------------
হ্যাঁ, React এ **Recharts ছাড়াও অনেক chart library** আছে। Project অনুযায়ী আলাদা আলাদা library use করা হয়।

### 1. Chart.js + React wrapper

সবচেয়ে popular chart library।

Install:

```bash
npm install chart.js react-chartjs-2
```

Example:

```jsx
import {
 Line
} from "react-chartjs-2";


const data = {
 labels:["Jan","Feb","Mar"],
 datasets:[
  {
   label:"Sales",
   data:[4000,6000,8000]
  }
 ]
};


function App(){

 return (
   <Line data={data}/>
 )
}
```

Use:

- Dashboard
    
- Analytics
    
- Business reports
    

---

### 2. Apache ECharts (echarts-for-react)

Install:

```bash
npm install echarts echarts-for-react
```

Example:

```jsx
import ReactECharts from "echarts-for-react";


const option = {

 xAxis:{
  type:"category",
  data:["Jan","Feb","Mar"]
 },

 yAxis:{
  type:"value"
 },

 series:[
  {
   data:[10,20,30],
   type:"line"
  }
 ]

};


function App(){

 return (
  <ReactECharts option={option}/>
 )

}
```

Features:

- Very powerful
    
- Animation
    
- Large data
    
- 3D support
    

---

### 3. Victory

Install:

```bash
npm install victory
```

Example:

```jsx
import {
 VictoryLine
} from "victory";


<VictoryLine
 data={[
  {x:1,y:5},
  {x:2,y:10}
 ]}
/>
```

Good for:

- React native
    
- Simple charts
    

---

### 4. Nivo

Install:

```bash
npm install @nivo/line
```

Example:

```jsx
import {ResponsiveLine} from "@nivo/line";


<ResponsiveLine
 data={data}
/>
```

Features:

- Beautiful UI
    
- Modern dashboards
    

---

### 5. D3.js

Install:

```bash
npm install d3
```

Low level library.

Example:

```javascript
import * as d3 from "d3";
```

Used by:

- Custom visualization
    
- Complex graphs
    

---

### 6. Plotly.js React

Install:

```bash
npm install react-plotly.js plotly.js
```

Features:

- Scientific charts
    
- 3D
    
- Maps
    

---

## Comparison

|Library|Easy|Power|Best For|
|---|---|---|---|
|Recharts|⭐⭐⭐⭐⭐|⭐⭐⭐|React dashboard|
|Chart.js|⭐⭐⭐⭐⭐|⭐⭐⭐⭐|General charts|
|ECharts|⭐⭐⭐|⭐⭐⭐⭐⭐|Big data|
|Nivo|⭐⭐⭐⭐|⭐⭐⭐⭐|Beautiful UI|
|Victory|⭐⭐⭐⭐|⭐⭐⭐|Simple apps|
|D3.js|⭐⭐|⭐⭐⭐⭐⭐|Custom visualization|
|Plotly|⭐⭐⭐|⭐⭐⭐⭐⭐|Scientific data|

For **React + Tailwind + DaisyUI admin dashboard**, I would choose:

1. **Recharts** → easiest
    
2. **Nivo** → best looking
    
3. **ECharts** → professional large dashboard
    

Most companies use Recharts/Chart.js/Nivo.