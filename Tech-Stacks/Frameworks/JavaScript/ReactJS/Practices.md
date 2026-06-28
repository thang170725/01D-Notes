import { useState, useEffect, useRef } from "react";

function Demo() {
  // 1. Hiển thị ra UI
  const [count, setCount] = useState(0);

  // 2. Lưu số lần render (không hiển thị)
  const renderCount = useRef(0);

  // 3. Chạy sau khi render xong
  useEffect(() => {
    console.log("UI render xong");
  });

  renderCount.current += 1;

  return (
    <div>
      <h2>Count (useState): {count}</h2>
      <h3>Render count (useRef): {renderCount.current}</h3>

      <button onClick={() => setCount(count + 1)}>
        Click
      </button>
    </div>
  );
}