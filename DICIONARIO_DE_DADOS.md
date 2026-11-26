# Dicionário de dados

Este documento descreve as variáveis do trabalho "Mortes violentas em Mato Grosso do Sul, 2016–2024: trânsito × agressão". Ele acompanha o notebook `E4_entrega_final.ipynb` e os arquivos da pasta `dados/` do `dados.zip`.

Ele traz duas coisas: as colunas **como vêm de cada fonte** (A.1 a A.7 e A.9) e as variáveis **criadas no notebook** (A.8).

**Como ler.**

- `c.NNN` é o número da célula do notebook, contando a partir de 0 (a célula de título é a `c.0`; a primeira célula de código é a `c.1`).
- "Usada em" cita a seção do notebook que usa a coluna. "Não usada na análise" quer dizer que a coluna está no arquivo, mas nenhuma tabela, conta ou gráfico do notebook a utiliza.
- "Origem da descrição" diz de onde veio a descrição: o documento oficial (com a página, quando o notebook a cita) ou "elaborada neste trabalho" (descrição feita pelo grupo, a partir do nome da coluna e dos valores que aparecem no arquivo).
- Quando o significado de um código não está em nenhum documento que o trabalho tenha, a descrição diz "significado não documentado na fonte". Nenhum significado foi inventado.
- Os arquivos CSV do SIM, da PRF e da RAIS usam `;` como separador; o do VDE, o do IBGE e `tb_regsaud.csv` usam `,`. As colunas "Tipo" dizem como o dado é lido: texto, inteiro, decimal, data ou código (texto que identifica uma categoria ou um lugar e que não se soma).

**Índice.** A.1 SIM · A.2 RAIS · A.3 PRF · A.4 VDE · A.5 IBGE (população e municípios) · A.6 Região de saúde (DATASUS) · A.7 SIGO · A.8 Variáveis criadas no notebook · A.9 Arquivos de controle da entrega.

---

## A.1 SIM: `sim_ms_2016_2024.csv`

Fonte: Sistema de Informações sobre Mortalidade (Ministério da Saúde). Dicionário oficial: Dicionário de dados do SIM, versão de 06/2025 (`Dicionario_SIM_2025.pdf`). O arquivo tem 172.231 linhas e 15 colunas, todas lidas como texto (c.25). Na limpeza, sete colunas ganham outro nome (regra SIM-12, c.77); o nome novo aparece entre parênteses.

| Variável | Descrição | Tipo | Valores ou códigos | Usada em | Origem da descrição |
|---|---|---|---|---|---|
| `ANO` | Ano do arquivo de origem | inteiro (lido como texto) | 2016 a 2024 | 4b.1 (SIM-5, RAIS-6), 4c | Elaborada neste trabalho (vem do nome do arquivo) |
| `CONTADOR` | Número de ordem do registro dentro do ano | inteiro (lido como texto) | de 1 a 99999; não é único entre os anos | 4b.1 (identificação das linhas no log e nos duplicados, SIM-5) | Elaborada neste trabalho (não consta do dicionário do SIM) |
| `TIPOBITO` (`TIPO_OBITO`) | Tipo do óbito | código | 1 fetal; 2 não fetal. No arquivo só aparece 2 | 4b.1 (SIM-3) | Dicionário SIM, p. 1 |
| `DTOBITO` (`DATA_OBITO`) | Data do óbito | data, no formato `ddmmaaaa` | 8 caracteres; em 11.750 linhas de 2022 e 2023 vem com 7 e recebe o zero à esquerda | 4b.1 (SIM-2), 4c | Dicionário SIM, p. 1 |
| `CODMUNOCOR` (`MUN_MORTE`) | Município de ocorrência do óbito | código | Código IBGE de 6 dígitos; começa com `50` quando é MS | 4b.1 (SIM-4), 4c, 5 a 10 | Dicionário SIM, p. 3 |
| `CODMUNRES` (`MUN_MORADIA`) | Município de residência | código | Código IBGE de 6 dígitos; começa com `50` quando é MS | 4b.1 (SIM-4), 4c, 5 | Dicionário SIM, p. 3 |
| `LOCOCOR` (`LOC_MORTE`) | Local de ocorrência do óbito | código | 1 hospital; 2 outro estabelecimento de saúde; 3 domicílio; 4 via pública; 5 outros; 6 aldeia indígena; 9 ignorado. No arquivo aparecem 1, 2, 3, 4, 5 e 9 | 4c (`VIA_PUBLICA`), 5.2 | Dicionário SIM, p. 3 |
| `CAUSABAS` (`CAUSA_CID`) | Causa básica do óbito, pela CID-10 | código | Letra e números (3 ou 4 caracteres, ex.: `V892`, `X954`) | 4b.1 (SIM-6), 4c (`CATEGORIA`), 5 a 9 | Dicionário SIM, p. 5 |
| `CIRCOBITO` (`CIRCUNSTANCIA`) | Tipo de morte externa | código | 1 acidente; 2 suicídio; 3 homicídio; 4 outros; 9 ignorado; vazio quando a morte não é externa (152.511 linhas) | 5.5 | Dicionário SIM, p. 5 |
| `IDADE` | Idade em 3 caracteres | código composto | 1º caractere = unidade (4 anos; 5 = mais de 100 anos; 9 ignorado); 2 últimos = quantidade. Também aparecem os dígitos 0 a 3 (minutos, horas, dias e meses, pelas faixas dos valores) e 79 valores com menos de 3 caracteres | 4b.1 (SIM-10), 6.1 | Dicionário SIM, p. 2 |
| `SEXO` | Sexo | código | 1 masculino; 2 feminino; 0 ou 9 ignorado. No arquivo aparecem 0 (24 linhas), 1 e 2 | 4b.1 (SIM-9), 6.1 | Dicionário SIM, p. 2 |
| `RACACOR` | Raça/cor | código | 1 branca; 2 preta; 3 amarela; 4 parda; 5 indígena; vazio em 835 linhas | 4b.1 (SIM-8), 6.2 | Dicionário SIM, p. 2 |
| `ESTCIV` | Situação conjugal | código | 1 solteiro; 2 casado; 3 viúvo; 4 separado judicialmente/divorciado; 5 união estável; 9 ignorado; vazio em 7.795 linhas | 4b.1 (SIM-8), 6.2 | Dicionário SIM, p. 2 |
| `ESC2010` | Escolaridade (última série concluída) | código | 0 sem escolaridade; 1 fundamental I; 2 fundamental II; 3 médio; 4 superior incompleto; 5 superior completo; 9 ignorado; vazio em 8.653 linhas | 4b.1 (SIM-8), 6.2 | Dicionário SIM, p. 2 |
| `OCUP` | Ocupação habitual (CBO 2002, 6 dígitos) | código | 6 dígitos; 299 linhas vêm com 5 e recebem o zero à esquerda; 17.924 vazias. Códigos especiais: 999991 a 999995 e 998999 (ver A.8, `OCUP_ROTULO`) | 4b.1 (SIM-7, SIM-11), 4b.2 (RAIS-6), 6.3 | Dicionário SIM, p. 2 (CBO 2002, 6 dígitos); códigos especiais em `CBO2002.CNV` do TABNET (DATASUS) |

---

## A.2 RAIS: `rais_vinculos_ms_2016_2024.csv` e `rais_fontes.csv`

Fonte: Relação Anual de Informações Sociais (Ministério do Trabalho), vínculos de emprego. O recorte de MS tem 9.948.113 linhas de dados (uma por vínculo) e 4 colunas, lidas como texto (c.81). O layout usado como referência é `RAIS_vinculos_layout2020.xls`, aba "RAISD - layout". Ele é de 2020 e não cobre os anos seguintes.

