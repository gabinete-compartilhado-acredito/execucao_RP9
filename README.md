# Execução orçamentária das emendas de relator (RP9)


## Apresentação

Aqui nós disponibilizamos dados a respeito da execução orçamentária (e.g. empenhos) de emendas do Relator Geral
(RP9) destinadas a alguns órgãos selecionados (e.g. FNDE e MDR), realizadas nos anos de 2020/2021. Além disso, também
disponibilizamos alguns dados auxiliares que foram utilizados, como a lista de prefeitos eleitos em 2020 e tabelas de
correspondências entre códigos de municípios de diferentes sistemas/órgãos, e o código de raspagem (web scraping)
das informações orçamentárias do Portal da Transparência.

## Reportagens que utilizaram esses dados

* [Governo destinou R$ 5,7 bilhões do orçamento secreto nos últimos dias de 2021](https://oglobo.globo.com/politica/governo-destinou-57-bilhoes-do-orcamento-secreto-nos-ultimos-dias-de-2021-25347221)
* [Distribuição de verbas gera conflitos e intrigas no Planalto e no Congresso](https://oglobo.globo.com/politica/distribuicao-de-verbas-gera-conflitos-intrigas-no-planalto-no-congresso-2-25346748)

## Tabelas disponíveis

### `dados/aux/conexao_cnpj-2019-2021_prefeitos-2020.csv`

Tabela que associa cada CNPJ favorecido por emendas (que podem ser de municípios, escolas, associações, etc) ao município
onde o favorecido está localizado, aos códigos do SIAFI, IBGE e TSE que se referem a esse município e ao prefeito do
município, com seu partido. Essa tabela foi construída da seguinte forma:

1. Pegamos os dados das [transferências](http://www.portaltransparencia.gov.br/download-de-dados/transferencias)
realizadas de 2019 a 2021 pelo governo federal no Portal da Transparência, onde consta os CNPJs, nomes e municípios
dos favorecidos dessas transferências, junto com o código SIAFI do município.

2. Selecionamos uma entrada para cada CNPJ, dando preferência, nos raros casos de duplicadade, àquelas para as quais o município
é informado.

3. Cruzamos a seleção acima com uma [tabela](https://www.tesourotransparente.gov.br/ckan/dataset/abb968cb-3710-4f85-89cf-875c91b9c7f6/resource/eebb3bc6-9eea-4496-8bcf-304f33155282/download/TABMUN.CSV) que traduz o código SIAFI dos municípios para o código do IBGE.

4. Cruzamos o resultado com uma a [tabela denominada "municipios"](https://basedosdados.org/dataset/br-bd-diretorios-brasil)
que relaciona o código IBGE do município com o código do TSE.

5. Baixamos o resultado das eleições (dados dos candidatos) de 2020 do [repositório de dados do TSE](https://www.tse.jus.br/eleicoes/estatisticas/repositorio-de-dados-eleitorais-1/) e selecionamos
os prefeitos eleitos, assim como seus partidos na época da eleição.

6. Cruzamos os dados do TSE, selecionados da forma acima, com nossa tabela anterior, obtendo o resultado final.

Portanto, é importante notar que:

* Os prefeitos que aparecem na tabela final são os eleitos em 2020 (ou em eleições suplementares posteriores,
até o momento da análise). Por isso, os raros casos nos quais o prefeito pode ter renunciado, falecido ou
sido removido do cargo não são considerados. Além disso, possíveis trocas de partidos posteriormente à eleição
também não são consideradas.

* Vale lembrar que o CNPJ que acaba associado a um prefeito não é, necessariamente, do município em questão.
Ele pode ser de uma entidade localizada no município.

* É possível que no cruzamento das várias tabelas algum código de município possa estar faltando, de maneira que
  a associação não é exaustiva (i.e. podem existir CNPJs de municípios sem municípios associados).

* Algumas transferências foram feitas a entidades que não possuem localização precisa na tabela de transferências,
de maneira que qualquer informação associada ao município estará vazia.

### `dados/aux/municipios_cod_ibge_tse.csv` e  `municipios_cod_siafi_ibge.csv`

São tabelas que relacionam os códigos dos municípios utilizados pelo IBGE com os códigos utilizado pelo TSE
(primeiro arquivo) e com os códigos utilizados pelo SIAFI (segundo arquivo).

### `dados/brutos/ptransp/scrap_fnde/documentos-empenho_emendas-relator_FNDE.csv`

Esses dados foram obtidos da concatenação dos detalhes de todas as execuções orçamentárias apresentadas pelo
Portal da Transparência na [consulta manual](http://www.portaltransparencia.gov.br/despesas/orgao/consulta?paginacaoSimples=true&tamanhoPagina=&offset=&direcaoOrdenacao=asc&de=01%2F12%2F2021&ate=31%2F12%2F2021&orgaos=OR26298&autor=8100&colunasSelecionadas=linkDetalhamento%2CmesAno%2CorgaoSuperior%2CorgaoVinculado%2CunidadeGestora%2Cfuncao%2CsubFuncao%2Cprograma%2Cacao%2CprogramaGoverno%2Cautor%2CplanoOrcamentario%2CgrupoDespesa%2CelementoDespesa%2CmodalidadeDespesa%2CvalorDespesaEmpenhada%2CvalorDespesaLiquidada%2CvalorDespesaPaga%2CvalorRestoPago&ordenarPor=valorDespesaEmpenhada&direcao=desc)
sobre a execução do FNDE de emendas do relator em dezembro de 2021.
Essa metodologia foi adotada em detrimento da utilização dos [dados do portal](http://www.portaltransparencia.gov.br/download-de-dados/despesas) pois, na época da coleta, estes últimos
não estavam disponíveis.

### `dados/brutos/ptransp/scrap_mdr/documentos-empenho_emendas-relator_MDR.csv`

Esses dados foram obtidos da mesma maneira que os acima, mas para a [consulta](https://www.portaltransparencia.gov.br/despesas/orgao/consulta?paginacaoSimples=true&tamanhoPagina=&offset=&direcaoOrdenacao=asc&de=01%2F12%2F2021&ate=31%2F12%2F2021&orgaos=OR53000&autor=8100&colunasSelecionadas=linkDetalhamento%2CmesAno%2CorgaoSuperior%2CorgaoVinculado%2CunidadeGestora%2Cfuncao%2CsubFuncao%2Cprograma%2Cacao%2CprogramaGoverno%2Cautor%2CplanoOrcamentario%2CgrupoDespesa%2CelementoDespesa%2CmodalidadeDespesa%2CvalorDespesaEmpenhada%2CvalorDespesaLiquidada%2CvalorDespesaPaga%2CvalorRestoPago&ordenarPor=valorDespesaEmpenhada&direcao=desc) da execução do MDR.

### `dados/processados/empenhos_2021-12_RP9_FNDE_PTransp+Prefeitos-TSE_cleaned.csv`

Esse é a tabela final produzida para a execução orçamentária do FNDE em dezembro de 2021, de emendas de relator (RP 9). Ela é resultado do cruzamento de `dados/aux/conexao_cnpj-2019-2021_prefeitos-2020.csv` com `dados/brutos/ptransp/scrap_fnde/documentos-empenho_emendas-relator_FNDE.csv` através dos CNPJs dos favorecidos.

### `dados/processados/empenhos_2021-12_RP9_MDR_PTransp+Prefeitos-TSE_cleaned.csv`

Esse é a tabela final produzida para a execução orçamentária do MDR em dezembro de 2021, de emendas de relator (RP 9). Ela é resultado do cruzamento de `dados/aux/conexao_cnpj-2019-2021_prefeitos-2020.csv` com `dados/brutos/ptransp/scrap_mdr/documentos-empenho_emendas-relator_MDR.csv` através dos CNPJs dos favorecidos.

### `empenhos_2020-completo_RP9_FNDE_PTransp+Prefeitos-TSE.csv`

Mesmo que `dados/processados/empenhos_2021-12_RP9_FNDE_PTransp+Prefeitos-TSE_cleaned.csv` mas para o ano inteiro (completo) de 2020. Esses dados foram obtidos com o notebook de web scraping
[analises/web_scraping_ptransp.ipynb](analises/web_scraping_ptransp.ipynb).

### `empenhos_2021-completo_RP9_FNDE_PTransp+Prefeitos-TSE.csv`

Mesmo que `dados/processados/empenhos_2021-12_RP9_FNDE_PTransp+Prefeitos-TSE_cleaned.csv` mas para o ano inteiro (completo) de 2021. Esses dados foram obtidos com o notebook de web scraping
[analises/web_scraping_ptransp.ipynb](analises/web_scraping_ptransp.ipynb).

## Contato

Para maiores informações, entrar em contato com [Henrique Xavier](https://github.com/hsxavier) - henrique.xavier@senado.leg.br






