# **Pokemon Graph Database**

Este projeto utiliza dados da [PokeAPI](https://pokeapi.co/) para criar um banco de dados de grafos no **Neo4j**. Ele permite explorar e visualizar conexões entre os primeiros 151 Pokémon, como tipos, habilidades e evoluções.

---

## **Recursos**

1. **Pipeline ETL**:
   - Extração de dados da PokeAPI.
   - Transformação dos dados para criar nós e relacionamentos.
   - Carregamento no banco de grafos Neo4j.
   
2. **Banco de Grafos**:
   - **Nós**: Pokémon, Tipos, Habilidades.
   - **Arestas**:
     - `PERTENCE_A`: Liga Pokémon aos seus tipos.
     - `TEM_HABILIDADE`: Liga Pokémon às suas habilidades.
     - `EVOLUI_PARA`: Liga Pokémon às suas evoluções.

3. **Consultas em Cypher**:
   - Explore Pokémon por tipo.
   - Visualize cadeias evolutivas.
   - Descubra habilidades específicas de Pokémon.

---

## **Requisitos**

1. **Dependências do Projeto**:
   - Python 3.8+
   - [Neo4j Community Edition](https://neo4j.com/download-center/)

2. **Instale as Dependências**:
   Certifique-se de instalar os pacotes listados no `requirements.txt`:
   
   ```bash
     pip install -r requirements.txt
   ```
3. **Configuração do Neo4j**:
    Certifique-se de que o Neo4j esteja disponível em:
   - [Porta HTTP](http://localhost:7474)
   - [Porta BOLT](http://localhost:7687)
---
## **Como Executar**

1. **Clone o Repositório**:
    Repositório com a base do projeto:

```bash
   git clone https://github.com/maryucha/graph_pokemon.git

    # navegue até o repositório clonado
   cd graph_pokemon
```
1. **Inicie o Neo4j via compose**:
    Certifique-se de que o Neo4j esteja disponível em localhost:7474:
```bash
    docker compose up --build -d
```
2. **Prepare seu ambiente instalando as bibliotecas necessárias**:
    Prepare seu ambiente na sua ide utilizando o arquivo requiremnts.txt
```bash
    pip install -r requirements.txt
```
3. **Execute o Jupyter Notebook**:
    No Jupyter Notebook, execute o script principal para:

```bash
    jupyter notebook
```
Execute a pipeline para:

 >   - jupyter: Para desenvolvimento e análise.
 >   - pandas: Manipulação de dados.
 >   - requests: Requisições HTTP para a PokeAPI.
 >   - neo4j: Driver para conexão com o banco de grafos.
---
## **Consultas**

1. Pokémon por Tipo
```cypher
    MATCH (p:Poke)-[:PERTENCE_A]->(t:Type {name: "Fire"})
    RETURN p.name
```
2. Cadeia Evolutiva
```cypher
MATCH (p:Poke {name: "Bulbasaur"})-[:EVOLUI_PARA*]->(evo)
RETURN evo.name
```
3. Habilidades de um Pokémon
```cypher
MATCH (p:Poke {name: "Pikachu"})-[:TEM_HABILIDADE]->(a:Ability)
RETURN a.name
```
