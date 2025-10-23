# Python Package Creation Notes

Python Package Creation 
Legacy Method (Using setup.py)


Folder structure example:
my_package/
├── my_package/
│   ├── __init__.py
│   ├── module1.py
│   └── module2.py
├── tests/
│   └── test_module1.py
├── README.md
├── setup.py
└── requirements.txt


Key files:
1. __init__.py — marks package. 
2. setup.py — package metadata & install logic.
 3. requirements.txt — runtime deps. 
4. MANIFEST.in — include non-code files.
Step-by-step (Legacy):
- Create project folder and package subfolder (my_package/).
- Add __init__.py and your modules (module1.py, etc.).
- Create setup.py using setuptools (example below).
- Optionally add requirements.txt, README.md, LICENSE, MANIFEST.in.
- Build distributions: python setup.py sdist bdist_wheel
- Install locally for testing: pip install .
- Test import: python -c "import my_package; print(my_package.__version__)"
- Upload to PyPI (optional): pip install twine; twine upload dist/*
Example setup.py:
from setuptools import setup, find_packages

setup(
    name="my_package",
    version="0.1.0",
    packages=find_packages(),
    install_requires=["numpy"],
    author="name",
    author_email="email",
    description="Sample package (legacy)",
    license="MIT",
    url="https://github.com/yourusername/my_package",
)

Regular Method (Using pyproject.toml without Poetry)
Folder structure example:
my_package/
├── my_package/
│   ├── __init__.py
│   └── module1.py
├── tests/
│   └── test_module1.py
├── pyproject.toml
└──README.md


Example pyproject.toml (setuptools backend):
[build-system]
requires = ["setuptools>=61.0", "wheel"]
build-backend = "setuptools.build_meta"

project
name = "my_package"
version = "0.1.0"
description = "A sample package using pyproject.toml"
authors = [
  { name = "name", email = "email" }
]

readme = "README.md"
dependencies = ["numpy"]


Step-by-step (Regular):
- Create project folder and package subfolder (my_package/).
- Add __init__.py and your modules.
- Create pyproject.toml with [build-system] and [project] sections as shown.
- Install build tool: pip install build
- Build distributions: python -m build
- Install locally: pip install .
- Test import and functionality.
- Upload to PyPI (optional): pip install twine; twine upload dist/*
Advanced Method (Using Poetry)
Folder structure (created by poetry new):
my_package/
├── my_package/
│   └── __init__.py
├── tests/
│   └── __init__.py
├── pyproject.toml
└── README.rst

Step-by-step (Poetry):
- Install Poetry: pip install poetry (or use official installer).
- Create package: poetry new my_package (creates structure).
- Enter project: cd my_package
- Add runtime deps: poetry add numpy
- Add dev deps: poetry add --dev pytest
- Install deps and create virtualenv: poetry install
- Run commands inside project's venv: poetry run python -c "import my_package"
- Build: poetry build
- Publish: poetry publish --build
Example pyproject.toml (Poetry):
[tool.poetry]
name = "my_package"
version = "0.1.0"
description = "A sample Python package created using Poetry"
authors = ["Your Name <your email>"]

[tool.poetry.dependencies]
python = "^3.10"
numpy = "^1.26"

[build-system]
requires = ["poetry-core"]
build-backend = "poetry.core.masonry.api"

Comparison Table
Summary & Tips
- Legacy: use when maintaining older projects.
- Regular: recommended if you want PEP-compliant packages without Poetry.
- Poetry: best when you want dependency resolution, lockfile, and simpler workflow.
Quick tips:
• Use a virtual environment