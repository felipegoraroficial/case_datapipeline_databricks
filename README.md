# Steam - Databricks Pipeline - Google Cloud


## Introdução: 
Neste projeto pessoal, utilizo o Databricks na Google Cloud Platform (GCP). Reconheci a necessidade de incorporar a ferramenta Databricks na minha rotina de trabalho diária e, desde janeiro de 2024, comecei a praticar no ambiente Databricks para lidar com grandes volumes de dados. Além disso, o Databricks me permite integrar scripts com um sistema de controle de versão Git, facilita a administração e a integração de novos usuários no ambiente e possibilita a escalabilidade rápida do cluster conforme necessário.

Uma estratégia interessante que incorporei a este projeto foi armazenar os dados extraídos na pasta "raw" do datalake (bucket) no formato JSON, com o nome do arquivo correspondente à data da extração. Isso é feito em vez de sobrescrever dados antigos com novos dados e, ao final, em vez de adicionar registros à tabela dentro do data warehouse, trato os duplicados, mantendo apenas os valores mais recentes. Acredito que essa abordagem economiza custos ao evitar a sobrecarga do data warehouse com informações duplicadas.

![Steam](https://github.com/felipegoraroficial/projetos/assets/138418925/4405a38f-f516-4420-adbc-d506dab94a28)

## Extração de Dados:
O coração do projeto é a extração diária de detalhes sobre jogos, DLCs e outros conteúdos diretamente da API do Steam, assim como dados específicos do meu perfil de usuário, como o tempo gasto em cada jogo. Essas informações são coletadas no formato JSON e armazenadas na pasta 'raw' de um bucket, organizadas pela data da extração.

## Unificação e Filtragem:
Após a coleta, os arquivos JSON são agrupados e unificados. Nesse processo, seleciono as informações relevantes que desejo analisar e as salvo novamente em um arquivo JSON estruturado na pasta 'bronze' do bucket.

## Transformação e Limpeza:
Usando PySpark, transformo esses dados unificados em um dataframe, onde realizo uma série de tratamentos para garantir a qualidade dos dados. Isso inclui a limpeza de valores nulos, definição de esquemas, expansão de colunas aninhadas e conversão de preços de libras para reais. O resultado final é um dataframe limpo e estruturado, salvo em formato CSV na pasta 'silver'.

## Duplicação e Armazenamento Final:
A etapa final envolve a filtragem do dataframe para remover duplicatas, mantendo apenas os registros mais recentes com base no ID. Os dados são então armazenados em formato Delta Lake na pasta 'gold' do bucket e também carregados no Databricks Hive Metastore.

![steam games](https://github.com/felipegoraroficial/projetos/assets/138418925/78dc98f7-0854-478f-9610-5cbe2bb43c7b)

## Automação e Monitoramento:
Para garantir que esse processo ocorra diariamente sem falhas, configurei fluxos de trabalho no Databricks que seguem os passos mencionados acima. Além disso, criei alertas por e-mail automatizados para notificar sobre a conclusão dos fluxos de trabalho, qualquer atraso ou falhas na execução.

![steam_game](https://github.com/felipegoraroficial/projetos/assets/138418925/9f0463af-a9ab-47fa-8cbb-72abc1a75877)
![steam_user](https://github.com/felipegoraroficial/projetos/assets/138418925/2fedb2f4-7e59-4efd-b684-6745aebf0c67)

![notifi](https://github.com/felipegoraroficial/projetos/assets/138418925/b980fda3-a63a-4a62-9f16-f1fc008fb43f)  ![trigger](https://github.com/felipegoraroficial/projetos/assets/138418925/49df47a1-bc7a-469c-8ed1-7c1fe8d05ff2) ![computer](https://github.com/felipegoraroficial/projetos/assets/138418925/dcc79ce8-857b-4964-8bd7-cc68fc6cde7e)
