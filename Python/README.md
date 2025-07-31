# Flask App — Quick Guide (Python)

## Prerequisites

* **Python 3.9+** (3.10+ recommended)
* **pip** installed

Check:

```bash
python --version
pip --version
```

> On some systems use `python3` and `pip3`.

---

## Project Files

* `app.py` (your Flask code)
* `requirements.txt` (recommended):

  ```
  Flask==3.0.0
  # For production:
  gunicorn==21.2.0
  ```

---

## Using a Virtual Environment (venv)

Use **venv** when:

* You need isolation between projects (different library versions).
* You want reproducible setups for teammates or CI.
* You don’t want to pollute system Python.

You might skip venv only for very quick experiments, but **best practice is to use it**.

**Create & activate venv**

**macOS/Linux:**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

**Windows (PowerShell):**

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

**Install dependencies inside venv**

```bash
pip install -U pip
pip install -r requirements.txt
```

**Deactivate**

```bash
deactivate
```

---

## Installing Dependencies via `requirements.txt` (and `--no-cache-dir`)

**Correct filename:** use **`requirements.txt`** (plural), not `requirement.txt`.

**Standard install:**

```bash
pip install -r requirements.txt
```

**Why/when to use `--no-cache-dir`:**

```bash
pip install --no-cache-dir -r requirements.txt
```

* Forces fresh downloads (ignores pip’s local cache).
* Useful in **Docker builds** (keeps images smaller, avoids stale wheels).
* Useful in **CI/CD** to ensure clean, repeatable installs.

**Example `requirements.txt` for this app:**

```
Flask==3.0.0
gunicorn==21.2.0
```

---

## Run in Development

### Direct run

```bash
python app.py
```

* App runs at: `http://127.0.0.1:3000/`


## Production (don’t use Flask’s dev server)

Use **Gunicorn** (or uWSGI) behind a reverse proxy (e.g., Nginx):

```bash
pip install gunicorn
gunicorn -w 2 -b 0.0.0.0:3000 app:app
```

---

## Quick Start (copy & paste)

**macOS/Linux:**

```bash
python3 -m venv .venv
source .venv/bin/activate
echo "Flask==3.0.0" > requirements.txt
pip install --no-cache-dir -r requirements.txt
python app.py
# open http://127.0.0.1:3000/
```

**Windows (PowerShell):**

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
echo Flask==3.0.0 > requirements.txt
pip install --no-cache-dir -r requirements.txt
python app.py
# open http://127.0.0.1:3000/
```


