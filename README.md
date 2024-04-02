# fastbuilder
Build Web Applications with poure Python


## 📦 Install

```bash
pip install fastbuilder

```
```plaintext


project_folder_struktur/
│
├── static/
│   ├── 
├── templates/
│   ├── 
├── .venv
├── main.py
├── build.py



```

## Usage

### main.py
```python
from pathlib import Path
import uvicorn
from fastapi import FastAPI, Request, Response
from fastapi.responses import HTMLResponse
from fastapi.staticfiles import StaticFiles
from fastapi.templating import Jinja2Templates


app = FastAPI()

project_path = Path(__file__).parent
templates = Jinja2Templates(project_path / "templates")

static_files = StaticFiles(
    directory=(project_path / "static").resolve(),
    follow_symlink=True,
)
app.mount("/static", static_files, name="static")

# important !!!!!!!!!!!!!!!!!!!!!!!!!!
@app.get("/", response_class=HTMLResponse)
async def read_item(request: Request):
    prefix = request.headers.get(
        "X-Forwarded-Prefix", request.scope.get("root_path", "")
    ) 
    return templates.TemplateResponse(
        "index.html", {"request": request, "prefix": prefix}
    )


@app.get("/favicon.ico", response_class=HTMLResponse)
async def favicon_ico(request: Request):
    return Response(content=b"", media_type="image/x-icon")


@app.get("/exit")
async def logging(request: Request):
    import os
    import signal

    os.kill(os.getpid(), signal.SIGINT)


if __name__ == "__main__":
    uvicorn.run(app=app)
```

### build.py
```python

from fastbuilder import Build

executable = Build(executable_name="server", app_path="main.py")


executable.add_data("static")
executable.add_data("templates")
executable.set_icon("logo.ico")


executable.run_build(
    static_folder="static",
    templates_folder="templates",
    frontend_folder="client",
    frontend_framework="React",
    backend_framework="fastapi",
)

```




### In April 2024, fastbuilder was just publicly released by software architecture Malek Ali at Yellow-SiC Group and is in alpha stage.
<p>Anyone can install and use PyNexumJS, There may be issues, but we are actively working to resolve them</p>
