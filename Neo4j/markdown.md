# 🧑‍🏫 Aula Prática com Neo4j — Comandos Cypher

Este roteiro é ideal para introdução prática ao uso do **Neo4j** e sua linguagem de consulta **Cypher**.

---

## 📌 1. Criar Nós

```cypher
CREATE (:Person {name: 'Ana', age: 25});
CREATE (:Person {name: 'Bruno', age: 30});
CREATE (:Person {name: 'Carlos', age: 28});
CREATE (:Movie {title: 'Matrix', year: 1999});
CREATE (:Movie {title: 'Inception', year: 2010});
```

---

## 🔗 2. Criar Relacionamentos

```cypher
MATCH (a:Person {name: 'Ana'}), (b:Person {name: 'Bruno'})
CREATE (a)-[:FRIENDS_WITH]->(b);

MATCH (a:Person {name: 'Ana'}), (m:Movie {title: 'Matrix'})
CREATE (a)-[:WATCHED {rating: 5}]->(m);

MATCH (b:Person {name: 'Bruno'}), (m:Movie {title: 'Inception'})
CREATE (b)-[:WATCHED {rating: 4}]->(m);
```

---

## 🔍 3. Consultas Básicas

```cypher
MATCH (p:Person) RETURN p;

MATCH (p:Person)-[:WATCHED]->(m:Movie)
RETURN p.name, m.title;
```

---

## 🎯 4. Filtros com WHERE

```cypher
MATCH (p:Person)
WHERE p.age > 26
RETURN p.name, p.age;

MATCH (p:Person)-[r:WATCHED]->(m:Movie)
WHERE r.rating >= 5
RETURN p.name, m.title, r.rating;
```

---

## 🔄 5. Travessias Múltiplos Níveis

```cypher
// Amigos de amigos
MATCH (a:Person {name: 'Ana'})-[:FRIENDS_WITH]->()-[:FRIENDS_WITH]->(fof:Person)
WHERE a <> fof
RETURN DISTINCT fof.name;
```

---

## 🧠 6. Funções úteis

```cypher
MATCH (p:Person)
RETURN p.name, toUpper(p.name) AS name_upper, size(p.name) AS name_length;

MATCH (p:Person)-[r:WATCHED]->(m:Movie)
RETURN m.title, avg(r.rating) AS avg_rating
ORDER BY avg_rating DESC;
```

---

## 🧭 7. Encontrar o Caminho mais Curto

```cypher
MATCH p=shortestPath((a:Person {name: 'Ana'})-[*]-(c:Person {name: 'Carlos'}))
RETURN p;
```

---

## 🛠 8. Atualização de Dados

```cypher
MATCH (p:Person {name: 'Carlos'})
SET p.city = 'São Paulo'
RETURN p;
```

---

## 🧹 9. Remover Dados

```cypher
// Remove um relacionamento
MATCH (:Person {name: 'Ana'})-[r:FRIENDS_WITH]->(:Person {name: 'Bruno'})
DELETE r;

// Remove um nó e seus relacionamentos
MATCH (m:Movie {title: 'Matrix'})
DETACH DELETE m;
```

---

## ✅ 10. Verificar o Grafo Visualmente

```cypher
MATCH (n) RETURN n;
```

---

## 💡 Exercício Final

Crie:

- Duas novas pessoas
- Relacionamentos de amizade e visualização de filmes
- Uma consulta para listar os filmes assistidos por amigos de uma pessoa

```cypher
// Exemplo de desafio
MATCH (p:Person {name: 'Carlos'})-[:FRIENDS_WITH]->(friend)-[:WATCHED]->(movie)
RETURN DISTINCT movie.title;
```