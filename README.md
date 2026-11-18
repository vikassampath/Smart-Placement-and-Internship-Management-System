# Campus2Career

Campus2Career is a student internship and placement portal. The primary application is a Node.js and Express single-page app with a SQL.js database. A Java Servlet prototype is also included under `java-version/`.

## Features

- Browse, search, and filter internship listings
- Student registration, login, profiles, and application tracking
- Internship recommendations based on student CGPA
- Admin tools for internships, applications, and student accounts
- Persistent SQLite-compatible storage using SQL.js
- Responsive browser interface

## Run the Node.js application

Requirements: Node.js 18 or newer and npm. The server uses Express 5.

```sh
npm ci
npm start
```

Open [http://localhost:3000](http://localhost:3000). The app creates its database and sample records on first launch. Records are saved to `data/campus2career.sqlite` and kept across restarts. Set `DB_PATH` to choose a different database file and `PORT` to change the port.

The included demo accounts are for local development only:

| Role | Email | Password |
| --- | --- | --- |
| Admin | `admin@atme.com` | `admin123` |
| Student | `vikas@student.com` | `student123` |

The login endpoint allows up to 10 failed attempts per IP in 15 minutes. Successful logins do not count toward this limit. The server also sends security headers and uses a content security policy that permits the app's current CDN assets.

For production, set `NODE_ENV=production` and provide a strong, private `SESSION_SECRET`. The default Express session store is intended for local development; configure a persistent production session store and a database suitable for your deployment, and replace the demo accounts. When running behind a trusted reverse proxy, set `TRUST_PROXY_HOPS` to the number of trusted proxy hops so secure cookies work correctly.

Run the JavaScript syntax check with:

```sh
npm run check
```

## Java prototype

`java-version/` contains a small Jakarta Servlet/Maven prototype. It requires Java 17 or newer and can be packaged with:

```sh
cd java-version
mvn package
```

The WAR is written to `target/internhub.war`. The Java prototype is separate from the main Node.js app and requires a compatible servlet container and MySQL configuration to run.

Configure its connection with `INTERNHUB_DB_URL`, `INTERNHUB_DB_USER`, and `INTERNHUB_DB_PASSWORD`. Local defaults target MySQL on `localhost` with the `root` account; use a dedicated MySQL account and a private password outside local development.

## Repository layout

```text
server.js                 Express API and SQL.js initialization
public/                   Browser app, styles, and images
java-version/             Jakarta Servlet prototype and SQL schema
```
