- [Recharts](#recharts)
---

# Recharts
```bash
- Recharts là thư viện vẽ biểu đồ cho ReactJS, xây dựng dựa trên SVG và D3.
- Dùng để tạo:
  + Bar chart
  + Line chart
  + Pie chart
  + Area chart
  + Composed chart
  + Responsive chart
- https://recharts.org | https://recharts.org/en-US/examples
```
**Installation**
```bash
npm install recharts
```
**Ex: Line Chart**
```js
import {
  LineChart, Line, XAxis, YAxis,
  CartesianGrid, Tooltip, Legend
} from "recharts";

const data = [
  { name: "Jan", uv: 400 },
  { name: "Feb", uv: 300 },
  { name: "Mar", uv: 500 },
];

export default function MyChart() {
  return (
    <LineChart width={400} height={300} data={data}>
      <CartesianGrid strokeDasharray="3 3" />
      <XAxis dataKey="name" />
      <YAxis />
      <Tooltip />
      <Legend />
      <Line type="monotone" dataKey="uv" stroke="#8884d8" />
    </LineChart>
  );
}
```
