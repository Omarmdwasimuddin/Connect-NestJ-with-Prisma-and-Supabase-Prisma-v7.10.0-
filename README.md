## Connect NestJ with Prisma and Supabase (Prisma v7.10.0)

#### Create Project
```bash
nest new my-nest
```
```bash
cd my-nest
```
---

### install @nestjs/config
```bash
npm i @nestjs/config
```

### `app.module.ts`
```bash
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { ConfigModule } from '@nestjs/config';
import { MongooseModule } from '@nestjs/mongoose';

@Module({
  imports: [ ConfigModule.forRoot({ isGlobal: true }) ],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```

#### Prisma install
```bash
npm install -D prisma@7.10.0
```
```bash
npm install @prisma/client@7.10.0
```
>### PostgreSQL Driver Adapter install
>#### Prisma 7 requires a driver adapter for direct PostgreSQL database connections.
```bash
npm install @prisma/adapter-pg pg
```
```bash
npx prisma init
```
---




#### `.env`
>#### DATABASE_URL copy kore paste kore daw.
```bash
DATABASE_URL=''
```
---


#### `schema.prisma`
```bash
generator client {
  provider = "prisma-client"
  output   = "../generated/prisma"
}

datasource db {
  provider = "postgresql"
}


model Book {
  id String @id @default(uuid())
  title String
  author String
  createdAt DateTime @default(now())
}
```
---

#### `prisma.config.ts`
```bash
npm install dotenv
```
```bash
import "dotenv/config";
import { defineConfig, env } from "prisma/config";

export default defineConfig({
  schema: "prisma/schema.prisma",

  migrations: {
    path: "prisma/migrations",
  },

  datasource: {
    url: env("DATABASE_URL"),
  },
});
```
---

#### Create and run your migration & Generate Prisma Client
```bash
npx prisma migrate dev --name init
```
```bash
npx prisma generate
```
<img width="1350" height="351" alt="image" src="https://github.com/user-attachments/assets/a7c8d829-2048-4ec3-97a5-ec72067b2eaa" />

---
