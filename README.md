# Substabelecimentos por Advogado — versão HTML para GitHub Pages

## Como publicar
1. Crie um repositório no GitHub.
2. Envie todo o conteúdo desta pasta, mantendo `index.html`, `assets/` e `modelos/`.
3. Em **Settings > Pages**, escolha **Deploy from a branch**, branch `main`, pasta `/root`.
4. Abra o endereço publicado pelo GitHub Pages.

## Funcionalidades disponíveis no navegador
- Importação e tratamento da aba **CLIENTES** de uma base Excel.
- Busca e filtros.
- Visão por ocorrências e por documento/cliente em uma linha.
- Consulta das demais abas.
- Edição e exclusão na memória.
- Gravação no mesmo arquivo quando o navegador permite **File System Access API** (Chrome/Edge, mediante autorização).
- Exportação da base e dos resultados.
- Elaboração individual e importação em lote.
- Agrupamento em lote por **GRUPO + UF + GESTOR**.
- Geração de Word no navegador.
- Modelo de importação disponível para download.

## Limitações da hospedagem estática
GitHub Pages não executa Python/Playwright e não tem acesso irrestrito ao computador. Por isso:
- o RPA automático da Lexio não roda dentro do GitHub Pages;
- a automação de login, upload, posicionamento de carimbos e captura de URL exige um backend/robô local;
- a prévia do Word no navegador é aproximada; a paginação 100% fiel depende do Microsoft Word;
- o acesso automático ao SharePoint requer Microsoft Graph/Azure ou uma pasta sincronizada escolhida pelo usuário.

A interface já está preparada para uma futura API. Para manter o RPA atual, a melhor arquitetura é: **GitHub Pages para a interface + pequeno serviço local/servidor para Lexio, Word e SharePoint**.

## Otimizações desta versão

- Leitura do Excel em segundo plano por Web Worker, evitando travar a interface.
- Pesquisa com pequeno atraso inteligente (debounce), sem filtrar a cada tecla imediatamente.
- Índice de pesquisa criado uma única vez ao carregar a base.
- Tabela exibida em blocos de 250 linhas, com botão **Mostrar mais**.
- Consulta de abas auxiliares limitada inicialmente para manter a janela responsiva.
- Indicador visual durante leitura e gravação da planilha.

Observação: a primeira leitura ainda depende do tamanho da planilha e da velocidade do computador, mas a página deve continuar responsiva e mostrar o andamento.


## Ajuste v5
Ao alternar para **Documento por linha**, a interface exibe uma tela de carregamento com as mensagens **Agrupando Informações** e **Isso pode levar alguns minutos**, evitando a impressão de travamento durante o agrupamento.


## Base padrão no SharePoint
A página tenta carregar automaticamente a planilha padrão do SharePoint. Em navegadores que bloqueiam CORS ou cookies de terceiros, a leitura automática pode falhar; nesse caso, use **Selecionar base Excel**. Para acesso automático garantido em um site estático, é necessário disponibilizar o arquivo com acesso público ou usar um backend autenticado/Microsoft Graph.


## Registro automático na base
Ao gerar um Word, a ferramenta acrescenta os clientes na aba CLIENTES, preenche a data da última alteração e define o link como SUBIR NA LEXIO. Em navegadores compatíveis, grava no mesmo arquivo selecionado; nos demais, baixa automaticamente a base atualizada.


## Regras de acordos
No modo individual, informe separadamente o advogado autorizado até R$ 10.000,00, o sócio gestor e o sócio coordenador para a faixa até R$ 199.999,99, além do gestor validador/diretor para valores acima de R$ 200.000,00.


## Versão 19
- Salvamento corrigido para bases com milhares de colunas formatadas vazias.
- Campo UF em lista suspensa.
- Minutas alinhadas aos modelos oficiais por UF incluídos em `modelos/minutas_oficiais`.


## Base automática pelo navegador
Na primeira utilização, clique em **Selecionar base Excel** e escolha a planilha sincronizada pelo OneDrive/SharePoint. O Chrome ou Edge memorizará a referência do arquivo neste computador e tentará carregá-la automaticamente nas próximas aberturas. Caso a permissão expire, o botão mudará para **Autorizar base salva**.
