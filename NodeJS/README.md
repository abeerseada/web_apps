
# Node.js App — Quick Guide

## 1️⃣ `npm init` — Initialize a Project

**Purpose:**

* Creates **`package.json`** which is the Node.js project definition.
* Stores the project name, version, scripts, and dependencies.

**Usage:**

```bash
npm init      # step-by-step interactive setup
npm init -y   # quick setup with default values
```

**After running it, you get:**

* `package.json` → contains:

  * Project metadata (name, version)
  * Scripts (e.g., `"start": "node server.js"`)
  * Dependencies (added after `npm install`)

---

## 2️⃣ `npm install` — Install Dependencies

**Purpose:**

* Reads **`package.json`** and installs packages listed under `"dependencies"` and `"devDependencies"` into the `node_modules` folder.
* Creates or updates `package-lock.json` for exact version locking.

**Usage:**

```bash
npm install               # install all dependencies
npm install express       # add a new dependency
npm install --save-dev nodemon  # add dev-only dependency
```

**Notes:**

* For reproducible installs in **CI/CD**, use:

  ```bash
  npm ci            # cleans node_modules and installs from package-lock.json
  npm ci --omit=dev # production install without devDependencies
  ```
* **Never commit `node_modules/`**; only commit `package.json` and `package-lock.json`.

---

## 3️⃣ `npm start` — Run the App

**Purpose:**

* Runs the **`start` script** from `package.json`.
* If your `package.json` has:

  ```json
  "scripts": {
    "start": "node server.js"
  }
  ```

  Then `npm start` is equivalent to:

  ```bash
  node server.js
  ```

**Why use it?**

* Short and easy to remember.
* Flexible: you can change the command later (e.g., to `nodemon` in dev or `pm2` in prod) without changing your terminal habits.

---

## Example Workflow

### 1) Initialize Project

```bash
npm init -y
```

### 2) Install Express

```bash
npm install express
```

### 3) Create `app.js`

```js
const express = require('express');
const app = express();

app.get('/', (req, res) => res.send('Hello, Node.js!'));

const PORT = process.env.PORT || 8080;
app.listen(PORT, () => console.log(`app running on ${PORT}`));
```

### 4) Add Start Script to `package.json`

```json
"scripts": {
  "start": "node app.js"
}
```

### 5) Run the app

```bash
npm start
# open http://127.0.0.1:8080/
```

---

## Quick Tips

* **`npm init`** → Create `package.json` (project metadata + scripts)
* **`npm install`** → Install dependencies from `package.json` (into `node_modules`)
* **`npm start`** → Run your app using the `start` script

> For development with auto-reload:
>
> ```bash
> npm install --save-dev nodemon
> npx nodemon server.js
> ```

---
