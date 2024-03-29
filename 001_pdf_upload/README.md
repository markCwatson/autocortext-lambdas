## Creating package for AWS lambda function

This is required ebcause `PyPDF2` is not supported in AWS Lambda runtime environment.

Create a new directory for Lambda project.

Note: this lambda function is configured with 256 MB memory and a 15 minute timeout.

```python
mkdir lambda_project && cd lambda_project
```

Create a virtual environment in the project directory

```python
python3 -m venv venv
```

Activate the virtual environment

```python
source venv/bin/activate
```

Install PyPDF2 and chardet

```python
pip install PyPDF2
pip install chardet
```

Deactivate the virtual environment

```python
deactivate
```

Prepare the deployment package (assuming pyhton 3.10 is being used)

```python
cd venv/lib/python3.10/site-packages/
zip -r9 ${OLDPWD}/my-deployment-package.zip .
```

Go back to previous location

```pythoncd 
cd -
```

Add the Lambda function code to the deployment package
Note: run this command whenever `lambda_function.py` changes inside the `/lambda_project` directory.

```python
zip -g my-deployment-package.zip lambda_function.py
```
