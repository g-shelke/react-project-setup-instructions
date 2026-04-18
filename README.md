# React + TypeScript + Vite Starter

[![React](https://img.shields.io/badge/React-61DAFB?logo=react&logoColor=black)](https://react.dev/)
[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![Vite](https://img.shields.io/badge/Vite-646CFF?logo=vite&logoColor=white)](https://vitejs.dev/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3-06B6D4?logo=tailwindcss&logoColor=white)](https://tailwindcss.com/)
[![shadcn/ui](https://img.shields.io/badge/shadcn%2Fui-UI-000000?logo=shadcnui&logoColor=white)](https://ui.shadcn.com/)

A scalable **React + TypeScript** project setup using **Vite**, **Tailwind CSS**, and **shadcn/ui**. Includes mock data generation, a clear folder layout, and conventions suited to production-grade frontend apps.

---

## Table of contents

- [Getting started](#getting-started)
- [Git setup](#git-setup)
- [Authentication (GitHub)](#authentication-github)
- [UI setup](#ui-setup)
- [Mock data generation](#mock-data-generation)
- [Project structure](#project-structure)
- [Tech stack](#tech-stack)
- [Troubleshooting](#troubleshooting)

---

## Getting started

### 1. Create project

```bash
npm create vite@latest my-app -- --template react
cd my-app
```

### 2. Install dependencies

```bash
npm install
```

### 3. Run development server

```bash
npm run dev
```

---

## Git setup

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git push -u origin main
```

---

## Authentication (GitHub)

Use a **GitHub Personal Access Token** instead of your account password when pushing over HTTPS.

- **Tokens:** [github.com/settings/tokens](https://github.com/settings/tokens)

> **Security:** Never commit tokens, paste them into README files, or expose them in client-side code.

---

## UI setup

### Tailwind CSS

```bash
npm install -D tailwindcss@3 postcss autoprefixer
npx tailwindcss init -p
```

### Optional: pnpm

```bash
npm install -g pnpm
```

### References

| Resource    | Link                                      |
| ----------- | ----------------------------------------- |
| Tailwind CSS | [tailwindcss.com](https://tailwindcss.com) |
| shadcn/ui   | [ui.shadcn.com](https://ui.shadcn.com)    |

---

## Mock data generation

Generate realistic fake data with [Faker](https://fakerjs.dev/).

### 1. Create `generateData.ts` (project root)

```typescript
import { faker } from "@faker-js/faker";
import fs from "fs";

const USERS = 1000;

// Users
const users = Array.from({ length: USERS }, (_, i) => ({
  id: i + 1,
  firstName: faker.person.firstName(),
  lastName: faker.person.lastName(),
  email: faker.internet.email().toLowerCase(),
  phone: `+91-${faker.helpers.arrayElement(['6','7','8','9'])}${faker.string.numeric(9)}`,
  address: faker.location.streetAddress(),
  zipCode: `41${faker.string.numeric(4)}`,
  role: i < 2 ? "admin" : "user",
  password: faker.string.alphanumeric(6)
}));

fs.writeFileSync(
  "db.json",
  JSON.stringify({ users }, null, 2)
);
```

### 2. Install dependencies

```bash
npm install @faker-js/faker
npm install -D typescript tsx
```

### 3. Run script

```bash
npx tsx generateData.ts
```

### Output

| Item        | Detail                          |
| ----------- | ------------------------------- |
| File        | `db.json` in the project root   |
| Sample size | 1000 users                      |

---

## Project structure

```text
src/
├── assets/
│   ├── images/
│   ├── icons/
│   └── styles/
├── components/
│   ├── common/
│   ├── layout/
│   └── ui/
├── pages/
│   ├── Home/
│   ├── About/
│   └── Dashboard/
├── hooks/
│   ├── useAuth.ts
│   ├── useApi.ts
│   └── useLocalStorage.ts
├── services/
│   ├── api.ts
│   ├── authService.ts
│   └── userService.ts
├── utils/
│   ├── helpers.ts
│   ├── constants.ts
│   └── validation.ts
├── types/
│   ├── index.ts
│   ├── user.ts
│   └── api.ts
├── contexts/
│   ├── AuthContext.tsx
│   └── ThemeContext.tsx
├── lib/
│   └── axios.ts
├── styles/
│   ├── globals.css
│   ├── theme.ts
│   └── variables.css
├── constants/
│   ├── routes.ts
│   └── config.ts
├── mocks/
│   └── data.ts
├── App.tsx
├── main.tsx
└── index.css
```

---

## Tech stack

| Category   | Technology        |
| ---------- | ----------------- |
| Framework  | React (Vite)      |
| Language   | TypeScript        |
| Styling    | Tailwind CSS      |
| Components | shadcn/ui         |
| Mock data  | Faker (`@faker-js/faker`) |

---

## Troubleshooting

If Tailwind or other dependencies fail to install or resolve:

```bash
rm -rf node_modules package-lock.json
npm install
npm install -D tailwindcss@3 postcss autoprefixer
npx tailwindcss init -p
```
