# Aluna
* 222687: Mylena Roberta dos Santos

## Tarefa de Cypher sobre Marcadores e Taxonomia

## Tarefa 1

Escreva em Cypher uma consulta que retorne os marcadores da categoria `Serviços`, sem considerar as categorias subordinadas.

### Resolução
~~~cypher
MATCH (m:Marcador)-[:Pertence]->(c:Categoria)
WHERE c.id = "Serviços"
RETURN m, c
~~~

## Tarefa 2

Escreva em Cypher uma consulta que retorne os marcadores da categoria `Serviços`, considerando as categorias subordinadas.

### Resolução
~~~cypher
MATCH (m:Marcador)-[:Pertence]->(c:Categoria)
MATCH (cat1:Categoria)-[:Superior]->(sup1:Categoria)
MATCH (cat2:Categoria)-[:Superior]->(sup2:Categoria)
WHERE (c.id = cat2.id OR c.id = cat1.id OR c.id = sup1.id) AND sup1.id = "Serviços" AND (sup2.id = cat1.id OR sup2.id = sup1.id)
RETURN m, c, cat1, sup1, cat2, sup2
~~~