### `rais_vinculos_ms_2016_2024.csv`

| Variável | Descrição | Tipo | Valores ou códigos | Usada em | Origem da descrição |
|---|---|---|---|---|---|
| `ANO` | Ano do arquivo da RAIS de onde vem o vínculo | inteiro (lido como texto) | 2016 a 2024 | 4b.2 | Elaborada neste trabalho (vem do arquivo de origem) |
| `CBO_2002` | Ocupação do vínculo, pela CBO 2002 | código | 6 dígitos. Casos tratados na limpeza: `0000-1` (ignorado, layout), 14.357 códigos de 5 dígitos (em 2023 e 2024, completados com zero), `000000` e `999999` (a partir de 2022; significado não documentado na fonte) | 4b.2 (RAIS-1 a RAIS-6) | Layout da RAIS (`RAIS_vinculos_layout2020.xls`, aba RAISD - layout, sem página); `999999`: significado não documentado na fonte |
| `REM_MEDIA_SM` | Remuneração média do vínculo, em salários mínimos | decimal (lido como texto) | Aparece como `000004,51` (vírgula decimal, zeros à esquerda) e como `.89` ou `1.55` (ponto decimal). Zero (`000000,00`, `.00`) quer dizer vínculo sem remuneração no ano | 4b.2 (RAIS-4, RAIS-5) | Layout da RAIS (coluna `Vl Remun Média (SM)`, sem página) |
| `MUNICIPIO` | Município do vínculo | código | Código de 6 dígitos (IBGE sem o dígito verificador); 79 códigos distintos, todos de MS | 4b.2 (só a contagem de municípios distintos, c.81); não usada na análise | Elaborada neste trabalho (pelos valores e pela ligação com o código de 6 dígitos usado nas demais bases) |

### `rais_fontes.csv`

Uma linha por ano (9 linhas). Registra de onde veio cada arquivo da RAIS e quantas linhas foram lidas no recorte.

| Variável | Descrição | Tipo | Valores ou códigos | Usada em | Origem da descrição |
|---|---|---|---|---|---|
| `ano` | Ano da RAIS | inteiro | 2016 a 2024 | 4b.2 (conferência, c.83) | Elaborada neste trabalho |
| `arquivo` | Nome do arquivo no FTP | texto | `MS2016.7z`, `MS2017.7z` e `RAIS_VINC_PUB_CENTRO_OESTE_ANO.7z` (2018 a 2024, com o ano acrescentado ao nome) | Não usada na análise | Elaborada neste trabalho |
| `url` | Endereço do arquivo no FTP do Ministério do Trabalho | texto | Endereços `ftp://ftp.mtps.gov.br/pdet/microdados/RAIS/ANO/...` | Não usada na análise | Elaborada neste trabalho |
| `bytes` | Tamanho do `.7z` | inteiro | De 37.275.317 a 343.753.235 | Não usada na análise | Elaborada neste trabalho |
| `data_ftp` | Data do arquivo no FTP | data (`aaaa-mm-dd`) | De 2017-10-19 a 2026-05-18 | Não usada na análise (as datas aparecem na tabela de fontes do notebook, c.0) | Elaborada neste trabalho |
| `separador` | Separador de colunas do arquivo original | texto | `;` (7 anos) e `,` (2 anos) | Não usada na análise | Elaborada neste trabalho |
| `coluna_cbo` | Nome da coluna de ocupação no arquivo original | texto | `CBO Ocupação 2002` (7 anos); `CBO 2002 Ocupação - Código` (2 anos) | Não usada na análise | Elaborada neste trabalho |
| `coluna_rem` | Nome da coluna de remuneração no arquivo original | texto | `Vl Remun Média (SM)` (7 anos); `Vl Rem Média (SM)` (2 anos) | Não usada na análise | Elaborada neste trabalho |
| `coluna_municipio` | Nome da coluna de município no arquivo original | texto | `Município` (7 anos); `Município - Código` (2 anos) | Não usada na análise | Elaborada neste trabalho |
| `linhas_lidas` | Linhas de dados lidas no arquivo original (Brasil ou Centro-Oeste) | inteiro | De 997.933 a 8.732.359 | Não usada na análise | Elaborada neste trabalho |
| `linhas_ms` | Linhas que ficaram no recorte de MS | inteiro | De 971.173 a 1.385.141; soma 9.948.113 | 4b.2 (c.83: a contagem por ano do arquivo lido tem de bater com esta coluna) | Elaborada neste trabalho |
| `linhas_curtas` | Linhas sem a coluna de município, que não dão para atribuir a uma UF; só são contadas | inteiro | 0 em todos os anos | Não usada na análise | Elaborada neste trabalho (comentário do código de recorte da RAIS, c.11) |

---

## A.3 PRF: `prf_ms_2016_2025.csv`

Fonte: Polícia Rodoviária Federal, acidentes em rodovias federais (arquivos `datatran`, um por ano). O recorte tem os acidentes com `uf = MS`, de 2016 a 2025: 17.372 linhas e 31 colunas (as 30 do arquivo da PRF mais `ANO`), todas lidas como texto (c.121). A PRF publica 25 colunas em 2016 e 30 de 2017 em diante; as 5 colunas a mais (`latitude`, `longitude`, `regional`, `delegacia`, `uop`) ficam vazias em 2016 (2.466 linhas). O trabalho não usa um dicionário da PRF: as descrições vêm dos nomes das colunas e dos valores do arquivo.

