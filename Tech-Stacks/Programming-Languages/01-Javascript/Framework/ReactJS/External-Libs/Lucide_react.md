# lucide-react
**installation**
```bash
npm install lucide-react
```
**website lấy icons**
```bash
1. https://lucide.dev/icons
```
# fontawesome
**Installation**
```bash
1. npm install @fortawesome/react-fontawesome
2. npm install @fortawesome/fontawesome-svg-core
3. npm install @fortawesome/free-solid-svg-icons
4. npm install @fortawesome/free-regular-svg-icons
5. npm install @fortawesome/free-brands-svg-icons
```
**Ex**
```js
import React from "react";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faCoffee } from "@fortawesome/free-solid-svg-icons";

function App() {
  return (
    <div>
      <h1>Ví dụ Font Awesome</h1>
      <FontAwesomeIcon icon={faCoffee} />
    </div>
  );
}

export default App;
```