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

>#### Select Direct Connection string and Session pooler
<img width="714" height="614" alt="image" src="https://github.com/user-attachments/assets/2201f575-8976-468a-afd1-45ea81cc575a" />

>#### Copy Connection string
<img width="722" height="303" alt="image" src="https://github.com/user-attachments/assets/92ca057a-09eb-434c-b75b-010145e92622" />


#### `.env`
>#### Copy kora url paste kore daw.
```bash
DATABASE_URL=""
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

model User {
  id                String    @id @default(cuid())
  email             String    @unique
  password          String    // bcrypt hash, plain text kokhono na

  // Account lockout tracking
  failedLoginAttempts Int      @default(0)
  lockoutUntil        DateTime?

  // Timestamps
  createdAt         DateTime  @default(now())
  updatedAt         DateTime  @updatedAt

  @@index([email])
  @@map("users")
}
```
---

#### Create and run your migration & Generate Prisma Client
```bash
npx prisma migrate dev --name init
```
```bash
npx prisma generate
```
<img width="1475" height="268" alt="image" src="https://github.com/user-attachments/assets/5a568af1-411c-4159-a08c-14cc1494d03c" />

---