| Variável | Descrição | Tipo | Valores ou códigos | Usada em | Origem da descrição |
|---|---|---|---|---|---|
| `id` | Identificador do acidente | código | 17.372 valores distintos em 17.372 linhas | 4b.4 (PRF-1), 7.2 (contagem de acidentes) | Elaborada neste trabalho |
| `data_inversa` | Data do acidente | data | `dd/mm/aa` em 2016 (ex.: `01/01/16`); `aaaa-mm-dd` de 2017 em diante | 4b.4 (PRF-3, vira `DATA_ACIDENTE`) | Elaborada neste trabalho |
| `dia_semana` | Dia da semana do acidente | texto | 2016: `Domingo`, `Segunda`, `Terça`, `Quarta`, `Quinta`, `Sexta`, `Sábado`. De 2017 em diante: `domingo`, `segunda-feira`, `terça-feira`, `quarta-feira`, `quinta-feira`, `sexta-feira`, `sábado` | Não usada na análise | Elaborada neste trabalho |
| `horario` | Hora do acidente | texto (`hh:mm:ss`) | De `00:00:00` a `23:59:00` | Não usada na análise | Elaborada neste trabalho |
| `uf` | Unidade da federação | código (renomeada `UF`) | `MS` em todas as linhas | 4b.4 (PRF-4, conferência de que todas são MS) | Elaborada neste trabalho |
| `br` | Número da rodovia federal (BR) | código | 12 valores: 0, 60, 158, 163, 262, 267, 359, 376, 419, 436, 463, 487. O valor `0` aparece em 52 linhas; significado não documentado na fonte | Não usada na análise | Elaborada neste trabalho |
| `km` | Quilômetro da rodovia onde ocorreu o acidente | decimal (vírgula decimal, ex.: `257,3`) | De 0 a 1.530 | 4b.4 (PRF-2, conversão para número); não usada na análise | Elaborada neste trabalho |
| `municipio` | Município do acidente, em maiúsculas e sem acento | texto (renomeada `MUNICIPIO`) | 63 nomes distintos, todos de MS | 4b.4 (PRF-4, liga ao código IBGE), 7.2 | Elaborada neste trabalho |
| `causa_acidente` | Causa do acidente | texto | 92 categorias (ex.: `Velocidade incompatível`, `Defeito mecânico em veículo`) | Não usada na análise | Elaborada neste trabalho |
| `tipo_acidente` | Tipo do acidente | texto | 31 categorias (ex.: `Colisão traseira`, `Saída de Pista`, `Tombamento`) | Não usada na análise | Elaborada neste trabalho |
| `classificacao_acidente` | Gravidade do acidente | texto | `Com Vítimas Fatais` (1.251), `Com Vítimas Feridas` (12.036), `Sem Vítimas` (4.041), `Ignorado` (44) | Não usada na análise | Elaborada neste trabalho |
| `fase_dia` | Fase do dia | texto | `Amanhecer`, `Pleno dia`, `Anoitecer` e `Plena Noite` (2017 em diante) ou `Plena noite` (2016) | Não usada na análise | Elaborada neste trabalho |
| `sentido_via` | Sentido da via | texto | `Crescente` (10.284), `Decrescente` (7.036), `Não Informado` (52) | Não usada na análise | Elaborada neste trabalho |
| `condicao_metereologica` | Condição do tempo (a grafia "metereologica" é a do arquivo) | texto | `Céu Claro` (2016: `Ceu Claro`), `Chuva`, `Garoa/Chuvisco`, `Granizo`, `Ignorado` (2016: `Ignorada`), `Nevoeiro/Neblina` (2016: `Nevoeiro/neblina`), `Nublado`, `Sol`, `Vento` | Não usada na análise | Elaborada neste trabalho |
| `tipo_pista` | Tipo de pista | texto | `Simples` (14.457), `Dupla` (2.801), `Múltipla` (114) | Não usada na análise | Elaborada neste trabalho |
| `tracado_via` | Traçado da via | texto | 149 combinações, separadas por `;` (ex.: `Reta`, `Curva`, `Cruzamento`, `Viaduto;Reta`) | Não usada na análise | Elaborada neste trabalho |
| `uso_solo` | Uso do solo no local | texto | 2016: `Urbano` (657) e `Rural` (1.809). De 2017 em diante: `Sim` e `Não`. A equivalência entre as duas formas não está documentada na fonte | Não usada na análise | Elaborada neste trabalho |
| `pessoas` | Total de pessoas envolvidas no acidente | inteiro | De 1 a 60 | Não usada na análise | Elaborada neste trabalho |
| `mortos` | Pessoas mortas no acidente | inteiro (renomeada `MORTOS_PRF`) | De 0 a 8 | 4b.4 (PRF-4), 7.2, 7.3, 8.4 | Elaborada neste trabalho |
| `feridos_leves` | Feridos leves | inteiro | De 0 a 31 | Não usada na análise | Elaborada neste trabalho |
| `feridos_graves` | Feridos graves | inteiro | De 0 a 10 | Não usada na análise | Elaborada neste trabalho |
| `ilesos` | Pessoas ilesas | inteiro | De 0 a 60 | Não usada na análise | Elaborada neste trabalho |
| `ignorados` | Pessoas com condição ignorada | inteiro | De 0 a 31 | Não usada na análise | Elaborada neste trabalho |
| `feridos` | Total de feridos | inteiro | De 0 a 31. Em todas as linhas é igual a `feridos_leves` + `feridos_graves` | Não usada na análise | Elaborada neste trabalho |
| `veiculos` | Veículos envolvidos | inteiro | De 1 a 14 | Não usada na análise | Elaborada neste trabalho |
| `ANO` | Ano do arquivo de origem (coluna acrescentada ao recorte) | inteiro (lido como texto) | 2016 a 2025 | 4b.4 (PRF-1, PRF-3), 7.2 | Elaborada neste trabalho |
| `latitude` | Latitude do acidente | decimal (vírgula decimal) | Vazia em 2016 (2.466 linhas); de 2017 em diante, graus decimais negativos | 4b.4 (PRF-2, conversão); não usada na análise | Elaborada neste trabalho |
| `longitude` | Longitude do acidente | decimal (vírgula decimal) | Vazia em 2016 (2.466 linhas); de 2017 em diante, graus decimais negativos | 4b.4 (PRF-2, conversão); não usada na análise | Elaborada neste trabalho |
| `regional` | Regional da PRF responsável pelo trecho | código | `SPRF-MS` (14.902), `SPRF-PR` (4); vazio em 2016 | Não usada na análise | Elaborada neste trabalho |
| `delegacia` | Delegacia da PRF responsável pelo trecho | código | `DEL01-MS` a `DEL09-MS`, `DEL06-PR` e `N/A`; vazio em 2016 | Não usada na análise | Elaborada neste trabalho |
| `uop` | Unidade operacional da PRF (a sigla não é expandida na fonte) | código | 29 valores (ex.: `UOP01-DEL01-MS`, `DEL3/7-UOP01/MS`) e `N/A`; vazio em 2016. Significado da sigla não documentado na fonte | Não usada na análise | Elaborada neste trabalho |

---

## A.4 VDE: `v0_vde_ms_bruto_2016_2024.csv`

Fonte: Vítimas e Dados de Ocorrência (VDE), Ministério da Justiça e Segurança Pública, planilha `bancovde-ANO.xlsx` (primeira aba), recortada para MS. O arquivo tem 103.172 linhas e 15 colunas, lidas como texto e com codificação UTF-8 com marca de ordem de bytes (c.137). Cada linha é um evento, um município e um mês. O VDE tem 31 tipos de evento; o trabalho usa só três séries (ver `SERIE_VDE` em A.8). O trabalho não usa um dicionário do VDE: as descrições vêm dos nomes das colunas e dos valores do arquivo.

| Variável | Descrição | Tipo | Valores ou códigos | Usada em | Origem da descrição |
|---|---|---|---|---|---|
| `ano_arquivo` | Ano da planilha de origem | inteiro (lido como texto) | 2016 a 2024 (renomeada `ANO` na limpeza) | 4b.5 (VDE-2), 7 | Elaborada neste trabalho |
| `uf` | Unidade da federação | código | `MS` em todas as linhas | Não usada na análise | Elaborada neste trabalho |
| `municipio` | Município da linha | texto | 80 valores: os 79 municípios de MS (em maiúsculas, com acento) e `NÃO INFORMADO` | 4b.5 (VDE-2, liga ao código IBGE), 7 | Elaborada neste trabalho |
| `evento` | Tipo de evento registrado | texto | 31 categorias (ex.: `Homicídio doloso`, `Suicídio`, `Apreensão de Cocaína`). Usadas: `Morte no trânsito ou em decorrência dele (exceto homicídio doloso)`, `Mortes no trânsito` e `Morte por intervenção de Agente do Estado` | 4b.5 (VDE-1) | Elaborada neste trabalho |
| `data_referencia` | Mês de referência da linha | data (`aaaa-mm-dd hh:mm:ss`) | Sempre o primeiro dia do mês, de 2016-01-01 a 2024-12-01 (108 meses) | 4b.5 (VDE-2) | Elaborada neste trabalho |
| `agente` | Categoria do agente do Estado, nos eventos de morte ou suicídio de agente | texto | Só tem valor em `Morte de Agente do Estado` e `Suicídio de Agente do Estado`: `Agente de Trânsito`, `Bombeiro Militar`, `Guarda Municipal`, `PF`, `PRF`, `Polícia Civil`, `Polícia Militar`, `Polícia Penal`, `Profissionais de Perícia` | Não usada na análise | Elaborada neste trabalho |
| `arma` | Tipo de arma, no evento de arma de fogo apreendida | texto | Só tem valor em `Arma de Fogo Apreendida`: `Carabina`, `Espingarda`, `Fuzil`, `Metralhadora`, `Outra`, `Pistola`, `Revolver`, `Rifle`, `Submetralhadora` | Não usada na análise | Elaborada neste trabalho |
| `faixa_etaria` | Faixa etária, nos eventos de pessoa desaparecida ou localizada | texto | Só tem valor em `Pessoa Desaparecida` e `Pessoa Localizada`: `Menor de Idade`, `Maior de Idade`, `Idade Não Informada` | Não usada na análise | Elaborada neste trabalho |
| `feminino` | Vítimas do sexo feminino | inteiro | De 0 a 320; vazia nos eventos que não contam vítimas e em parte das linhas de alguns eventos | Não usada na análise | Elaborada neste trabalho |
| `masculino` | Vítimas do sexo masculino | inteiro | De 0 a 145; vazia nos eventos que não contam vítimas e em parte das linhas de alguns eventos | Não usada na análise | Elaborada neste trabalho |
| `nao_informado` | Vítimas sem sexo informado | inteiro | De 0 a 152; vazia nos eventos que não contam vítimas e em parte das linhas de alguns eventos | Não usada na análise | Elaborada neste trabalho |
| `total_vitima` | Total de vítimas da linha | inteiro (vira `TOTAL_VITIMA`) | De 0 a 365; vazia nos eventos que não contam vítimas | 4b.5 (VDE-2), 7.2, 7.3, 7.5 | Elaborada neste trabalho |
| `total` | Total do evento nos eventos que não contam vítimas (ex.: mandados cumpridos, armas apreendidas) | inteiro | De 0 a 12.797; a unidade de contagem de cada evento não está documentada na fonte | Não usada na análise | Elaborada neste trabalho |
| `total_peso` | Peso apreendido nos eventos `Apreensão de Cocaína` e `Apreensão de Maconha` | decimal (ponto decimal) | De 1,04 a 130.972,35; a unidade de medida não está documentada na fonte | Não usada na análise | Elaborada neste trabalho |
| `abrangencia` | Instituição que registra o evento | texto | `Estadual` (91.152), `Polícia Rodoviária Federal` (8.964), `Polícia Federal` (3.056) | 4b.5 (VDE-1) | Elaborada neste trabalho |

