# Extrator de Cenários de Teste do Robot Framework

##  Visão Geral

Este script Python foi projetado para automatizar a documentação e análise de suítes de teste do Robot Framework. Ele varre um diretório especificado em busca de arquivos `.robot`, extrai informações detalhadas sobre cada cenário de teste — incluindo nome, documentação e tags — e exporta esses dados para um arquivo Excel (`.xlsx`) multifolha.

O objetivo é fornecer uma visão clara e organizada de toda a base de testes, facilitando a análise de cobertura, o planejamento e a geração de relatórios.

## Funcionalidades

- **Extração Automática**: Varre recursivamente um diretório para encontrar todos os arquivos de teste `.robot`.
- **Análise Detalhada**: Para cada cenário, extrai o nome, a documentação (docstring) e todas as tags associadas.
- **Relatório em Excel**: Gera um arquivo `.xlsx` com três abas para uma análise completa:
    1.  **Cenários de Testes**: Lista detalhada de todos os testes, com cada tag separada em sua própria coluna para facilitar a filtragem.
    2.  **Resumo**: Uma visão geral que mostra a quantidade de cenários por arquivo `.robot`, com um total geral.
    3.  **Tags**: Um resumo de todas as tags utilizadas no projeto, com a contagem de quantas vezes cada uma aparece, ordenado pela mais comum.
- **Flexibilidade**: Utiliza argumentos de linha de comando para especificar os diretórios de entrada e saída, permitindo que o script seja facilmente integrado em pipelines de CI/CD ou executado para diferentes projetos.

## Pré-requisitos

Antes de executar, certifique-se de ter o Python 3 instalado. Você também precisará instalar as bibliotecas Python necessárias.

1.  **Crie um arquivo** `requirements.txt` com o seguinte conteúdo:
    ```
    robotframework
    openpyxl
    ```

2.  **Instale as dependências** executando o comando abaixo no seu terminal:
    ```bash
    pip install -r requirements.txt
    ```

## Como Usar

O script é executado através da linha de comando, especificando o diretório dos testes a serem analisados e, opcionalmente, o diretório onde o relatório Excel será salvo.

### Sintaxe do Comando

```bash
python export_list_cenary.py --testinput <caminho_para_pasta_de_testes> [--outputdir <caminho_para_pasta_de_saida>]
```

### Argumentos de Linha de Comando

| Argumento     | Descrição                                                                                                  | Obrigatório | Padrão                                |
|---------------|------------------------------------------------------------------------------------------------------------|-------------|---------------------------------------|
| `--testinput` | O caminho para o diretório raiz que contém os arquivos de teste `.robot` a serem analisados.                 | **Sim** | N/A                                   |
| `--outputdir` | O caminho para o diretório onde o arquivo Excel gerado será salvo. Se não for fornecido, salva no diretório atual. | Não         | Diretório de execução do script (`.`) |

### Exemplos de Uso

- **Analisar uma pasta de testes `frontend` e salvar o relatório no diretório `reports`:**

  ```bash
  python export_list_cenary.py --testinput ./tests/frontend --outputdir ./reports
  ```
  *(Isso irá gerar um arquivo como `reports/cenarios_frontend.xlsx`)*

- **Analisar uma pasta de testes `api` e salvar o relatório no diretório atual:**

  ```bash
  python export_list_cenary.py --testinput ./tests/api
  ```
  *(Isso irá gerar um arquivo como `cenarios_api.xlsx`)*

## Estrutura do Relatório Excel

O arquivo Excel gerado (ex: `cenarios_testes.xlsx`) contém as seguintes abas:

1.  **Cenários de Testes**:
    - **Arquivo**: Nome do arquivo `.robot` de origem.
    - **Nome do Teste**: O nome do cenário de teste.
    - **Documentação**: O conteúdo da tag `[Documentation]` do cenário.
    - **Tag1, Tag2, ...**: As tags do cenário, cada uma em uma coluna separada.

2.  **Resumo**:
    - **Arquivo**: O nome de cada arquivo `.robot` processado.
    - **Quantidade de Testes**: O número total de cenários de teste encontrados em cada arquivo.
    - **TOTAL**: A soma de todos os testes encontrados.

3.  **Tags**:
    - **Tag**: O nome de cada tag única encontrada.
    - **Quantidade**: O número de vezes que a tag foi usada em todos os cenários.