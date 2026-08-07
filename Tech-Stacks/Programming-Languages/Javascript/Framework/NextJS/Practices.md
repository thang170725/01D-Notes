```bash
Next.js (web-ssr)
frontend/web-ssr/
├── public/assets/logo.png
├── src/app/page.jsx
├── src/components/Hello.jsx
├── src/services/user.service.js
├── src/styles/main.css
├── package.json
└── README.md

src/app/page.jsx
import Hello from "../components/Hello";
import { getUserMock } from "../services/user.service";

export default function HomePage() {
  const user = getUserMock();

  return (
    <div style={{ padding: "20px", fontFamily: "sans-serif" }}>
      <h1>Next.js SSR Demo</h1>
      <p>This is Home Page (rendered on server)</p>
      <Hello name={user.name} />
    </div>
  );
}

src/components/Hello.jsx
export default function Hello({ name }) {
  return <h2>Hello {name} 👋</h2>;
}

src/services/user.service.js
export function getUserMock() {
  return { id: 1, name: "Next User" };
}

src/styles/main.css
body {
  margin: 0;
  font-family: sans-serif;
}


✅ Chạy thử Next.js:

cd frontend/web-ssr
npm install
npm run dev
```