---

## A.5 IBGE: população e municípios

### `ibge_populacao_ms_sidra.csv`

Fonte: IBGE, SIDRA (estimativas, tabela 6579; Censo 2000 e 2010, tabela 202; Censo 2022, tabela 4709). O arquivo tem 1.960 linhas de dados e 4 colunas, e traz só o que o IBGE publicou: de 2000 a 2026, sem 2007 e sem 2023 (c.22).

| Variável | Descrição | Tipo | Valores ou códigos | Usada em | Origem da descrição |
|---|---|---|---|---|---|
| `municipio_ibge` | Município | código | Código IBGE de 7 dígitos (o 7º é verificador); 79 municípios | 3, 4b.3 (IBGE-1, IBGE-2) | IBGE, SIDRA (sem página); a regra do 7º dígito é descrita no notebook (c.112) |
| `ano` | Ano da população | inteiro | 2000 a 2026, sem 2007 e sem 2023 | 3, 4b.3 (IBGE-2) | Elaborada neste trabalho |
| `populacao` | População residente do município no ano | inteiro | De 1.873 a 970.843 | 3, 4b.3 (IBGE-2), 8.3, 9 | IBGE, SIDRA (sem página) |
| `fonte` | Tabela do SIDRA de onde veio a linha | texto | `SIDRA 6579 (estimativa)` (1.726 linhas); `SIDRA 202 (Censo 2000/2010)` (155); `SIDRA 4709 (Censo 2022)` (79) | 3 | Elaborada neste trabalho |

### `municipios_ms.json`

Fonte: IBGE, serviço de localidades (`/estados/50/municipios`). Lista de 79 objetos, um por município (c.20). Campos de cada objeto:

| Campo | Descrição | Tipo | Valores ou códigos | Usada em | Origem da descrição |
|---|---|---|---|---|---|
| `id` | Código do município | código | 7 dígitos (o 7º é verificador); de 5000203 a 5008404 | 3, 4b.3 (IBGE-1) | IBGE, localidades (sem página); regra do 7º dígito no notebook (c.112) |
| `nome` | Nome do município, com acento | texto | 79 nomes (ex.: `Água Clara`) | 3, 4b.3 (IBGE-1) | IBGE, localidades (sem página) |
| `microrregiao` (`id`, `nome` e `mesorregiao` com `id`, `nome` e `UF`) | Microrregião e mesorregião do município, e a UF dentro delas | objeto aninhado (código e texto) | Ex.: `Três Lagoas`; `Leste de Mato Grosso do Sul`; UF `MS` | Não usada na análise | Elaborada neste trabalho (pelo nome do campo) |
| `regiao-imediata` (`id`, `nome` e `regiao-intermediaria` com `id`, `nome` e `UF`) | Região geográfica imediata e intermediária do município | objeto aninhado (código e texto) | Ex.: `Três Lagoas`; intermediária `Campo Grande` | Não usada na análise | Elaborada neste trabalho (pelo nome do campo) |

---

## A.6 Região de saúde (DATASUS): `ref_regiao_saude/`

Fonte: tabelas territoriais do DATASUS, base territorial de 06/2026 (`ref_regiao_saude/FONTE.txt`). Os dois arquivos foram extraídos sem alteração. Os arquivos não vêm com dicionário no pacote: as descrições vêm dos nomes e dos valores.

### `rl_municip_regsaud.csv` (5.572 linhas, separador `;`)

| Variável | Descrição | Tipo | Valores ou códigos | Usada em | Origem da descrição |
|---|---|---|---|---|---|
| `CO_MUNICIP` | Município | código | Código IBGE de 6 dígitos; 5.572 municípios do Brasil; os de MS começam com `50` (79) | 4b.6 (REGIAO-1; vira `COD_MUN`) | Elaborada neste trabalho |
| `CO_REGSAUD` | Região de saúde do município | código | 5 dígitos; 439 regiões distintas na tabela | 4b.6 (REGIAO-1; vira `COD_REGIAO_SAUDE`), 10.1 | Elaborada neste trabalho |

### `tb_regsaud.csv` (466 linhas, separador `,`)

| Variável | Descrição | Tipo | Valores ou códigos | Usada em | Origem da descrição |
|---|---|---|---|---|---|
| `CO_REGSAUD` | Código da região de saúde | código | 5 dígitos; 466 valores distintos | 4b.6 (REGIAO-1, chave da junção) | Elaborada neste trabalho |
| `CO_STATUS` | Situação do registro | código | `S` em todas as linhas; significado não documentado na fonte | Não usada na análise | Elaborada neste trabalho; significado não documentado na fonte |
| `DS_NOME` | Nome da região de saúde | texto | 466 nomes distintos (ex.: `Vale do Jamari - RO`); vira `REGIAO_SAUDE` | 4b.6 (REGIAO-1), 9.5 | Elaborada neste trabalho |
| `DS_NOMEPAD` | Nome da região de saúde padronizado | texto | O mesmo nome, em maiúsculas e sem acento (ex.: `VALE DO JAMARI - RO`) | Não usada na análise | Elaborada neste trabalho (pelos valores) |
| `DS_ABREV` | Nome da região de saúde em outra grafia | texto | O mesmo nome, sem acento e com cada palavra iniciada em maiúscula (ex.: `Vale Do Jamari - RO`); sentido de "abreviado" não documentado na fonte | Não usada na análise | Elaborada neste trabalho (pelos valores) |
| `NU_ORDEM` | Número de ordem (pelo nome da coluna) | código | `S` em todas as linhas; significado não documentado na fonte | Não usada na análise | Elaborada neste trabalho; significado não documentado na fonte |

---

