# Relatório – Classificador Production Ready

## 1. Objetivo

O objetivo deste projeto foi transformar um classificador simples baseado em LLM em uma versão mais robusta e preparada para um ambiente de produção.

A proposta incluiu implementar validações, tratamento de erros e testes controlados para garantir maior confiabilidade no sistema.

---

## 2. Melhorias Implementadas

Foram implementadas as seguintes melhorias:

### 2.1 Parser JSON

Foi criada uma função para realizar o parsing seguro da resposta retornada pelo modelo, garantindo que o formato esteja correto antes de qualquer processamento.

Função implementada:
- `parse_json()`

---

### 2.2 Tratamento de JSON inválido

Foi adicionado tratamento de exceção para capturar erros de `JSONDecodeError`, evitando que a aplicação quebre caso o modelo retorne um JSON malformado.

Foi criada uma exceção personalizada:
- `ValidationError`

---

### 2.3 Validação de Campo Obrigatório

O sistema verifica se o campo `"categoria"` está presente na resposta do modelo.

Função implementada:
- `validate_required_field()`

---

### 2.4 Validação Contra Lista Permitida

Foi implementada uma validação para garantir que o modelo não retorne categorias inventadas.

Categorias permitidas:
- Suporte
- Vendas
- Financeiro
- Geral

Função implementada:
- `validate_allowed_category()`

---

### 2.5 Fallback Seguro

Foi criado um mecanismo de fallback para garantir que o sistema continue funcionando mesmo em caso de erro.

Quando ocorre qualquer falha de validação, o sistema retorna:

```json
{
  "categoria": "Geral",
  "erro": true
}