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

Quando queremos executar o Airflow, nós temos a opção de executar cada um de seus componentes de forma separada, inicializando o banco de dados do Airflow, executando o scheduler e o webserver. Tudo de forma manual. No entanto, também temos a opção de utilizar o comando:

`airflow standalone`

Esse comando já faz tudo de forma mais automática, ou seja, inicia o banco de dados padrão do airflow, cria um novo usuário e inicia os serviços principais (o webserver e o scheduler).

Para finalizar a execução desses processos localmente, basta acessar o terminal onde o Airflow está sendo executado e pressionar Ctrl + C. É importante finalizar o processo antes de fechar o terminal para não termos problemas quando executarmos o Airflow novamente.

Para mais informações, você pode acessar a [documentação do Airflow](https://airflow.apache.org/docs/apache-airflow/2.3.2/start/local.html#running-airflow-locally).
