# ✅ Option 1: Create a WordPress Plugin (PHP) + Use Python via API (Best way)

### How it works:

- Plugin = PHP (WordPress side)
- Python = separate service (Flask/FastAPI)
- Plugin calls Python using HTTP requests

📌 Example use cases:

- AI tools
- data scraping
- machine learning predictions
- automation

---

# ✅ Option 2: Run Python Script from WordPress Plugin (Not recommended)

You can run python using:

- `shell_exec()`
- `exec()`

⚠️ Most hosting providers block this for security.

---

# ✅ Recommended Architecture

### Step 1: Create plugin folder

Inside:

`wp-content/plugins/my-python-plugin/`

Create file:

`my-python-plugin.php`

---

# ✅ Basic WordPress Plugin Code (PHP)

```php
<?php
/*
Plugin Name: My Python Plugin
Description: Calls a Python API
Version: 1.0
Author: You
*/add_action('admin_menu', function () {add_menu_page("Python Tool","Python Tool","manage_options","python-tool","python_tool_page");
});functionpython_tool_page() {echo"<h1>Python API Result</h1>";$response =wp_remote_get("http://127.0.0.1:8000/predict");if (is_wp_error($response)) {echo"Error connecting to Python API";return;
    }$body =wp_remote_retrieve_body($response);echo"<pre>$body</pre>";
}
```

---

# ✅ Step 2: Create Python API (FastAPI Example)

```python
from fastapiimport FastAPI

app = FastAPI()@app.get("/predict")defpredict():return {"message":"Hello from Python!","result":42}
```

Run it:

```bash
uvicorn main:app --host 0.0.0.0 --port 8000
```

---

# ✅ Step 3: Access in WordPress Admin

Now in WP Dashboard you’ll see:

📌 **Python Tool menu**

It will display Python API response.
