### O que não é o Airflow?
O Airflow não é um framework para realizar processamento de dados. Não use o Airflow como se estivesse usando o Spark. Para isso, chame um job do Spark no Airflow.

### O que é o Airflow?
O Apache Airflow é uma plataforma de código aberto para criar, agendar e monitorar seus workflows de forma programática. É um orquestrador, onde é possível criar pipelines dinâmicos e executar suas tarefas na ordem correta, de forma correta e no seu devido tempo.

### Benefícios do Apache Airflow

#### 1 - Dinâmico
#### 2 - Escalável
#### 3 - Interativo
#### 4 - Extensível

### Core Components
### 1 - Web Server
### 2 - Scheduler
### 3 - Metadata Database

2 componentes adicionais: Executor e Worker.

### Executor
Define como as tasks são executadas.

### Worker
É um processo ou subprocesso onde as suas tasks são executadas.

### Arquitetura
Dados os componentes, é possível criar diversos tipos de arquiteturas usando o Airflow.

#### Single Node

Neste caso, todos os recursos ficam disponíveis em uma unica máquina.
Não escala.
O Web Server é responsável por retornar os dados do banco de dados
O Scheduler se comunica com a base para verificar os horários de execução e realiza as chamadas para o Executor
O Executor faz o processamento (insere na fila - que faz parte do Executor, nesta arquitetura) e retorna as informações para o Banco.

![image](https://user-images.githubusercontent.com/77291949/210261685-f4f54695-cc6b-4ef3-8c37-71d85ab52639.png)

#### Multi Node cluster

Neste modelo os recursos ficam disponíveis em "nós" e é possível escalar conforme a necessidade.
O WebServer é responsável por retornar os dados do banco de dados
O Scheduler se comunica com a base para verificar os horários de execução e realiza as chamadas para o Executor
O Executor coloca as informações na fila (desta vez, à parte do Executor) e os workers buscam os dados da fila para processar.
Com isso, caso seja necessário aumentar o paralelismo, basta adicionar novos workers no cluster.

![image](https://user-images.githubusercontent.com/77291949/210606267-0b03d7d9-84fc-4b61-a400-9d771b745469.png)

### Conceitos

#### DAGs: 
É o conjunto de tarefas, possuindo um começo e um fim, sem passar novamente pelas etapas anteriores (Direct Acyclic Graph)

#### Operadores: 
É uma das tarefas dentro da DAG.

##### 1 - Action Operator:
Responsável por executar algo dentro da DAG, por exemplo o PythonOperator, que executará um script em python desenvolvido, ou o BashOperator, que executará um comando bash.

#####  2 - Transfer Operator:
Permite transportar dados entre origens e destinos.

##### 3 - Sensor Operator:
Fica monitorando um status ocorrer antes de mover para a próxima task.

#### Task:
Quando o Operator está vinculado à uma DAG (uma instância de um Operator). Task é uma instância do Operator.

#### Task Instance:
É a execução de uma Task. Representa uma execução específica da task: DAG + TASK + Data e Horário.

#### Dependências:
Determina os relacionamentos entre as Tasks.
Podem ser utilizadas as funções set_upstream ou set_downstream, mas não é uma boa prática recomendada.
O ideal é usar os sinais "<<" ou ">>" para determinar as dependências entre as tasks

#### Workflow:
Combinação de todos os tópicos citados acima.
![image](https://user-images.githubusercontent.com/77291949/210609798-1ea40f77-3507-4159-96c1-246e4283c0c7.png)

