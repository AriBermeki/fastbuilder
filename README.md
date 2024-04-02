# fastbuilder
Build Web Applications with poure Python




## Usage
'''python

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


'''
