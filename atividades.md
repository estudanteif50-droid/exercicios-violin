# Atividades: SQL vs MongoDB e API no React

## 1. Descobrindo o banco

Abra a URL da API no navegador, aperte F12 e vá na aba **Network**. Clique na requisição e veja a aba **Response**.

- Se o item tiver `"_id": "64f1a2b3c4d5e6f7a8b9c0d1"` (24 caracteres), provavelmente é **MongoDB**.
- Se o item tiver `"id": 1` (número), provavelmente é **SQL**.

**Preencha com o que apareceu na sua API:** o identificador é `____` e isso indica `____`.

**Por quê:** o MongoDB cria o `_id` sozinho em cada documento. No SQL, o mais comum é uma coluna `id` numérica. Mas isso não é 100% certo, porque o backend pode mudar os nomes.

## 2. O documento do café

```json
{
  "_id": "abc123",
  "produto": "Café",
  "preco": 12.5,
  "tags": ["quente", "manhã"],
  "fornecedor": { "nome": "CoopeCafé", "cidade": "Dourados" }
}
```

- **(a) O `_id`:** `"abc123"`. É o código único do documento.
- **(b) Subdocumento:** `fornecedor`, um objeto dentro do documento, com `nome` e `cidade`.
- **(c) Array:** `tags`, uma lista com `"quente"` e `"manhã"`.

## 3. Conceitos

- **Coleção:** grupo de documentos no MongoDB, parecido com uma tabela do SQL. Exemplo: a coleção `produtos` guarda todos os produtos.
- **Schemaless:** o banco não obriga uma estrutura fixa. Um documento pode ter `tags` e outro não, sem precisar alterar nada antes. Quem costuma definir a estrutura é a aplicação (por exemplo, com Mongoose).

## 4. Vantagens

**SQL:**
1. Relacionamentos fortes entre tabelas (chaves estrangeiras e `JOIN`).
2. Transações seguras (ACID), boas para dinheiro e estoque.
3. Linguagem padronizada e boa para relatórios.

**MongoDB:**
1. Estrutura flexível, fácil de mudar.
2. Usa JSON, que combina com JavaScript, Express e React.
3. Guarda dados aninhados no mesmo documento e escala bem.

## 5. URL da API

Formato: `http://localhost:PORTA/CAMINHO`

Exemplo (troque pelos valores da turma): **`http://localhost:3000/produtos`**

Para testar, cole a URL no navegador. O JSON da lista deve aparecer.

## 6. Componente que consome a API

Veja o arquivo `ListaProdutos.jsx`. Ele mostra os três estados (carregando, erro e vazio) e usa `key={item._id ?? item.id}`.

O `??` usa o `_id` se existir; se não, usa o `id`. Assim funciona com MongoDB e com SQL.

## 7. Detetive de API

Se o JSON tem `_id` de 24 caracteres e os itens têm campos diferentes, o backend provavelmente usa MongoDB, por dois motivos:

1. **`_id` de 24 caracteres:** é o formato ObjectId, criado automaticamente pelo MongoDB. No SQL, o normal é `id` numérico ou UUID (36 caracteres com hífens).
2. **Campos diferentes entre os itens:** mostra estrutura flexível (schemaless), típica do MongoDB. Numa tabela SQL, todas as linhas têm as mesmas colunas.

## Critério de sucesso

- [ ] Abri a API no navegador e vi o JSON.
- [ ] Vi se o retorno tem `_id` ou `id`.
- [ ] O componente mostra os dados com os estados de carregando, erro e vazio.