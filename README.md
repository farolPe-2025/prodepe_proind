# PRODEPE e PROIND em Pernambuco – mapa interativo

Mapa de calor interativo dos projetos aprovados no PRODEPE e no PROIND, por município de Pernambuco, a partir da planilha de novos investimentos da ADEPE. O site mostra, para cada município, o número de empresas, o número de projetos, o investimento previsto e os empregos gerados, e recalcula o mapa a cada filtro aplicado.

**Site:** https://farolpe-2025.github.io/prodepe_proind/

## O que o site permite

O usuário escolhe o indicador exibido no mapa (empresas, projetos, investimento ou empregos) e restringe a base por programa (PRODEPE ou PROIND), ano do decreto, segmento de atividade, tipo de projeto, natureza do projeto, região de desenvolvimento e condição de empreendimento (novo ou já existente). Os quatro totais do topo, o ranking dos dez maiores municípios e a barra de escala acompanham o filtro. Ao passar o mouse sobre um município aparece o resumo dos quatro indicadores; ao clicar, o painel lateral detalha o município por ano e por segmento. Há ainda uma opção de escala linear e três paletas de cor.

O visual segue o padrão dos mapas de infografia usados nos estudos do NAIEE: título em destaque, subtítulo em cinza, escala contínua resumida numa barra fina com apenas os valores das pontas e municípios sem projeto em cinza. A página tem dois temas, claro e escuro, alternáveis pelo botão no canto superior direito; na primeira visita ela segue a preferência do sistema e depois lembra a escolha do usuário.

O site é responsivo. No celular, o indicador e os totais ficam no topo, o mapa aparece inteiro logo abaixo, com botões de ampliar e reduzir e rolagem lateral, e um toque em um município mostra os valores e abre o detalhamento logo abaixo do mapa. Os filtros ficam numa gaveta aberta pelo botão "Filtros", que informa quantos estão ativos, e o botão "Ver mapa" a fecha. As mudanças de filtro valem imediatamente, mesmo com a gaveta aberta.

## Base utilizada (posição de setembro de 2026)

A base tem 913 projetos, 773 empresas distintas, 77 municípios com ao menos um projeto, R$ 3,27 bilhões de investimento previsto (a preços de 2026) e 11.254 empregos, com decretos até agosto de 2026. Como 2026 ainda está em curso, os dados do ano cobrem apenas parte dele.

## Tratamento dos dados

**Deflação.** Todos os valores monetários são levados a preços do último ano da planilha de deflatores (2026), com base no IPCA do IBGE. O fator é aplicado segundo o ano do decreto, e os valores são apresentados em R$ milhões.

**Anonimização.** O nome da empresa é usado apenas para contar empresas distintas: é normalizado, convertido em um código inteiro sorteado e descartado. O número do decreto, a data e qualquer texto livre da planilha não são publicados. O notebook confere, antes de gravar o site, que nenhum nome de empresa aparece no HTML gerado. Nenhum arquivo de dados brutos é versionado (ver `.gitignore`).

**Contagem de empresas.** Uma empresa com vários projetos no mesmo município conta uma única vez naquele município; nos totais do estado, conta uma única vez no estado. Empresas com grafias diferentes do mesmo nome podem ser contadas em duplicidade.

**Padronização.** A região de desenvolvimento de algumas linhas estava preenchida com o nome de um segmento e foi reconstituída a partir do município. Erros de digitação de municípios foram corrigidos, as 30 grafias de segmento foram agrupadas em 15 categorias e a natureza do projeto foi agrupada em quatro classes. Projetos do PROIND não têm segmento informado na planilha e aparecem como "Não informado (PROIND)"; filtrar por um segmento específico, portanto, exclui o PROIND. Linhas sem investimento ou emprego informado (em geral, importação e centrais de distribuição do PRODEPE) contam como projeto e empresa, mas entram com zero nas somas.

**Malha.** Shapefile municipal do IBGE (2025), recortado para Pernambuco, sem Fernando de Noronha, simplificado preservando a vizinhança entre municípios e convertido em caminhos SVG.

## Como regenerar o site

O notebook `notebooks/prodepe_proind_01_mapa_interativo.ipynb` lê a planilha, os deflatores e o shapefile, e grava `docs/index.html`. Requer Python com `pandas`, `openpyxl`, `geopandas`, `pyogrio`, `shapely` e `matplotlib`. Os caminhos de entrada são definidos na primeira célula; a pasta de dados pode ser indicada pela variável de ambiente `PRODEPE_BASE` e a de saída por `PRODEPE_OUT`. Depois de executar, basta versionar o novo `docs/index.html`.

## Estrutura

```
docs/index.html                                   site completo (HTML único, sem dependências além da fonte)
notebooks/prodepe_proind_01_mapa_interativo.ipynb notebook que gera o site
```

## Fonte e responsabilidade

Fonte: ADEPE (planilha de novos investimentos, PRODEPE e PROIND). Elaboração: Secretaria de Desenvolvimento Econômico de Pernambuco (SDEC-PE), Núcleo de Estudos Econômicos (NAIEE).
