# Setup

Install `yum` packages

```
sudo yum update -y &&
sudo yum install gcc gcc-c++ libffi-devel python-devel python-pip python-wheel openssl-devel cyrus-sasl-devel openldap-devel -y
```

---

Use `pip` to install the Python Virtual Environment

```
pip install virtualenv
```

---

Create and activate the virtual environment

```
python3 -m venv venv &&
. venv/bin/activate
```

---

Install apache-superset

```
pip install apache-superset
```

---

Create and set the FLASK_APP environment variable

```
export FLASK_APP=superset &&
source venv/bin/activate
```

---

Generate a random secret key and store that in superset_config.py script

```
GENERATED_KEY=$(openssl rand -base64 42) &&
echo "SECRET_KEY = '${GENERATED_KEY}'" >> superset_config.py
```

---

Create and export the SUPERSET_CONFIG_PATH environment variable with the full-path to your superset_config.py script

```
export SUPERSET_CONFIG_PATH=/home/<user>/superset_config.py
```

---

Initialize the database

```
flask --app superset db upgrade
```

---

Create admin user

```
superset fab create-admin
```

---

Load sample data

```
superset load_examples
```

---

Create default roles and permissions

```
superset init
```

---

Start development web server on port 8088 (connect to the user interface with hostname:8088)

```
superset run -h 0.0.0.0 -p 8088 --with-threads --reload --debugger
```