## A.7 SIGO: `regioes_municipios.json` e `snapshot-2026-11-15/`

Fonte: Sistema Integrado de Gestão Operacional (SIGO), SEJUSP-MS, painel público de estatísticas. Não há arquivo para baixar: o trabalho guardou 346 respostas JSON da API do painel (consulta de 15/11/2026) e a lista de municípios do painel. Os JSON não têm dicionário publicado: as descrições vêm da estrutura das respostas e dos valores. O nome de cada arquivo tem o formato `searchEstatisticas{Vitimas|Ocorrencias|CVLI}_t{tipo}_a{período}_{estado|munID}.json`. Tipos de crime (c.251): 1 Homicídio doloso; 2 Latrocínio; 3 Lesão corporal seguida de morte; 4 Tentativa de homicídio; 5 Feminicídio; 6 Morte por intervenção legal; 7 Morte de causa indeterminada; 8 Morte no trânsito; 10 Suicídio; 29 CVLI (no notebook, o rótulo do tipo 29 é "CVLI (vítimas)"; o arquivo `CVLI` do tipo 29 traz ocorrências).

### `regioes_municipios.json`

| Campo | Descrição | Tipo | Valores ou códigos | Usada em | Origem da descrição |
|---|---|---|---|---|---|
| `municipios[].id_municipio` | Código do município no painel do SIGO (não é o código do IBGE) | código | 79 valores, de `4103` a `4265` (aparecem no nome dos arquivos como `munID`) | 7.1 | Elaborada neste trabalho |
| `municipios[].nm_municipio` | Nome do município, sem acento | texto | 79 nomes (ex.: `Agua Clara`); ligados ao IBGE pelo nome normalizado | 7.1 | Elaborada neste trabalho |
| `municipios[].ordem` | Número de ordem | texto | `0` em todos os municípios; significado não documentado na fonte | Não usada na análise | Elaborada neste trabalho; significado não documentado na fonte |
| `regioes[].id_regiao_municipio` e `regioes[].nm_regiao_municipio` | Agrupamentos de municípios do painel | código e texto | código 6 `Capital`; 4 `Estado`; 1 `Faixa de Fronteira`; 5 `Interior`. A lista de municípios de cada agrupamento não está no arquivo | Não usada na análise | Elaborada neste trabalho |

### Respostas JSON de `snapshot-2026-11-15/`

| Campo | Descrição | Tipo | Valores ou códigos | Usada em | Origem da descrição |
|---|---|---|---|---|---|
| `items.anual.labels` | Anos da série | texto | Anos consultados (ex.: `2016` a `2026`) | 7.1 (`serie_anual_sigo`) | Elaborada neste trabalho |
| `items.anual.dados` | Valor da série em cada ano de `labels`: vítimas (arquivos `Vitimas`), ocorrências (`Ocorrencias`) ou ocorrências de CVLI (`CVLI`, que conta ocorrências; as vítimas de CVLI estão nos arquivos `Vitimas` do tipo 29) | inteiro | Número de casos por ano | 7.1 a 7.5 | Elaborada neste trabalho |
| `items.mensal.datasets[0].data` | Valores mês a mês (janeiro a dezembro) do ano consultado | inteiro | 12 valores por ano | 7.6 (arquivos de intervenção legal, tipo 6, por ano) | Elaborada neste trabalho |
| `total`, `items.mensal.labels`, `items.mensal.defaultLabels`, `items.mensal.dados`, `items.anual.defaultLabels`, `items.anual.colors` | Campos de apresentação do painel (totais, rótulos, cores) | texto e inteiro | Sem uso nas tabelas do trabalho; significado de `total` e de `mensal.dados` não documentado na fonte | Não usada na análise | Elaborada neste trabalho; significado não documentado na fonte |
| `items.sexo` e `items.faixaEtaria` | Vítimas por sexo e por faixa etária (nos arquivos de `Vitimas`) | texto e inteiro | Sexo: `Masculino`, `Feminino`, `Não informado`. Faixa: `Criança`, `Adolescente`, `Jovem`, `Adulto`, `Idoso`, `Não informado` (os limites de idade de cada faixa não estão documentados na fonte) | Não usada na análise | Elaborada neste trabalho |
| `items.totalOcorrencias` (`ID_ITEM`, `ITEM`, `total`) e `items.tipoCrime` | Tipo de crime consultado e seu total no período | código e texto | Ex.: `ID_ITEM` 8, `ITEM` `Morte no Trânsito` | Não usada na análise | Elaborada neste trabalho |

---

## A.8 Variáveis criadas no notebook

Todas são **elaboradas neste trabalho**. A coluna "Célula" diz onde a variável nasce (`c.NNN`, contando do 0). As variáveis do SIM ficam na tabela `sim`, as das vítimas na tabela `vitimas` (óbitos de trânsito e agressão com ocorrência em MS, 2016–2024), e as dos municípios na tabela `V2` (79 linhas, uma por município).

### A.8.1 SIM (tabela `sim`) e vítimas (tabela `vitimas`)

