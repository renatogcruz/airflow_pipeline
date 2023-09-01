# Airflow pipeline

Para atualizar os pacotes do Ubuntu
```
sudo apt update
sudo apt upgrade
```

Instalação do Python 3.9 e do pacote venv
```
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt install python3.9
sudo apt install python3.9-venv
```

Criação e ativação do ambiente virtual no diretório Documents/airflow
```
cd Documents
mkdir airflowalura
python3.9 -m venv venv
source venv/bin/activate
```

Para a instalação e execução do Airflow 2.3.2, foram utilizados os comandos:

Instalação do Airflow
```
pip install 'apache-airflow==2.3.2' \
 --constraint "https://raw.githubusercontent.com/apache/airflow/constraints-2.3.2/constraints-3.9.txt"
```

ou

```
AIRFLOW_VERSION=2.3.2
PYTHON_VERSION="$(python --version | cut -d " " -f 2 | cut -d "." -f 1-2)"
CONSTRAINT_URL="https://raw.githubusercontent.com/apache/airflow/constraints-${AIRFLOW_VERSION}/constraints-${PYTHON_VERSION}.txt"
pip install "apache-airflow[async,postgres,google]==${AIRFLOW_VERSION}" --constraint "${CONSTRAINT_URL}"
```

Importação da variável de ambiente

```
export AIRFLOW_HOME=~/Documents/airflow
```

Execução do Airflow
```
airflow standalone
```


Pode-se observar, no log de execução, que há um trecho indicando que o Airflow está pronto ("Airflow is ready") seguido de um usuário ("admin") e uma senha, que consta em "password". 

A senha também pode ser encontrada na pasta de execução do Airflow, no arquivo chamado "standalone_admin_password.txt".

No navegador, acessaremos `localhost:8080`, e logaremos com o usuário e senha que nos foram fornecidos para acessar a interface do Airflow.

Quando queremos executar o Airflow, nós temos a opção de executar cada um de seus componentes de forma separada, inicializando o banco de dados do Airflow, executando o scheduler e o webserver. Tudo de forma manual. No entanto, também temos a opção de utilizar o comando:

`airflow standalone`

Esse comando já faz tudo de forma mais automática, ou seja, inicia o banco de dados padrão do airflow, cria um novo usuário e inicia os serviços principais (o webserver e o scheduler).

Para finalizar a execução desses processos localmente, basta acessar o terminal onde o Airflow está sendo executado e pressionar Ctrl + C. É importante finalizar o processo antes de fechar o terminal para não termos problemas quando executarmos o Airflow novamente.

Para mais informações, você pode acessar a [documentação do Airflow](https://airflow.apache.org/docs/apache-airflow/2.3.2/start/local.html#running-airflow-locally).

Para mais informações sobre a interface do Airflow, acesse a [documentação](https://airflow.apache.org/docs/apache-airflow/2.3.2/ui.html).
