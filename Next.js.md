> ### 🚀 Tools Used
Next.js (Framework)
Built on top of React, Next.js provides a robust framework for building server-side rendered and statically generated web applications.  
👉 Get Started with Next.js – [nextjs.org](https://nextjs.org/docs/getting-started)

---

### Installation

To create a new Next.js app, run the following command in your terminal:

```bash
npx create-next-app@latest
```

This command will prompt you with a few questions to configure your project. It's recommended to use the App Router, TypeScript, and Tailwind CSS for modern Next.js applications.

### Next.js Project Full Structure

```bash
my-next-app/
├── app/                         # (ใช้ใน App Router - Next.js 13+)
│   ├── layout.tsx               # Layout หลักของแอป (ใช้ครอบทุกหน้า)
│   ├── page.tsx                 # หน้าแรก (Home page)
│   ├── loading.tsx              # แสดงตอนโหลดข้อมูล (optional)
│   ├── error.tsx                # แสดงเมื่อเกิด error (optional)
│   ├── not-found.tsx            # หน้า 404 (optional)
│   ├── favicon.ico
│   ├── globals.css              # CSS หลัก
│   ├── (auth)/                  # Group routes (เช่น login/register)
│   │   ├── layout.tsx
│   │   ├── login/
│   │   │   └── page.tsx
│   │   └── register/
│   │       └── page.tsx
│   ├── dashboard/               # หน้า Dashboard (protected)
│   │   ├── layout.tsx
│   │   ├── page.tsx
│   │   └── settings/
│   │       └── page.tsx
│   └── api/                     # (ถ้าใช้ Route Handler แทน pages/api)
│       ├── route.ts             # ตัวอย่าง API route เดียว
│       └── users/
│           └── route.ts
│
├── components/                  # UI Components ที่ใช้ซ้ำได้
│   ├── ui/                      # ส่วนประกอบเล็ก ๆ เช่น Button, Input, Modal
│   │   ├── Button.tsx
│   │   ├── Input.tsx
│   │   ├── Card.tsx
│   │   └── Modal.tsx
│   ├── layout/                  # Layout components
│   │   ├── Header.tsx
│   │   ├── Sidebar.tsx
│   │   ├── Footer.tsx
│   │   └── Navbar.tsx
│   └── common/                  # Components ที่ใช้ทั่วไป เช่น Loading, EmptyState
│       ├── LoadingSpinner.tsx
│       ├── EmptyState.tsx
│       └── ErrorMessage.tsx
│
├── lib/                         # ฟังก์ชันช่วยเหลือ (helper functions)
│   ├── db.ts                    # การเชื่อมต่อฐานข้อมูล (Prisma / MongoDB)
│   ├── auth.ts                  # การจัดการ Auth logic
│   ├── utils.ts                 # Utility functions
│   ├── api-client.ts            # ฟังก์ชันสำหรับ fetch API
│   └── constants.ts             # ค่าคงที่ต่าง ๆ
│
├── hooks/                       # Custom React Hooks
│   ├── useAuth.ts
│   ├── useTheme.ts
│   └── useFetch.ts
│
├── context/                     # React Contexts (Global State)
│   ├── ThemeContext.tsx
│   ├── AuthContext.tsx
│   └── UIContext.tsx
│
├── styles/                      # Global & module CSS
│   ├── globals.css
│   ├── variables.css
│   └── components/
│       ├── button.module.css
│       └── layout.module.css
│
├── public/                      # Static files เช่น รูป, icon, font
│   ├── images/
│   │   ├── logo.png
│   │   └── avatar.png
│   ├── icons/
│   │   └── favicon.ico
│   └── robots.txt
│
├── middleware.ts                # ใช้สำหรับตรวจสอบ auth / redirect
├── next.config.mjs              # การตั้งค่า Next.js
├── postcss.config.mjs           # ใช้กับ Tailwind หรือ PostCSS
├── tailwind.config.ts           # ถ้าใช้ Tailwind CSS
├── tsconfig.json                # การตั้งค่า TypeScript
├── package.json
└── README.md

```