| Variável | Descrição | Como é calculada | Valores | Célula | Origem |
|---|---|---|---|---|---|
| `RACA_COR_ROTULO` | Raça/cor por extenso | Troca o código de `RACACOR` pelo rótulo; vazio e 9 viram "sem informação" | Branca, Preta, Amarela, Parda, Indígena, sem informação | c.61 | Elaborada neste trabalho |
| `ESTADO_CIVIL_ROTULO` | Estado civil por extenso | Troca o código de `ESTCIV` pelo rótulo; vazio e 9 viram "sem informação" | Solteiro, Casado, Viúvo, Separado judicialmente/divorciado, União estável, sem informação | c.61 | Elaborada neste trabalho |
| `ESC2010_ROTULO` | Escolaridade por extenso | Troca o código de `ESC2010` pelo rótulo; vazio e 9 viram "sem informação" | Sem escolaridade, Fundamental I, Fundamental II, Médio, Superior incompleto, Superior completo, sem informação | c.61 | Elaborada neste trabalho |
| `SEXO_ROTULO` | Sexo por extenso | Troca o código de `SEXO` pelo rótulo; vazio, 0 e 9 viram "sem informação" | Masculino, Feminino, sem informação | c.65 | Elaborada neste trabalho |
| `IDADE_ANOS` | Idade em anos | Lê `IDADE`: unidade 4 = os 2 últimos dígitos; unidade 5 = 100 mais os 2 últimos; vazio ou unidade 9 = vazio; qualquer outro valor = 0 (menos de 1 ano) | Número de 0 a 199, ou vazio | c.69 | Elaborada neste trabalho |
| `FAIXA_ETARIA` | Faixa etária | Agrupa `IDADE_ANOS`; idade vazia vira "sem informação" | 0–14, 15–19, 20–29, 30–39, 40–49, 50–59, 60+, sem informação | c.69 | Elaborada neste trabalho |
| `OCUP_ROTULO` | Tipo da ocupação | Códigos especiais de `OCUP` recebem o rótulo do `CBO2002.CNV`; vazio e 998999 viram "sem informação"; os demais são "ocupação CBO" | ocupação CBO, Estudante (999991), Dona de casa (999992), Aposentado/Pensionista (999993), "Desempregado cronico ou cuja habitação habitual" (999994, texto truncado na fonte), Presidiário (999995), sem informação | c.73 | Elaborada neste trabalho |
| `CLASSE_RENDA` (na tabela `sim`) | Classe de renda da vítima | Para a vítima, procura a classe da ocupação (`OCUP`) no ano da morte na tabela da RAIS (`tabela_rais`); se a ocupação não existe naquele ano, usa o ano mais próximo (empate: o anterior). Quem não é vítima fica vazio | `baixa`, `média`, `alta`, `sem_dado` (ocupação sem vínculos suficientes, nem na família), `sem_casamento` (ocupação ausente da RAIS), `nao_classificavel` (ocupação vazia, especial ou fora do formato); vazio = não é vítima | c.109 | Elaborada neste trabalho |
| `ANO_RAIS_USADO` | Ano da RAIS de onde veio a classe de renda | Ano da morte, ou o ano mais próximo quando a ocupação não existe no ano da morte | Ano em texto (2016 a 2024), ou vazio | c.109 | Elaborada neste trabalho |
| `USOU_ANO_PROXIMO` | Marca se a classe veio de outro ano da RAIS | Verdadeiro quando a ocupação não existia no ano da morte | Verdadeiro ou falso | c.109 | Elaborada neste trabalho |
| `CATEGORIA` | Categoria da causa de morte | Classifica `CAUSA_CID` pelas três primeiras posições da CID-10 | `transito` (V01–V89), `transporte_outros` (V90–V99), `agressao` (X85–Y09), `indeterminada` (Y10–Y34), `intervencao_legal` (Y35–Y36), `outra_causa` | c.157 | Elaborada neste trabalho |
| `CID_3` | Causa básica em 3 caracteres | Os 3 primeiros caracteres de `CAUSA_CID` | Ex.: `V89`, `X95`, `Y09` | c.157 | Elaborada neste trabalho |
| `MORTE_EM_MS` | Óbito ocorrido em MS | Verdadeiro quando `MUN_MORTE` começa com `50` | Verdadeiro ou falso (168.341 verdadeiros) | c.159 | Elaborada neste trabalho |
| `MORADIA_EM_MS` | Óbito de residente em MS | Verdadeiro quando `MUN_MORADIA` começa com `50` | Verdadeiro ou falso (170.031 verdadeiros) | c.159 | Elaborada neste trabalho |
| `ANO_OBITO` | Ano do óbito | Ano de `DATA_OBITO` (já com o zero à esquerda corrigido) | 2016 a 2024 | c.161 | Elaborada neste trabalho |
| `MES_OBITO` | Mês do óbito | Mês de `DATA_OBITO` | 1 a 12 | c.161 | Elaborada neste trabalho |
| `VIA_PUBLICA` | Óbito em via pública | Verdadeiro quando `LOC_MORTE` é 4 | Verdadeiro ou falso (7.377 verdadeiros) | c.161 | Elaborada neste trabalho |
| `GRUPO_VITIMA` | Grupo da vítima (tabela `vitimas`) | `CATEGORIA` trânsito ou agressão, com o rótulo em português | `trânsito`, `agressão` | c.203 | Elaborada neste trabalho |
| `OCUPACAO_GRUPO` | Grande grupo da ocupação (tabela `vitimas`) | Primeiro dígito da `OCUP` quando `OCUP_ROTULO` é "ocupação CBO"; nos demais casos, o próprio `OCUP_ROTULO` | Grandes grupos 0 a 9 da CBO (7 e 8 têm o mesmo rótulo no notebook), Estudante, Dona de casa, Aposentado/Pensionista, Desempregado, Presidiário, sem informação | c.215 | Elaborada neste trabalho |
| `CLASSE_ROTULO` | Classe de renda por extenso (tabela `vitimas`) | Troca o código de `CLASSE_RENDA` pelo rótulo | baixa, média, alta, ocupação sem dado na RAIS, ocupação não encontrada na RAIS, sem informação | c.219 | Elaborada neste trabalho |
| `MEIO_AGRESSAO` | Meio da agressão (dicionário, não vira coluna) | Liga `CID_3` das agressões ao meio | X93, X94 e X95 arma de fogo; X99 cortante; Y00 contundente; X91 enforcamento; Y04 força corporal; Y09 não especificado; demais = demais meios | c.191 | Elaborada neste trabalho |
| `VITIMA_TRANSITO` | Quem morre no trânsito (dicionário, não vira coluna) | Liga os 2 primeiros caracteres de `CID_3` das mortes de trânsito à vítima | V0 pedestre; V1 ciclista; V2 motociclista; V3 triciclo; V4 automóvel; V5 caminhonete; V6 pesado; V7 ônibus; V8 outros | c.195 | Elaborada neste trabalho |
| `MORADIA` (tabela `ocorridos_ms`) | Situação de moradia do óbito ocorrido em MS (trânsito e agressão) | Compara `MUN_MORADIA` com `MUN_MORTE`: iguais = mora no município; diferentes e `MORADIA_EM_MS` verdadeiro = outro município de MS; senão fora de MS | `mora no município`, `outro município de MS`, `fora de MS` | c.199 | Elaborada neste trabalho |
| `LOCAL` (tabela `ocorridos_ms`) | Local do óbito agrupado | `LOC_MORTE` 1 e 2 = estabelecimento de saúde; 4 via pública; 3 domicílio; 5 outros; 6 aldeia indígena; 9 e vazio = ignorado | `estabelecimento de saúde`, `via pública`, `domicílio`, `outros`, `aldeia indígena`, `ignorado` | c.199 | Elaborada neste trabalho |

### A.8.2 RAIS (tabelas `tabela_rais` e do log)

| Variável | Descrição | Como é calculada | Valores | Célula | Origem |
|---|---|---|---|---|---|
| `motivo_exclusao` | Motivo da exclusão do vínculo da RAIS | Marca cada vínculo, na ordem das regras RAIS-1 a RAIS-4 | 0 mantido; 1 `cbo_0000-1`; 2 `cbo_nao_6_digitos`; 3 `cbo_000000`; 4 `cbo_999999`; 5 `rem_vazio_ou_ilegivel`; 6 `rem_zero_ou_negativo` | c.85 | Elaborada neste trabalho |
| `N_CBO` | Vínculos válidos da ocupação no ano | Conta os vínculos mantidos por ocupação (CBO de 6 dígitos) e ano | Inteiro | c.105 | Elaborada neste trabalho |
| `MEDIANA_CBO` | Remuneração mediana da ocupação no ano | Mediana de `REM_MEDIA_SM` por ocupação e ano | Decimal, em salários mínimos | c.105 | Elaborada neste trabalho |
| `FAMILIA` | Família da ocupação | Os 4 primeiros dígitos do CBO | Texto de 4 dígitos | c.105 | Elaborada neste trabalho |
| `N_FAMILIA` | Vínculos válidos da família no ano | Conta os vínculos mantidos por família e ano | Inteiro | c.105 | Elaborada neste trabalho |
| `MEDIANA_FAMILIA` | Remuneração mediana da família no ano | Mediana de `REM_MEDIA_SM` por família e ano | Decimal, em salários mínimos | c.105 | Elaborada neste trabalho |
| `NIVEL` | De onde vem a mediana usada | `cbo6` se a ocupação tem 10 vínculos ou mais; senão `familia4` se a família tem 10 ou mais; senão `sem_dado` | `cbo6`, `familia4`, `sem_dado` | c.105 | Elaborada neste trabalho |
| `MEDIANA` | Salário típico da ocupação no ano | `MEDIANA_CBO` quando `NIVEL` é `cbo6`; `MEDIANA_FAMILIA` quando é `familia4`; vazio quando é `sem_dado` | Decimal, em salários mínimos | c.105 | Elaborada neste trabalho |
| `CLASSE_RENDA` (na tabela `tabela_rais`) | Classe de renda da ocupação no ano | `baixa` até 2 salários mínimos; `média` acima de 2 até 6; `alta` acima de 6 | `baixa`, `média`, `alta`, ou vazio quando não há mediana | c.105 | Elaborada neste trabalho |

### A.8.3 Outras bases

