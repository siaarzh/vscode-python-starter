# Using pipenv on VS Code on Windows 10

1. Install desired python version (e.g. Python 3.7)
2. Install pipenv:
    ```powershell
    > python37 -m pip install pipenv
    OR
    > py -3 -m pip install pipenv
    ```
3. Check which pipenv is default, just in case:
    ```powershell
    > Get-Command pipenv
    CommandType     Name               Version    Source
    -----------     ----               -------    ------
    Application     pipenv.exe         0.0.0.0    C:\Python\3.7.2\Scripts\pipenv.exe
    ```
4. Create virtual environment:
    ```powershell
    > pipenv --three
    ```
5. Now find the path the Python executable with the following command:
    ```powershell
    > pipenv --py
    C:\Users\Serzhan\.virtualenvs\test_vs_code_python-KdIZ1Tg8\Scripts\python.exe
    ```
6. Insert this value in your `./.vscode/settings.json` `python.pythonPath` variable:

7. OPTIONAL: Install pylint or flake8 and black:
    ```powershell
    > pipenv install --skip-lock --dev flake8 black
    ```
8. OPTIONAL: If you have [Code Runner](https://marketplace.visualstudio.com/items?itemName=formulahendry.code-runner) installed, add the path too. Then you might as
well set linting options too. Django code style uses 119 as line-length:
    ```json
    {
        "python.pythonPath": "C:\\Users\\Serzhan\\.virtualenvs\\test_vs_code_python-KdIZ1Tg8\\Scripts\\python.exe",
        "code-runner.executorMap": {
            "python": "C:\\Users\\Serzhan\\.virtualenvs\\test_vs_code_python-KdIZ1Tg8\\Scripts\\python.exe"
        },
        "python.linting.enabled": true,
        "python.formatting.provider": "black",
        "python.formatting.blackArgs": ["--line-length", "119"],
        "python.linting.flake8Enabled": true
    }
    ``` 