## **Relatório de Testes – Cat Fact API**

### **Resumo Geral**

* **Data de execução:** 21/04/2025

* **Total de testes executados:** 126

* **Testes aprovados:**  114

* **Testes reprovados:**  12

* **Tempo total de execução:**  5.673 ms

---

### ** Cenários com Sucesso Total (Exemplos)**

| Caso de Teste | Descrição | Resultado |
| ----- | ----- | ----- |
| `Get Random Fact_CT01` | Obter um fato aleatório sobre gatos | Passou |
| `Get Random Fact_CT04` | Usar `max_length=100` | Passou |
| `Get a list of facts_CT03` | Usar `max_length=150` | Passou |
| `Get a list of breeds_CT02` | Listar raças com `limit=5` | Passou |

Todos os testes destes cenários passaram conforme esperado, com respostas válidas, JSON bem estruturado, cabeçalhos corretos e dados coerentes.

---

### **Falhas Identificadas**

| Caso de Teste | Descrição | Falhas |
| ----- | ----- | ----- |
| `Get Random Fact_CT05` | `max_length` como string (`DBR`) | Esperado status 400, retornou 200 |
| `Get a list of facts_CT04` | `max_length` como string | Lista não estava vazia |
| `Get a list of facts_CT06` | `limit=0` | Lista não estava vazia, limite não respeitado |
| `Get a list of facts_CT07` | `limit` negativo | Lista não estava vazia, limite não respeitado |
| `Get a list of facts_CT08` | `limit` como string | Lista não estava vazia, limite não respeitado |
| `Get a list of facts_CT09` | `max_length` vazio | Lista não estava vazia |
| `Get a list of facts_CT10` | `limit` vazio | Lista não estava vazia, limite não respeitado |

**Observação:** Em vários casos onde parâmetros inválidos foram fornecidos (`string`, `negativos` ou `vazios`), a API retorna status `200 OK`, quando o comportamento mais apropriado seria um erro como `400 Bad Request`.

---

### **Recomendações**

1. **Validação de parâmetros:**

   * Rejeitar entradas inválidas com mensagens claras e status HTTP adequado (`400 Bad Request`).

   * Ex: `max_length=DBR` ou `limit=-1`.

2. **Padrão de resposta:**

   * Garantir que listas estejam vazias quando valores como `limit=0` ou `max_length=0` são enviados.

   * Documentar o comportamento padrão quando os parâmetros são omitidos ou deixados em branco.

3. **Testes adicionais sugeridos:**

   * Testar limites extremos (`limit=999`, `max_length=1000`).

   * Testar campos adicionais no payload, caso sejam implementados.

---

### **Conclusão**

Apesar das falhas em alguns casos de entrada inválida, a API **Cat Fact** demonstrou boa estabilidade e consistência nas respostas padrão. Com algumas melhorias na validação de parâmetros, a robustez pode ser significativamente aprimorada.

