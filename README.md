# tourism-mis
import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Table } from "@/components/ui/table";
import { BarChart, Bar, XAxis, YAxis, CartesianGrid, Tooltip, Legend } from "recharts";

export default function TourismMIS() {
  const [products, setProducts] = useState([]);
  const [newProduct, setNewProduct] = useState({ name: "", category: "", price: "", stock: "" });
  const [orders, setOrders] = useState([]);

  const addProduct = () => {
    if (newProduct.name && newProduct.category && newProduct.price && newProduct.stock) {
      setProducts([...products, { ...newProduct, id: products.length + 1 }]);
      setNewProduct({ name: "", category: "", price: "", stock: "" });
    }
  };

  const placeOrder = (product) => {
    setOrders([...orders, { ...product, orderId: orders.length + 1 }]);
  };

  return (
    <div className="p-6">
      <h1 className="text-2xl font-bold mb-4">旅游管理信息系统模拟器</h1>
      
      {/* 产品上架 */}
      <Card className="mb-4 p-4">
        <h2 className="text-xl font-bold mb-2">添加旅游产品</h2>
        <div className="grid grid-cols-4 gap-2">
          <Input placeholder="产品名称" value={newProduct.name} onChange={(e) => setNewProduct({ ...newProduct, name: e.target.value })} />
          <Input placeholder="类别（酒店/景点/线路）" value={newProduct.category} onChange={(e) => setNewProduct({ ...newProduct, category: e.target.value })} />
          <Input placeholder="价格" type="number" value={newProduct.price} onChange={(e) => setNewProduct({ ...newProduct, price: e.target.value })} />
          <Input placeholder="库存" type="number" value={newProduct.stock} onChange={(e) => setNewProduct({ ...newProduct, stock: e.target.value })} />
          <Button onClick={addProduct}>添加产品</Button>
        </div>
      </Card>

      {/* 产品列表 */}
      <Card className="mb-4 p-4">
        <h2 className="text-xl font-bold mb-2">产品列表</h2>
        <Table>
          <thead>
            <tr>
              <th>名称</th>
              <th>类别</th>
              <th>价格</th>
              <th>库存</th>
              <th>操作</th>
            </tr>
          </thead>
          <tbody>
            {products.map((product) => (
              <tr key={product.id}>
                <td>{product.name}</td>
                <td>{product.category}</td>
                <td>{product.price}</td>
                <td>{product.stock}</td>
                <td><Button onClick={() => placeOrder(product)}>下单</Button></td>
              </tr>
            ))}
          </tbody>
        </Table>
      </Card>

      {/* 订单数据分析 */}
      <Card className="p-4">
        <h2 className="text-xl font-bold mb-2">订单数据分析</h2>
        <BarChart width={600} height={300} data={orders}>
          <CartesianGrid strokeDasharray="3 3" />
          <XAxis dataKey="name" />
          <YAxis />
          <Tooltip />
          <Legend />
          <Bar dataKey="price" fill="#8884d8" />
        </BarChart>
      </Card>
    </div>
  );
}
