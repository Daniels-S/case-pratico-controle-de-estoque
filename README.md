# Controle de estoque

## Execução

Abra `controle_estoque.ipynb` com Python 3.xx e execute as células em ordem. O código usa a biblioteca padrão. A célula AWS está comentada. Os testes ficam na última célula.

## Solução

`Estoque` oferece entrada, saída, reserva, bloqueio, liberação e consulta. Cada produto guarda o total físico, as quantidades reservada e bloqueada vêm dos registros ativos. `disponivel = total - reservada - bloqueada`. Cada registro tem ID único, solicitação e quantidade. As validações ocorrem antes de qualquer alteração.

**Premissas:** A primeira entrada cadastra o produto. Quantidades são inteiros positivos. IDs são textos não vazios. IDs de registro não são reutilizados. 

**Limites:** O estado permanece em memória durante a execução. Não há persistência nem controle de concorrência. A configuração Athena está comentada e não executa consultas.

**Evolução operacional:** persistir movimentos e saldos, impedir reprocessamento entre execuções agendadas, controlar concorrência e tratar falhas de consulta ao Athena. O núcleo de regras pode ser copiado para um script Python shell do Glue Studio.

## Cinco aspectos de engenharia

1. **Saldos derivados:** evitam contadores divergentes.
2. **Validação prévia:** rejeições preservam o estado.
3. **IDs únicos:** identificam reservas e bloqueios para consulta e liberação.
4. **Testes automatizados:** cobrem operações e erros sem efeito colateral.
5. **Lógica isolada:** facilita trocar entrada e persistência sem alterar as regras.

## Uso de IA

Trechos dos prompts utilizados: “Desejo entregar o kit mínimo proposto no desafio” e “[...] comentários úteis no código [...] A linguagem deve ser apenas python”. A IA (modelo GPT-6 SOL) ajudou a delimitar o escopo, organizar as regras e revisar os testes. A sugestão inicial de deixar a integração com dados apenas na documentação foi alterada para incluir a célula AWS comentada. Não houve erro relevante identificado nas respostas usadas.