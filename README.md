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
    C:\Users\Serzhan\.virtualenvs\vscode-python-starter-KdIZ1Tg8\Scripts\python.exe
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
        "python.pythonPath": "C:\\Users\\Serzhan\\.virtualenvs\\vscode-python-starter-KdIZ1Tg8\\Scripts\\python.exe",
        "code-runner.executorMap": {
            "python": "C:\\Users\\Serzhan\\.virtualenvs\\vscode-python-starter-KdIZ1Tg8\\Scripts\\python.exe"
        },
        "python.linting.enabled": true,
        "python.formatting.provider": "black",
        "python.formatting.blackArgs": ["--line-length", "119"],
        "python.linting.flake8Enabled": true,
        "python.linting.pylintEnabled": false
    }
    ``` 

## Troubleshooting:

### Error messages while attempting to install black
You might run in to the following error messages when trying to install black via pipenv:
```powershell
> pipenv install --dev black
...
[pipenv.exceptions.ResolutionFailure]: Warning: Your dependencies could not be resolved. You likely have a mismatch in your sub-dependencies.
  First try clearing your dependency cache with $ pipenv lock --clear, then try the original command again. 
  Alternatively, you can use $ pipenv install --skip-lock to bypass this mechanism, then run $ pipenv graph to inspect the situation.raph to inspect the situation.  
  Hint: try $ pipenv lock --pre if it is a pre-release dependency.
ERROR: ERROR: Could not find a version that matches black
Skipped pre-versions: 18.3a0, 18.3a0, 18.3a1, 18.3a1, 18.3a2, 18.3a2, 18.3a3, 18.3a3, 18.3a4, 18.3a4, 18.4a0, 18.4a0, 18.4a1, 18.4a118.4a0, 18.4a0, 18.4a1, 18.4a1, 18.4a2, 18.4a2, 18.4a3, 18.4a3, 18.4a4, 18.4a4, 18.5b0, 18.5b0, 18.5b1b1, 18.6b1, 18.6b2, 18.6b2, 18, 18.5b1, 18.6b0, 18.6b0, 18.6b1, 18.6b1, 18.6b2, 18.6b2, 18.6b3, 18.6b3, 18.6b4, 18.6b4, 18.9b0, 18.9b0, 19.3b0, 19.3b0
There are incompatible versions in the resolved dependencies.
```
This likely because the pipenv simply does not allow installation of pre-releases (e.g. `19.3b0`). As the promt suggests, simply run the following command to allow pre-release installation:
```powershell
> pipenv lock --pre
```