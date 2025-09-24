# 1 ; 
```bash
apt update && apt install python3-flask -y
```

# 2 ; 

```bash
nano upload.py
```
- Paste This ( Yapıştır ) ; 

```bash
from flask import Flask, request, render_template_string
import os

app = Flask(__name__)

UPLOAD_FOLDER = "/root/uploads"
os.makedirs(UPLOAD_FOLDER, exist_ok=True)

html = """
<!doctype html>
<title>Upload File</title>
<h1>Upload new File</h1>
<form method=post enctype=multipart/form-data>
  <input type=file name=file>
  <input type=submit value=Upload>
</form>
"""

@app.route("/", methods=["GET", "POST"])
def upload_file():
    if request.method == "POST":
        f = request.files["file"]
        f.save(os.path.join(UPLOAD_FOLDER, f.filename))
        return "File uploaded successfully!"
    return render_template_string(html)

app.run(host="0.0.0.0", port=8080)
```
```bash
python3 upload.py
```
