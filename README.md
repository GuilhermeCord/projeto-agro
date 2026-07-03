# Projeto Agro

Projeto de Business Intelligence para acompanhamento agricola de fazendas, talhoes e culturas. O relatorio consolida informacoes cadastrais, indicadores de saude dos talhoes, clima e solo, notificacoes e visualizacao geografica dos recortes de cada talhao em mapa, usando o visual de mapa do Azure no Power BI.

## Visao geral

O projeto foi desenvolvido em formato PBIP, permitindo versionamento do relatorio e do modelo semantico do Power BI. A solucao tem como objetivo apoiar a leitura rapida da situacao das fazendas monitoradas, com destaque para status de desenvolvimento, saude vegetal, vigor, uniformidade, produtividade estimada e areas por condicao do talhao.

## Principais recursos

- Dashboard executivo com indicadores gerais de fazendas, talhoes, culturas e hectares monitorados.
- Acompanhamento de score de saude, indice de vigor, uniformidade e produtividade.
- Classificacao dos talhoes por status: Saudavel, Atencao, Critico, Em desenvolvimento e Plantado.
- Visualizacao dos talhoes em mapa, com recortes geograficos em arquivo GeoJSON.
- Analise de hectares por status, separando areas saudaveis, em atencao e criticas.
- Indicadores de clima e solo, incluindo chuva, temperatura, umidade do solo, deficit hidrico e risco climatico.
- Notificacoes e recomendacoes associadas aos talhoes.
- Comparacoes temporais, incluindo variacao mes contra mes.
- Tema visual customizado, icones, layouts em modo claro/escuro e mockups de apoio.

## Estrutura do projeto

```text
.
|-- 0. Esquema Projeto/
|   |-- Projeto Agro.pbip
|   |-- Projeto Agro.Report/
|   |   |-- definition/
|   |   `-- StaticResources/
|   `-- Projeto Agro.SemanticModel/
|       |-- definition/
|       `-- diagramLayout.json
|-- 1. Complementos/
|   |-- Bases de Dados/
|   |-- Icones/
|   |-- Layout/
|   |-- Mockup/
|   `-- Tema.json
`-- README.md
```

## Bases de dados

As bases de apoio ficam em `1. Complementos/Bases de Dados/`:

- `dim_fazenda.csv`: cadastro das fazendas, com localizacao, regiao, area total e quantidade de talhoes.
- `dim_talhao.csv`: cadastro dos talhoes, com fazenda, area, coordenadas, solo, declividade, irrigacao e rotulo de mapa.
- `dim_cultura.csv`: cadastro das culturas monitoradas.
- `dim_status_talhao.csv`: tabela de status dos talhoes e cores utilizadas na comunicacao visual.
- `dim_calendario.csv`: calendario para analises temporais.
- `fato_saude_talhao.csv`: indicadores de saude, vigor, uniformidade, produtividade e hectares por condicao.
- `fato_clima_solo.csv`: dados de clima e solo por data, fazenda e talhao.
- `fato_notificacoes.csv`: alertas, notificacoes e recomendacoes.
- `fazendas_brasil_talhoes.geojson`: geometrias dos talhoes para visualizacao no mapa.

No estado atual, o conjunto cadastral possui 5 fazendas, 40 talhoes e 8 culturas.

## Modelo semantico

O modelo semantico esta em `0. Esquema Projeto/Projeto Agro.SemanticModel/` e utiliza tabelas dimensionais e fatos relacionados por chaves de fazenda, talhao, cultura, status e data.

Principais dimensoes:

- `dim_fazenda`
- `dim_talhao`
- `dim_cultura`
- `dim_status_talhao`
- `dim_calendario`

Principais fatos:

- `fato_saude_talhao`
- `fato_clima_solo`
- `fato_notificacoes`

As medidas DAX ficam centralizadas na tabela `Medidas`, com calculos para cadastros, monitoramento, clima e solo, comparativos temporais, formatacoes condicionais, SVGs e componentes HTML usados no relatorio.

## Relatorio

O relatorio esta em `0. Esquema Projeto/Projeto Agro.Report/`.

Paginas identificadas:

- `Dashboard`: pagina principal do relatorio, com KPIs e visao consolidada das fazendas e talhoes.
- `Mapa`: pagina de visualizacao geografica dos talhoes, com recorte por fazenda/talhao e status.
- `Pagina 4`: pagina oculta no modo de exibicao, possivelmente usada como apoio, tooltip, navegacao ou desenvolvimento.

## Como abrir

1. Abra o Power BI Desktop.
2. Use a opcao de abrir projeto/relatorio PBIP.
3. Selecione o arquivo `0. Esquema Projeto/Projeto Agro.pbip`.
4. Verifique os caminhos das fontes de dados em caso de mudanca de diretorio.
5. Atualize o modelo para carregar os CSVs e o GeoJSON da pasta `1. Complementos/Bases de Dados/`.

## Recursos visuais

A pasta `1. Complementos/` concentra os materiais de apoio do projeto:

- `Tema.json`: tema visual customizado.
- `Icones/`: logotipos, icones de score, vigor, uniformidade, filtros, setas e status.
- `Layout/`: telas de dashboard e mapa em versoes light/dark.
- `Mockup/`: imagens de referencia e evolucao visual do relatorio.

## Observacoes

- O projeto usa arquivos de texto e estrutura PBIP, o que facilita versionamento em Git.
- Ao alterar bases CSV, mantenha os nomes das colunas e delimitadores esperados pelo modelo.
- Ao atualizar o GeoJSON, preserve as chaves necessarias para relacionar os recortes do mapa aos talhoes do modelo.
- As medidas de status e saude dependem da data filtrada no relatorio, entao valide sempre o contexto temporal ao comparar resultados.
