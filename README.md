# ImportaPedidosCSV - Instruções

- Arquivos CSV (separador `;`, UTF-8):
  - `pedidos_header.csv`: Filial;Emissao;Cliente;Loja;CondPag;TabelaPreco;Vendedor;Obs
  - `pedidos_itens.csv`: PedidoExterno;Item;Produto;Quantidade;PrecoUnit;DescontoPerc

- Uso
  - Coloque os CSVs na pasta desejada ou ajuste os caminhos no comando abaixo.
  - No Protheus, carregue o fonte `ImportaPedidosCSV.tlpp` e execute:

    ImportaPedidosCSV():Importa("c:\\caminho\\para\\pedidos_header.csv","c:\\caminho\\para\\pedidos_itens.csv")

- Validações aplicadas
  - Verifica existência do cliente em SA1.
  - Verifica existência do produto em SB1.
  - Quantidade > 0 e Preço > 0.
  - Gera pedido apenas se houver pelo menos um item válido.
  - Evita duplicidade dentro do mesmo lote (mesmo `PedidoExterno` no CSV).

- Observações
  - A rotina valida e prepara os pedidos. É necessário mapear os campos do header
    (SC5) e dos itens (SC6) para montar o `aDat` adequado ao `MSEXECAUTO` antes de
    executar em produção.
  - Para evitar reimportação de pedidos já gravados, implemente verificação em `SC5`.

- Convenções de commit
  - `feat:` para novas funcionalidades
  - `fix:` correção de bugs
  - `chore:` tarefas não funcionais
  - `refactor:` refatoração sem mudança de comportamento

- Próximos passos sugeridos
  1. Implementar montagem completa do `aDat` e chamada de `MSEXECAUTO`.
  2. Adicionar verificação persistente de duplicidade em `SC5`.
  3. Criar rotinas opcionais para carregar `clientes_seed.csv` e `produtos_seed.csv`.
# ImportaPedidosCSV - Instruções

- Arquivos CSV (separador `;`, UTF-8):
  - `pedidos_header.csv`: Filial;Emissao;Cliente;Loja;CondPag;TabelaPreco;Vendedor;Obs
  - `pedidos_itens.csv`: PedidoExterno;Item;Produto;Quantidade;PrecoUnit;DescontoPerc

- Uso
  - Coloque os CSVs na pasta desejada ou ajuste os caminhos no comando abaixo.
  - No Protheus, carregue o fonte `ImportaPedidosCSV.tlpp` e execute:

    ImportaPedidosCSV():Importa("c:\\caminho\\para\\pedidos_header.csv","c:\\caminho\\para\\pedidos_itens.csv")

- Validações aplicadas
  - Verifica existência do cliente em SA1.
  - Verifica existência do produto em SB1.
  - Quantidade > 0 e Preço > 0.
  - Gera pedido apenas se houver pelo menos um item válido.
  - Evita duplicidade dentro do mesmo lote (mesmo `PedidoExterno` no CSV).

- Observações
  - A rotina valida e prepara os pedidos. É necessário mapear os campos do header
    (SC5) e dos itens (SC6) para montar o `aDat` adequado ao `MSEXECAUTO` antes de
    executar em produção.
  - Para evitar reimportação de pedidos já gravados, implemente verificação em `SC5`.

- Convenções de commit
  - `fix:` correção de bug
  - `chore:` tarefa não funcional
  - `refactor:` refatoração sem mudança de comportamento

- Próximos passos sugeridos
  1. Implementar montagem completa do `aDat` e chamada de `MSEXECAUTO`.
  2. Adicionar verificação persistente de duplicidade em `SC5`.
  3. Criar rotinas opcionais para carregar `clientes_seed.csv` e `produtos_seed.csv` quando necessário.
