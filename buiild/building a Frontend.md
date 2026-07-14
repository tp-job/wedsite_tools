Build a Frontend

See also: [[building a Backend]] · [[React.js]] · [[Next.js]] · [[Support Tools]] · [[command prompt]] · [[Web Tools MOC]]

```cmd
# react
npm create vite@latest . -- --template react
npm install

# axios and react router
npm install axios react-router-dom

# tailwindcss
npm install tailwindcss @tailwindcss/vite

# chart
npm install recharts

```

vite.config.js
```js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
import tailwindcss from '@tailwindcss/vite'

// https://vite.dev/config/
export default defineConfig({
  server: {
    host: true,  // เปิดให้เข้าถึงจากเครือข่าย
    port: 10005,  // กำหนดพอร์ตใหม่
  },
  plugins: [
    react(),
    tailwindcss(),
  ],
})

```

tailwind.config.js
```js
/** @type {import('tailwindcss').Config} */
export default {
  content: ["./index.html", "./src/**/*.{js,ts,jsx,tsx}"],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

src/index.css
```css
@import "tailwindcss";
```

AppRoute.jsx
```jsx
import { BrowserRouter as Router, Routes, Route, Link } from "react-router-dom";

<Link to="/booking">

<Router>
  <Routes>
    <Route path="/" element={<HomePage />} />
  </Routes>  
</Router>
```


Install Next.js
``` cmd
# install
npx create-next-app@latest my-next-app --typescript

# dependencies
npm install -D eslint prettier eslint-config-next @types/react-dom

```

install
``` cmd
npm install remixicon --save
```

Remixicon
```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/remixicon/4.6.0/remixicon.css" integrity="sha512-kJlvECunwXftkPwyvHbclArO8wszgBGisiLeuDFwNM8ws+wKIw0sv1os3ClWZOcrEB2eRXULYUsm8OVRGJKwGA==" crossorigin="anonymous" referrerpolicy="no-referrer" />
```

Icon N
```html
<link rel="icon" type="image/svg+xml" href="data:image/svg+xml,<svg xmlns=%22http://www.w3.org/2000/svg%22 width=%22256%22 height=%22256%22 viewBox=%220 0 100 100%22><rect width=%22100%22 height=%22100%22 rx=%2250%22 fill=%22%237d6ee7%22></rect><path fill=%22%23fff%22 d=%22M31.93 72.72L31.93 27.28L38.23 27.28L61.38 61.54L61.38 27.28L68.07 27.28L68.07 72.72L61.70 72.72L38.56 38.46L38.56 72.72L31.93 72.72Z%22></path></svg>" />
```


