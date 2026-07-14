See also: [[Next.js]] · [[React-and-MongoDB]] · [[building a Frontend]] · [[Web Tools MOC]]

> ### 🚀 Tools Used
React (Framework)
Built from scratch using React’s component-based architecture.  
👉 Build a React App from Scratch – [React.dev](https://react.dev/learn/build-a-react-app-from-scratch)

---

### Installation

To create a new React app, run the following command in your terminal:

```bash
npm create vite@latest
```

This will create a new folder called `my-app` with all the necessary files to start your React application.

### React.js Project Full Structure

```
my-react-app/
├── public/                         # Static files (เข้าถึงได้โดยตรงผ่าน URL)
│   ├── index.html                  # หน้า HTML หลัก (root)
│   ├── favicon.ico
│   ├── manifest.json
│   ├── robots.txt
│   └── assets/                     # รูปภาพ, icon, font, etc.
│       ├── images/
│       │   ├── logo.png
│       │   └── background.jpg
│       └── fonts/
│           └── Poppins-Regular.ttf
│
├── src/                            # โฟลเดอร์หลักของ React app
│   ├── main.tsx                    # Entry point ของแอป (สำหรับ React 18+)
│   ├── App.tsx                     # Root component (wrap routes/layouts)
│   ├── index.css                   # CSS รวมทั้งหมด
│
│   ├── assets/                     # ไฟล์ Static ภายใน src
│   │   ├── icons/
│   │   │   ├── edit.svg
│   │   │   └── delete.svg
│   │   └── images/
│   │       ├── hero.jpg
│   │       └── banner.png
│
│   ├── components/                 # ส่วนประกอบ UI ที่ใช้ซ้ำได้
│   │   ├── ui/                     # Component เล็ก ๆ เช่นปุ่ม / input
│   │   │   ├── Button.tsx
│   │   │   ├── Input.tsx
│   │   │   ├── Modal.tsx
│   │   │   └── Card.tsx
│   │   ├── layout/                 # โครงสร้างหลักของหน้า
│   │   │   ├── Navbar.tsx
│   │   │   ├── Sidebar.tsx
│   │   │   ├── Footer.tsx
│   │   │   └── Header.tsx
│   │   ├── charts/                 # Component สำหรับ charts (ถ้ามี)
│   │   │   ├── LineChart.tsx
│   │   │   └── PieChart.tsx
│   │   └── common/                 # Component ที่ใช้ทั่วไป
│   │       ├── LoadingSpinner.tsx
│   │       ├── EmptyState.tsx
│   │       └── ErrorMessage.tsx
│
│   ├── layouts/                    # Layout หลัก (ครอบแต่ละ page)
│   │   ├── MainLayout.tsx          # Layout หลักของแอป
│   │   ├── AuthLayout.tsx          # Layout สำหรับหน้า login/register
│   │   └── DashboardLayout.tsx     # Layout ของ dashboard
│
│   ├── pages/                      # หน้าแต่ละหน้า (ถ้าไม่ได้ใช้ React Router)
│   │   ├── Home.tsx
│   │   ├── About.tsx
│   │   ├── Contact.tsx
│   │   ├── Login.tsx
│   │   ├── Register.tsx
│   │   └── Dashboard/
│   │       ├── Index.tsx
│   │       ├── Users.tsx
│   │       └── Settings.tsx
│
│   ├── routes/                     # จัดการ routing (ถ้าใช้ react-router-dom)
│   │   ├── index.tsx               # Routes หลัก
│   │   └── ProtectedRoute.tsx      # Route ที่ต้อง login ก่อนเข้า
│
│   ├── context/                    # React Context API (Global State)
│   │   ├── AuthContext.tsx
│   │   ├── ThemeContext.tsx
│   │   └── AppContext.tsx
│
│   ├── hooks/                      # Custom Hooks
│   │   ├── useAuth.ts
│   │   ├── useTheme.ts
│   │   ├── useFetch.ts
│   │   └── useDebounce.ts
│
│   ├── services/                   # สำหรับติดต่อ API / Database
│   │   ├── apiClient.ts            # ตั้งค่า axios หรือ fetch
│   │   ├── userService.ts          # ฟังก์ชันเกี่ยวกับ users
│   │   ├── authService.ts          # ฟังก์ชัน login/logout/register
│   │   └── noteService.ts          # ตัวอย่าง CRUD API
│
│   ├── utils/                      # ฟังก์ชันช่วยเหลือ (utility functions)
│   │   ├── formatDate.ts
│   │   ├── generateId.ts
│   │   ├── localStorage.ts
│   │   ├── constants.ts
│   │   └── validators.ts
│
│   ├── styles/                     # ไฟล์ CSS/SCSS/Tailwind
│   │   ├── globals.css
│   │   ├── variables.css
│   │   ├── themes/
│   │   │   ├── dark.css
│   │   │   └── light.css
│   │   └── components/
│   │       ├── button.css
│   │       └── navbar.css
│
│   ├── store/                      # (optional) ใช้ถ้าใช้ Redux / Zustand
│   │   ├── index.ts
│   │   ├── authSlice.ts
│   │   └── userSlice.ts
│
│   ├── types/                      # TypeScript interfaces
│   │   ├── user.ts
│   │   ├── note.ts
│   │   └── api.ts
│
│   ├── config/                     # config ต่าง ๆ เช่น API_URL, env
│   │   ├── env.ts
│   │   └── constants.ts
│
│   └── tests/                      # Unit / Integration Tests
│       ├── App.test.tsx
│       ├── components/
│       └── hooks/
│
├── .env                            # Environment variables
├── .gitignore
├── package.json
├── tsconfig.json                   # การตั้งค่า TypeScript
├── vite.config.ts                  # ถ้าใช้ Vite (แทน CRA)
├── eslint.config.mjs               # Linter config
├── prettier.config.mjs             # Code formatter
├── tailwind.config.ts              # ถ้าใช้ Tailwind
└── README.md

```


### Fullstack Monorepo

```
my-fullstack-app/
├─ client/                     # React (Frontend)
│  ├─ src/
│  │  ├─ pages/                # เหมือน Next.js /app/
│  │  │  ├─ Home.jsx
│  │  │  ├─ About.jsx
│  │  │  ├─ Dashboard.jsx
│  │  │  └─ index.js
│  │  │
│  │  ├─ components/
│  │  │  ├─ Navbar.jsx
│  │  │  └─ Footer.jsx
│  │  │
│  │  ├─ api/                  # ใช้ fetch() เรียก backend
│  │  │  ├─ users.js
│  │  │  ├─ notes.js
│  │  │  └─ auth.js
│  │  │
│  │  ├─ lib/                  # ฟังก์ชันช่วยเหมือน Next.js /lib
│  │  │  └─ utils.js
│  │  │
│  │  ├─ styles/
│  │  │  └─ globals.css
│  │  │
│  │  ├─ App.jsx
│  │  └─ main.jsx
│  │
│  ├─ package.json
│  ├─ vite.config.js
│  └─ .env
│
├─ server/                     # Express (Backend)
│  ├─ api/
│  │  ├─ users/
│  │  │  └─ index.js
│  │  ├─ notes/
│  │  │  └─ index.js
│  │  └─ auth/
│  │     └─ index.js
│  │
│  ├─ lib/
│  │  └─ db.js
│  │
│  ├─ models/
│  │  ├─ UserModel.js
│  │  └─ NoteModel.js
│  │
│  ├─ middlewares/
│  │  ├─ authMiddleware.js
│  │  └─ errorHandler.js
│  │
│  ├─ server.js
│  ├─ .env
│  └─ package.json
│
├─ database/
│  └─ schema.sql               # โครงสร้างฐานข้อมูล
│
├─ .gitignore
└─ README.md
```