| Variável | Descrição | Como é calculada | Valores | Célula | Origem |
|---|---|---|---|---|---|
| `COD_MUN` | Código de município de 6 dígitos (chave de ligação entre as bases) | Os 6 primeiros dígitos do código IBGE de 7 dígitos; nas bases que só trazem o nome (PRF, VDE), liga pelo nome normalizado | Texto de 6 dígitos; os de MS começam com `50` | c.113 | Elaborada neste trabalho |
| `MUNICIPIO_NORM` | Nome do município normalizado | Maiúsculas, sem acento e sem espaços nas pontas (`normalizar_nome`) | Ex.: `AGUA CLARA` | c.113 | Elaborada neste trabalho |
| `POPULACAO` | População do município no ano, de 2016 a 2024 | Linhas de 2016 a 2024 da tabela do IBGE; 2023 é a média entre o Censo 2022 e a estimativa de 2024, arredondada | Inteiro; 711 linhas (79 municípios × 9 anos) | c.117 | Elaborada neste trabalho |
| `FONTE_POP` | Origem de cada linha de população | Cópia da coluna `fonte` do IBGE; para 2023 recebe o texto da média | `SIDRA 6579 (estimativa)`, `SIDRA 4709 (Censo 2022)`, `média entre Censo 2022 e estimativa 2024` | c.117 | Elaborada neste trabalho |
| `COD_REGIAO_SAUDE` | Código da região de saúde do município | `CO_REGSAUD` dos 79 municípios de MS | Código de 5 dígitos | c.147 | Elaborada neste trabalho |
| `REGIAO_SAUDE` | Nome da região de saúde do município | `DS_NOME` ligado pelo código da região | Nome (ex.: `Sul Fronteira`) | c.147 | Elaborada neste trabalho |
| `DATA_ACIDENTE` | Data do acidente da PRF | Converte `data_inversa` (`dd/mm/aa` em 2016 e `aaaa-mm-dd` depois) | Data | c.129 | Elaborada neste trabalho |
| `MORTOS_PRF` | Mortos no acidente da PRF | `mortos` convertido para inteiro | Inteiro de 0 a 8 | c.133 | Elaborada neste trabalho |
| `ACIDENTES_PRF` | Acidentes da PRF por município e ano | Conta as linhas (`id`) por `COD_MUN` e `ANO` | Inteiro | c.231 | Elaborada neste trabalho |
| `EVENTO_NORM` | Evento do VDE normalizado | `evento` em maiúsculas e sem acento | Texto | c.137 | Elaborada neste trabalho |
| `ABRANGENCIA_NORM` | Abrangência do VDE normalizada | `abrangencia` em maiúsculas e sem acento | Texto | c.137 | Elaborada neste trabalho |
| `SERIE_VDE` | Série do VDE usada na análise | Casa o início do nome do evento com a abrangência | `transito_estadual` (8.640 linhas), `transito_prf` (8.640), `intervencao_estadual` (108); vazio = linha fora da análise | c.137 | Elaborada neste trabalho |
| `TOTAL_VITIMA` | Vítimas do VDE na linha | `total_vitima` convertido para inteiro | Inteiro, 0 ou mais | c.143 | Elaborada neste trabalho |
| `DATA_REFERENCIA` | Mês de referência do VDE | `data_referencia` convertida para data | Data (primeiro dia do mês) | c.143 | Elaborada neste trabalho |
| `SIGO_VITIMAS` | Vítimas de trânsito do SIGO, por município e ano | `items.anual` do JSON de vítimas, tipo 8, de cada município | Inteiro; 711 linhas | c.227 | Elaborada neste trabalho |
| `SIGO_OCORRENCIAS` | Ocorrências de trânsito do SIGO, por município e ano | `items.anual` do JSON de ocorrências, tipo 8 | Inteiro; 711 linhas | c.227 | Elaborada neste trabalho |
| `SIGO_CVLI_OCORRENCIAS` | Ocorrências de CVLI do SIGO, por município e ano (conta ocorrências, não vítimas) | `items.anual` do JSON `searchEstatisticasCVLI`, tipo 29, de cada município | Inteiro; 711 linhas | c.227 | Elaborada neste trabalho |
| `sigo_cvli_vitimas_estado` | Vítimas de CVLI do SIGO, por ano, no estado (só existe para o estado, não por município) | `items.anual` do JSON `searchEstatisticasVitimas`, tipo 29, do estado | Inteiro; 9 valores (2016 a 2024) | c.227 | Elaborada neste trabalho |
| `SIGO_INTERVENCAO` | Mortes por intervenção legal no SIGO, por município e ano | `items.anual` do JSON de vítimas, tipo 6 | Inteiro; 711 linhas | c.227 | Elaborada neste trabalho |

### A.8.4 Comparações, taxas, agrupamento e números pequenos

