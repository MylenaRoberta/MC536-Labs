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
MATCH (sub:Categoria)-[:Superior]->(sup:Categoria {id: "Serviços"})
MATCH (subsub:Categoria)-[:Superior]->(subsup:Categoria)
WHERE (subsup.id = sup.id OR subsup.id = sub.id) AND
      (c.id = sup.id OR c.id = sub.id OR c.id = subsub.id)
RETURN m, c, sup, sub, subsub
~~~