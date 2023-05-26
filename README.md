# MongoDB-Guide
Guia de comandos do Mongo (Command's Guide MongoDB)

## 🔖 Tipos de Consulta

filter - { "campo" : "valor"} (filtra por campo)
 
project - {"campo" : 1, "campo" : 0} (É retornado apenas os campos com valor 1, campo com valor 0 é desconsiderado da consulta)
  
sort - {"campo" : 1, "campo" : -1} (ordem crescente/decrescente)
  
max time ms - limita o tempo máximo que uma consulta leva pra ser executada
  
limit - limita a quantidade de registros retornados
  
skip - pula uma certa quantidade de documentos ( valor 25 - pula os 25 primeiros registros)
  
collation - usado para especificar regras específicas do idioma para comparação de textos, letras maiúscula e minúscula e outras.


## 📦 Comandos (Insert, Update, Delete, Replace)

- mostra todos as bases de dados
```
show databases
```
- criação do base de dados
```
show databases
```
- cria uma collection
```
db.createCollection(“nomecollection”)
```
- remove a collection dentro da base de dados
```
db.<collection>.drop()
```
- remove a base de dados
```
db.dropDatabase()
```
- atualiza apenas um documento
```
db.createCollection(“nomecollection”)
```
- atualiza vários documentos
```
db.<collection>.updateMany({<filter>}, {$set: {<update>}})
```
- replicar documento
```
db.collection.replaceOne(<filter>, <replacement>)
```
- remover apenas um documento
```
db.series.deleteOne({<filter>})
```
- remover vários documentos
```
db.series.deleteMany({<filter>})
```
- remove todos os documentos
```
db.series.deleteMany({})
```


## ✅ Operadores de Comparação

$eq - Valores que são iguais a um valor especificado.

\n$gt - Valores que são maiores a um valor especificado.

$gte - Valores maiores ou iguais a um valor especificado.

$in - Qualquer valor correspondente em uma matriz.

$lt - Valores menores a um valor especificado.

$lte - Valores menores ou iguais ao especificado.

$and - operador AND.

$or - operador OR.

$nor - operador NOT.

$ne - operador diferente (!=).

$all - todos que tem ... (tal coisa).


## 👷 Exemplos

- Exemplos de consultas:
```
(COMPASS)
{ $nor: [{"Ano de lançamento" : 2018}, {"Classificação" : "18+"}] }
{"Temporadas disponíveis" : { $lte: 5}}
{"Série" : 1, "Linguagem" : 1, _id: 0}
{ "Série" : 1}

(SCRIPT)
db.<collection>.find()
db.<collection>.find({"Ano de lançamento" : 2018})
db.<collection>.find({}, {"Série" : 1, "Linguagem" : 1, _id: 0}) - chaves vazias referencia um filtro vazio, após a vígula é referenciado o project
db.<collection>.find({"Ano de lançamento" : {$in : [2018, 2020]})
db.<collection>.find().limit(5)
db.series.find().sort({"Série":1})
db.series.find({"Temporadas disponíveis": {$gte: 4}})
db.series.find({"Ano de lançamento": {$ne: 2020}})
db.series.find({"Genero": {$all:["Ação", "Comédia"]}})
db.series.updateOne({"Série": "Grimm"},{$set: {"Temporadas disponíveis": 6}})
db.series.updateMany({"Série":{$in:["Four More Shots Please", "Fleabag"]}},{$set: {"Classificação": "18+"}})
db.series.deleteOne({"Série": "The Boys"})
db.series.deleteMany({"Temporadas disponíveis": 1})
```
