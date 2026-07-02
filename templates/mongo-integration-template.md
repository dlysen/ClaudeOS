# MongoDB Integration — [Project Name]

Database layer: **MongoDB via Mongoose** — connection helper, models, and env-driven
config. Optional add-on for off-chain persistence. This is a **server-side** concern —
pairs with the `/backend-boilerplate` skill; never connect to Mongo from the browser.

## Prerequisites
- `core-technology-template.md` (base project) — and a server runtime (Node API,
  Next route handlers, or the `/backend-boilerplate` service)
- A MongoDB URI (Atlas or local)
```bash
npm install mongoose
```

## 1. Env
```env
# .env  (server-side only — NOT prefixed VITE_, never exposed to the client)
MONGODB_URI=mongodb+srv://user:pass@cluster.mongodb.net/[db]?retryWrites=true&w=majority
```
- Never commit `.env` (see `github-setup-template.md`).

## 2. Connection Helper (cached — safe for serverless / hot reload)
```ts
// src/server/db.ts
import mongoose from 'mongoose'

const uri = process.env.MONGODB_URI!
let cached = (global as any)._mongoose ?? { conn: null, promise: null }
;(global as any)._mongoose = cached

export async function connectDB() {
  if (cached.conn) return cached.conn
  if (!cached.promise) cached.promise = mongoose.connect(uri, { bufferCommands: false })
  cached.conn = await cached.promise
  return cached.conn
}
```

## 3. Model
```ts
// src/server/models/Item.ts
import { Schema, model, models } from 'mongoose'

const ItemSchema = new Schema({
  name: { type: String, required: true },
  ownerAddress: { type: String, index: true },   // e.g. wallet from web3-integration
  createdAt: { type: Date, default: Date.now },
})
export const Item = models.Item ?? model('Item', ItemSchema)
```

## 4. Usage (in a route/handler)
```ts
import { connectDB } from '../server/db'
import { Item } from '../server/models/Item'
// await connectDB(); const items = await Item.find().lean()
```

## 5. Structure
```
src/server/
  db.ts            # cached connection
  models/          # Mongoose schemas
  routes|api/      # handlers that call connectDB() then models
```

## Checklist
- [ ] `MONGODB_URI` server-side only; never bundled to the client (no `VITE_` prefix)
- [ ] Connection cached (no new pool per request / per hot reload)
- [ ] Models guarded with `models.X ?? model(...)` (avoids OverwriteModelError)
- [ ] Indexes on frequently queried fields
- [ ] Input validated before writes; errors handled
- [ ] Connectivity verified against Atlas/local before shipping

## Next
- Expose data via `/backend-boilerplate` routes; test with `/api-test-suite`.
