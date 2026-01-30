# ImportaPedidosCSV

Rotina TLPP para importação de pedidos de venda a partir de arquivos CSV. A solução valida informações, verifica duplicidades e cria pedidos (SC5/SC6) via MSEXECAUTO.

## Estrutura dos Arquivos CSV

Separador: `;` | Encoding: UTF-8

**pedidos_header.csv:**

- Filial, Emissao (DD/MM/AAAA), Cliente, Loja, CondPag, TabelaPreco, Vendedor, Obs, Origem

**pedidos_itens.csv:**

- PedidoExterno, Item, Produto, Quantidade, PrecoUnit, DescontoPerc

## Como Usar

1. Coloque os arquivos CSV no diretório desejado
2. No Protheus, carregue o fonte `ImportaPedidosCSV.tlpp`
3. Execute via User Function:
   ```
   ImportaPedidosCSV()
   ```
   Ou diretamente com os caminhos:
   ```
   ImportaPedidosCSV():Importa("c:\caminho\pedidos_header.csv", "c:\caminho\pedidos_itens.csv")
   ```

## Validações Implementadas

- ✅ Existência do cliente em SA1
- ✅ Existência do produto em SB1
- ✅ Quantidade > 0
- ✅ Preço > 0
- ✅ Origem válida (CRM, Ecommerce, Protheus)
- ✅ Pedido criado apenas com itens válidos
- ✅ Evita duplicidade no lote (PedidoExterno)

## Evolução do Projeto

### Melhores e Correções Realizadas

- **Correção de Loop/Continue:** Substituição de comandos `Continue` e `Loop` por controle de fluxo com flags booleanas, garantindo compatibilidade e legibilidade.
- **Validação de Chaves (DbSeek/AvKey):** Refatoração das métodos `ValidaCliente` e `ValidaProduto` para utilizar `MsSeek` combinado com `AvKey` e `AllTrim`, assegurando buscas corretas independente de espaços em branco e posicionamento de filiais (`FWxFilial`).
- **Hashmap com JsonObject:** Correção da estrutura de dados para agrupar header e itens, substituindo Arrays simples por `JsonObject` para permitir indexação por string (chave do pedido).
- **Refatoração de Código:** Quebra do método monolítico `ExecutaPedidos` em métodos menores e especialistas (`PreparaPedidos`, `ValidaCabecalho`, `ValidaItensPedido`, `GravaPedidos`).
- **Flexibilidade no Header:** O campo "Origem" agora é tratado como opcional na importação.

## Métodos Disponíveis

| Método             | Descrição                                   |
| ------------------ | ------------------------------------------- |
| `Importa()`        | Inicia o processo de importação             |
| `LoadCSV()`        | Lê arquivo CSV e retorna array mapeado      |
| `AgrupaItens()`    | Agrupa itens por PedidoExterno              |
| `ValidaCliente()`  | Verifica existência em SA1                  |
| `ValidaProduto()`  | Verifica existência em SB1                  |
| `ValidaOrigem()`   | Valida origem do pedido                     |
| `ExecutaPedidos()` | Executa a criação de pedidos via MSEXECAUTO |

## Observações Importantes

- A montagem do `aDat` está exemplarizada. Ajuste os campos SC5/SC6 conforme seu dicionário
- Para evitar reimportação, implemente verificação persistente em SC5
- Logs de validação são exibidos via `ConOut()` no console Protheus
- O campo `C5_ORIGEM` é preenchido com um dos valores: CRM, Ecommerce, Protheus

## Próximos Passos Sugeridos

1. Validar mapeamento de campos SC5/SC6 com seu dicionário Protheus
2. Implementar verificação persistente de duplicidade em SC5
3. Adicionar carregamento opcional de `clientes_seed.csv` e `produtos_seed.csv`
4. Criar vídeo demonstrativo da execução
