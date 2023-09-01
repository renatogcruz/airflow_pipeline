# Airflow pipeline

#### Environment
Dentro de "airflow" (pasta criada para instalação do pacote), criaremos o ambiente virtual no qual instalaremos o Airflow:

`python3.10 -m venv venv`

Ativnado o ambiente virtual:

`source venv/bin/activate`

#### Install Airflow

Instalando o Airflow. 

Utilizaremos o pacote pip para instalá-lo e passaremos a versão desejada, 2.3.2. Em seguida, passaremos o arquivo de restrição, que especifica todas as versões das bibliotecas que o Airflow precisa para funcionar corretamente, então adicionaremos --constraint e a url que direciona para este arquivo.

```
AIRFLOW_VERSION=2.3.2
PYTHON_VERSION="$(python --version | cut -d " " -f 2 | cut -d "." -f 1-2)"
CONSTRAINT_URL="https://raw.githubusercontent.com/apache/airflow/constraints-${AIRFLOW_VERSION}/constraints-${PYTHON_VERSION}.txt"
pip install "apache-airflow[async,postgres,google]==${AIRFLOW_VERSION}" --constraint "${CONSTRAINT_URL}"
```

Iniciando localmente:

```
export AIRFLOW_HOME=~/Documents/airflow
airflow standalone
```

Pode-se observar, no log de execução, que há um trecho indicando que o Airflow está pronto ("Airflow is ready") seguido de um usuário ("admin") e uma senha, que consta em "password". 

A senha também pode ser encontrada na pasta de execução do Airflow, no arquivo chamado "standalone_admin_password.txt".

No navegador, acessaremos `localhost:8080`, e logaremos com o usuário e senha que nos foram fornecidos para acessar a interface do Airflow.

