# Keystroq Backend

Backend for Keystroq, a real-time 1v1 typing battle app. It handles live matches over Socket.io, keeps in-progress match state in Redis, and saves final results and leaderboard data to PostgreSQL.

Frontend repo: https://github.com/randeep88/keystroq

## Features

- Real-time 1v1 matches over Socket.io
- Live WPM, accuracy and progress synced between both players
- Match state kept in Redis, so frequent updates never hit the database
- Only final results are written to PostgreSQL through Prisma
- Clerk token verification for authenticated users
- Global leaderboard API

## Architecture

1. Players join a match room through Socket.io.
2. While the match runs, each progress update (WPM, accuracy, typed characters) is stored in Redis and broadcast to the opponent.
3. When the match ends, the final result is calculated and saved once to PostgreSQL with Prisma.
4. The leaderboard is served from the saved results.

## Tech Stack

| Area | Tools |
|---|---|
| Runtime | Node.js, TypeScript |
| Server | Express.js, Socket.io |
| Database | PostgreSQL, Prisma ORM |
| Cache / live state | Redis |
| Auth | Clerk |

## Getting Started

```
git clone https://github.com/randeep88/keystroq-backend.git
cd keystroq-backend
npm install
```

Create a `.env` file in the root:

```
DATABASE_URL=
REDIS_URL=
IMAGEKIT_PUBLIC_KEY=
IMAGEKIT_PRIVATE_KEY=
IMAGEKIT_URL_ENDPOINT=
CLERK_PUBLISHABLE_KEY=
CLERK_SECRET_KEY=
```

Set up the database:

```
npx prisma generate
npx prisma migrate dev
```

Start the server:

```
npm run dev
```

## Author

Randeep Singh: [GitHub](https://github.com/randeep88) | [LinkedIn](https://linkedin.com/in/randeep-singh88)
