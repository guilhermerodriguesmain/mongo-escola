# Prova MongoDB - Escola

## Descrição

Este projeto foi desenvolvido como parte de uma atividade prática utilizando Docker e MongoDB, com execução via mongosh.

O objetivo foi criar um banco de dados escolar, inserir dados e realizar operações de consulta, atualização, remoção e agregação.

---

## Tecnologias

* Docker
* MongoDB
* mongosh

---

## Estrutura do Banco

* Banco: `escola`
* Collection: `alunos`

---

## Execução do Projeto

### Subir o container

```bash id="1k2m9f"
docker-compose up -d
```

### Verificar container

```bash id="m8d2qa"
docker ps
```

### Acessar o MongoDB

```bash id="x9r4pl"
docker exec -it mongodb-escola mongosh
```

---

## Comandos Utilizados

### Criar / acessar banco

```bash id="0qk7dz"
use escola
```

### Verificar bancos (opcional)

```bash id="6p2n3s"
show dbs
```

### Criar collection

```bash id="l4x8cf"
db.createCollection("alunos")
```

### Verificar collections (opcional)

```bash id="8k9w0t"
show collections
```

---

## Inserção de Dados

```bash id="r3d7hn"
db.alunos.insertMany([
  {
    nome: "João Silva",
    idade: 20,
    curso: "ADS",
    notas: [7, 8, 9],
    endereco: { cidade: "Maricá", estado: "RJ" }
  },
  {
    nome: "Maria Souza",
    idade: 22,
    curso: "SI",
    notas: [6, 7, 8],
    endereco: { cidade: "Niterói", estado: "RJ" }
  },
  {
    nome: "Carlos Lima",
    idade: 23,
    curso: "ADS",
    notas: [5, 6, 7],
    endereco: { cidade: "São Gonçalo", estado: "RJ" }
  },
  {
    nome: "Ana Costa",
    idade: 21,
    curso: "CC",
    notas: [9, 9, 10],
    endereco: { cidade: "Rio de Janeiro", estado: "RJ" }
  },
  {
    nome: "Pedro Rocha",
    idade: 24,
    curso: "ADS",
    notas: [8, 7, 6],
    endereco: { cidade: "Maricá", estado: "RJ" }
  }
])
```

---

## Consultas

### Buscar todos os alunos

```bash id="6fwjcz"
db.alunos.find()
```

### Buscar alunos do curso ADS

```bash id="u2w5nq"
db.alunos.find({ curso: "ADS" })
```

### Buscar alunos com idade maior que 21

```bash id="c1v8rx"
db.alunos.find({ idade: { $gt: 21 } })
```

---

## Atualizações

### Atualizar idade de um aluno

```bash id="p4z9yt"
db.alunos.updateOne(
  { nome: "João Silva" },
  { $set: { idade: 21 } }
)
```

### Adicionar nova nota

```bash id="h7n3qs"
db.alunos.updateOne(
  { nome: "Maria Souza" },
  { $push: { notas: 10 } }
)
```

---

## Remoção

```bash id="k2d8jf"
db.alunos.deleteOne({ nome: "Carlos Lima" })
```

---

## Aggregation Pipeline

### Média de notas por aluno

```bash id="v5m1qz"
db.alunos.aggregate([
  {
    $project: {
      nome: 1,
      media: { $avg: "$notas" }
    }
  }
])
```

### Quantidade de alunos por curso

```bash id="z8x4bn"
db.alunos.aggregate([
  {
    $group: {
      _id: "$curso",
      quantidade: { $sum: 1 }
    }
  }
])
```

---

## Evidências

Os prints da execução estão disponíveis na pasta:

```
prints/
```

Incluem:

* Execução do container
* Acesso ao mongosh
* Criação do banco e collection
* Inserção de dados
* Consultas
* Atualizações
* Remoção
* Aggregation

---

## Autor

Guilherme Rodrigues

---

## Status

Projeto concluído.