| Variável | Descrição | Como é calculada | Valores | Célula | Origem |
|---|---|---|---|---|---|
| `GRADE_OCORRENCIA` | Óbitos por município e ano | Conta os óbitos da categoria, com ocorrência em MS, por município de ocorrência e ano; um quadro de 79 × 9 por categoria. Célula sem óbito vale 0 | Inteiro, 0 ou mais | c.165 | Elaborada neste trabalho |
| `GRADE_RESIDENCIA` | Óbitos por município de residência e ano | Igual à anterior, pelo município de residência | Inteiro, 0 ou mais | c.165 | Elaborada neste trabalho |
| `tabelas_local` | Local do óbito por situação de moradia (5.9), trânsito e agressão | Uma linha por situação de moradia (3 linhas por categoria): `total`, contagem em cada local e `% ` de cada local na linha. Grava `sim_morte_fora_do_municipio_local.csv` (as duas categorias empilhadas, coluna `categoria`) | Inteiro e decimal; trânsito soma 5.868 e agressão 4.767 | c.199 | Elaborada neste trabalho |
| `resumo_local` | Moradores e não moradores por local do óbito (5.9) | Duas linhas por categoria (`moradores` e `não moradores`, que soma outro município de MS e fora de MS), com `total` e a contagem em cada local; base das conferências da 5.9 | Inteiro; trânsito 3.521 moradores e 2.347 não moradores | c.199 | Elaborada neste trabalho |
| `por_municipio` | Trânsito por município de ocorrência: moradores, não moradores e local dos não moradores (5.9) | Por `MUN_MORTE`: `ocorridos`, `moradores`, `não moradores`, não moradores em estabelecimento de saúde, em via pública e nos demais locais, e `%` dos não moradores em estabelecimento de saúde. Grava `sim_morte_fora_do_municipio_por_municipio.csv` com as tabelas `tres_municipios` (Dourados, Campo Grande, Três Lagoas) e `dez_mais_nao_moradores` (coluna `tabela`) | Inteiro e decimal; 79 municípios na tabela completa | c.199 | Elaborada neste trabalho |
| `serie_transito` | Série anual do trânsito por fonte | Uma coluna por fonte: SIM (ocorrência e residência), SIGO vítimas, VDE vítimas, SIGO ocorrências e mortos da PRF; mais "B comparável?" | Inteiro por ano; "B comparável?" = `NÃO COMPARÁVEL (2016–2017)` ou `sim` | c.235 | Elaborada neste trabalho |
| `razoes` | Razões das fontes sobre o SIM de trânsito | Cada fonte dividida pelo SIM de trânsito por ocorrência, ano a ano | Decimal | c.235 | Elaborada neste trabalho |
| `agressao_x_cvli` | Agressão do SIM × CVLI do SIGO | Colunas `SIM agressão (ocorrência)` e `SIM agressão (residência)`; `SIGO CVLI ocorrências` (soma dos 79 municípios); `SIGO CVLI vítimas (estado)`; e as razões `CVLI ocorrências / SIM` e `CVLI vítimas / SIM` (ambas sobre o SIM por ocorrência) | Inteiro por ano; razões decimais | c.245 | Elaborada neste trabalho |
| `intervencao_fontes` | Intervenção legal por fonte | Colunas SIM Y35–Y36, SIGO tipo 6, VDE, `VDE usado` (o VDE sem o ano de 2020), `SIM / SIGO` e `SIM / VDE` | Inteiro por ano; razões decimais | c.245 | Elaborada neste trabalho |
| `taxa_estadual` | Taxa estadual por 100 mil habitantes | Óbitos do ano na categoria ÷ população de MS no ano × 100.000 | Decimal, por categoria e ano | c.265 | Elaborada neste trabalho |
| `pessoas_ano` | Pessoas-ano do município, 2016–2024 | Soma da população do município nos 9 anos | Inteiro, por município | c.265 | Elaborada neste trabalho |
| `taxa_municipal` | Taxa municipal do período por 100 mil habitantes | Óbitos de 2016 a 2024 ÷ `pessoas_ano` × 100.000 | Decimal, por município e categoria | c.265 | Elaborada neste trabalho |
| `POP_2022` | População do município em 2022 (Censo) | `POPULACAO` de 2022 | Inteiro | c.275 | Elaborada neste trabalho |
| `PESSOAS_ANO` | Pessoas-ano do município (tabela `V2`) | O mesmo valor de `pessoas_ano` | Inteiro | c.275 | Elaborada neste trabalho |
| `OBITOS_TRANSITO` e `OBITOS_AGRESSAO` | Óbitos do período, por município | Soma de `GRADE_OCORRENCIA` nos 9 anos (trânsito e agressão) | Inteiro | c.275 | Elaborada neste trabalho |
| `TAXA_BRUTA_TRANSITO` e `TAXA_BRUTA_AGRESSAO` | Taxa bruta do período, por 100 mil | Óbitos ÷ pessoas-ano × 100.000 (`r_i = d_i / n_i`) | Decimal | c.275 | Elaborada neste trabalho |
| `TAXA_SUAV_TRANSITO` e `TAXA_SUAV_AGRESSAO` | Taxa suavizada por Bayes empírico, por 100 mil | `m + w_i (r_i − m)`, em que `m` é a taxa do estado e `w_i` o peso do município; a taxa encolhe para a do estado quando a população é pequena | Decimal | c.275 | Elaborada neste trabalho |
| `PESO_TRANSITO` e `PESO_AGRESSAO` | Peso `w_i` do Bayes empírico | `s² / (s² + m / n_i)`, com `s²` (variância entre municípios) valendo 0 se der negativo | Decimal de 0 a 1 | c.275 | Elaborada neste trabalho |
| `DIF_TRANSITO` e `DIF_AGRESSAO` | Quanto a suavização mudou a taxa | Taxa suavizada − taxa bruta | Decimal, positivo ou negativo | c.275 | Elaborada neste trabalho |
| `Z` | Taxas suavizadas padronizadas (escore z) | `(X − média) / desvio padrão`, para as duas taxas suavizadas | Decimal, 79 linhas × 2 colunas | c.281 | Elaborada neste trabalho |
| `GRUPO` | Grupo do município no agrupamento principal (k = 3) | k-means sobre `Z`, com rótulos dados por regra | `H1`, `H2`, `H3` | c.287 | Elaborada neste trabalho |
| `ROTULO_GRUPO` | Nome do grupo | H1 = agressão alta; H2 = trânsito alto; H3 = baixo nas duas | `agressão alta`, `trânsito alto`, `baixo nas duas` | c.287 | Elaborada neste trabalho |
| `SILHUETA` | Silhueta do município no agrupamento | Silhueta de cada município no k-means com k = 3 | Decimal de −1 a 1 | c.287 | Elaborada neste trabalho |
| `GRUPO_K2` | Grupo do município no agrupamento de conferência (k = 2) | k-means com k = 2; G1 é o grupo de maiores taxas padronizadas | `G1`, `G2` | c.293 | Elaborada neste trabalho |
| `PORTE` | Porte do município | Faixa de `POP_2022` | `até 20 mil`, `20–50 mil`, `50–100 mil`, `mais de 100 mil` | c.297 | Elaborada neste trabalho |
| `REGIAO_SAUDE` (na tabela `V2`) | Região de saúde do município | Copia a região de saúde de cada município | Nome da região | c.297 | Elaborada neste trabalho |
| `BLOCOS` | Blocos de 3 anos | Agrupa os anos em três blocos | `2016–18`, `2019–21`, `2022–24` | c.301 | Elaborada neste trabalho |
| `codigo_regiao` | Região de saúde de cada município, para somar óbitos | `COD_REGIAO_SAUDE` dos 79 municípios | Código de 5 dígitos | c.301 | Elaborada neste trabalho |
| `n_0`, `n_1a4`, `n_5a9`, `n_ge10` | Células com 0, 1 a 4, 5 a 9 e 10 ou mais óbitos | Conta as células de cada tabela (município × ano, município × bloco e região de saúde); as colunas `pct_...` trazem as porcentagens | Inteiro | c.301 | Elaborada neste trabalho |

---

## A.9 Arquivos de controle da entrega

### `MANIFESTO.csv` (358 linhas, separador `;`)

Lista os 358 outros arquivos do `dados.zip`, com o `sha256` de cada um. A primeira célula de código (c.1) confere os 358, um por um (descrição no `c.0` e em c.16).

| Variável | Descrição | Tipo | Valores ou códigos | Usada em | Origem da descrição |
|---|---|---|---|---|---|
| `arquivo` | Caminho do arquivo dentro de `dados/` | texto | 358 caminhos distintos | c.1, 2 | Elaborada neste trabalho |
| `linhas` | Linhas do arquivo, contando o cabeçalho | inteiro | `0` para os arquivos JSON (e 347 para o `manifesto.csv` do SIGO) | 2 | Elaborada neste trabalho |
| `bytes` | Tamanho do arquivo | inteiro | De 438 a 284.410.156 | c.1, 2 | Elaborada neste trabalho |
| `sha256` | Soma de verificação do arquivo | texto | 64 caracteres hexadecimais | c.1, 2 | Elaborada neste trabalho |

### `snapshot-2026-11-15/manifesto.csv` (346 linhas, separador `,`)

Registra cada consulta feita à API do SIGO (c.17 e c.18).

| Variável | Descrição | Tipo | Valores ou códigos | Usada em | Origem da descrição |
|---|---|---|---|---|---|
| `arquivo` | Nome do JSON guardado | texto | 346 nomes distintos | 2 | Elaborada neste trabalho |
| `endpoint` | Endereço da API consultado | texto | `https://estatistica.sigo.ms.gov.br/api/v2/action.php` em todas as linhas | Não usada na análise | Elaborada neste trabalho |
| `parametros` | Parâmetros da consulta | texto | Ex.: `_method=searchEstatisticasVitimas; tipo_crime=8; ano=2016-2026; municipio=estado(sem filtro)` | Não usada na análise | Elaborada neste trabalho |
| `data_hora_consulta` | Data e hora da consulta | data e hora (fuso -04:00) | De 2026-11-15T20:08:14 a 2026-11-15T20:16:14 | 2 | Elaborada neste trabalho |
| `status_http` | Resposta HTTP da consulta | código | `200` em todas as linhas | 2 | Elaborada neste trabalho |
| `bytes` | Tamanho do JSON | inteiro | De 1.294 a 4.880 | 2 | Elaborada neste trabalho |
| `sha256` | Soma de verificação do JSON | texto | 64 caracteres hexadecimais | 2 | Elaborada neste trabalho |
