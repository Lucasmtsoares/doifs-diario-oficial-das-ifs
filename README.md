# Projeto de iniciação científica PIBITI

## Trabalho desenvolvido a partir da necessidade de uma ferramenta de exploração e análise de portarias dos institutos federais de ensino. O presente descritivo do projeto tem por finalidade servir de guia para manutenção do código fonte e serviços externos cuja a ferramenta se coloca como usuária. 


Sumário

1. Visão geral (ex: tecnologias, período de desenvolvimento etc)
2. Instalação local em um editor de código (ex: vs code)
3. Estrutura de pastas
4. Interface gráfica
5. Banco de dados
6. Atualização
7. Considerações finais


## Visão geral

O projeto começou a ser desenvolvido em Setembro de 2023 e se estendeu até Setembro de 2024. A divisão foi entre front-end e back-end. Inicialmente foi desenvolvido o back-end. As etapas para construção do dessa parte foram:

1. Crawler - Coleta de dados
2. Scraping - Tratamento e limpeza de dados
3. Armazenamento - Salvar os dados em um banco de dados

Todas essas etapas foram feitas e se encontram funcionais, pelo menos na versão 1.0.

Quanto ao front-end, este não foi finalizado, apenas uma parte se encontra pronta, mas precisando de melhorias. Aperfeiçoamentos de design e exibição de dados precisam ser feitos. Infelizmente, algumas etapas demoraram mais do que o previsto e isso ocasionou na falta de tempo para realização das mesmas. As etapas do front-end, seriam: 

1. Construção da página home
2. Construção da página de resultados
3. Construção da página de exibição gráfica

Nas páginas de resultados e gráfica os dados exibidos são genéricos pois, o front-end e o back-end ainda não estão conectados. Esses dados são apenas para  testes. 

Os dados cujo sistema pretende coletar e armazenar são a partir de 2018 em diante, já que antes dessa data o Diário Oficial da União entregava os dados em um formato em que a coleta não seria totalmente funcional, pois o propósito é extrair os dados de páginas web, e antes era no formato de arquivo. 

Atualmente, o sistema tem todos os dados de 2018. A expectativa era contemplar o período de 2018 a 2024, e a partir disso fazer com que a alimentação do banco de dados fosse automatizada. Porém, houve alguns problemas na extração e o processo teve que ser realizados várias vezes, sem contar na demora considerável para a extração e tratamento dos dados. 


## Tecnologias

As tecnologias usadas para produção da ferramenta foram:

1. Flask - microframework python
2. Selenium - framework de automatização de tarefas
3. BeautifulSoup - biblioteca para raspagem de dados
4. Regex - biblioteca para reconhecimento de caracteres
5. Outras - também houve o uso de outra stacks


## Instalação

Para instalar o projeto e edita-lo, siga os passo:

1. Clone o projeto
2. Abra em algum editor de texto (ex: vs code)
3. Vá para a pasta raiz
4. Comandos válidos para Windows!!
5. Crie um ambiente virtual via terminal: python -m venv venv
6. Ative o ambiente virtual via terminal: venv\Scripts\activate
7. Instale as dependências com: pip install -r requirements.txt
8. Inicialização: python run.py runserver
9. Abra em um navegador: 127.0.0.1



## Estrutura de pastas

O projeto está organizado com base nos requisitos de hierarquia do Flask.

DOIFS: Pasta raiz é a pasta que contém todos os arquivos e subpastas da aplicação. Essa pasta é dividida entre a subpasta com o código principal e arquivos de configuração.

1. ChromeDriver: executável separado que o Selenium WebDriver usa para controlar o Chrome
2. .gitignore: arquivos a serem ignorados
3. Config.py: configurações básicas como senha e altenticação sobre o banco de dados
4. Readme: descrição do projeto
5. Requirements.txt: dependências do projeto
6. Run.py: arquivo de inicialização do projeto
7. Update.py: arquivo de atualização da basa de dados

APP: Pasta principal da aplicação

1. Controllers:pasta de roteamento da aplicação
    1. Default.py: arquivo de rotas
2. Core: pasta da lógica de negócio da aplicação
    1. Crawler.py: bot de extração de URLs
    2. Scraping: responsável pela raspagem de dados para cada URL
3. Models: pasta de classes
    1. Connection.py: conexão com o banco de dados
    2. Map.py: Mapa de entidades de período e institutos federais
    3. Publication.py: classe de publicação/materia
4. Service: pasta de banco de dados
    1. Database: lógica do banco de dados
        1. publicationDAO.py: funções CRUD do banco de dados
    2. Update: lógica de atualização 
        1. update.py: lógica de atualização do banco de dados
5. Static: pasta de arquivos CSS e assets
    1. Assets: arquivos visuais (ex: imagens)
    2. CSS: Estilização de páginas
    3. JS: arquivo de lógica de interatividade
        1. graphic.js: gráfico de visualização temporal de portarias
        2. modal.js: modal que apresenta um formulário 
6. Templates: pasta de arquivos HTML
    1. Basic.html: página home
    2. Page_de_busca.html: página de busca e apresentação de resultados
    3. Painel_de_analise.html:página de seleção de entidades para apresentação estatística
    4. Painel_grafico.html: página de apresentação estatística temporal


## Interface gráfica

A interface gráfica infelizmente não está finalizada. Contudo, há bastante progresso e cerca de 60% esteja pronto. A maior parte do que resta a se fazer são ajustes visuais e criação/edição de componentes e cards de apresentação de resultados e estatísticas. 


## Banco de dados

O banco de dados escolhido para armazenar as informações da aplicação foi o MongoDB, banco de dados NOSQL. Os dados estão armazenados no MongoDB Atlas, que oferece armazenamento gratuito na nuvem. A ideia era que ao colocar o sistema em produção fosse comprado um plano de hospedagem a fim de obter mais recursos da plataforma de armazenamento. 

Atualmente, há o armazenamento de todos os dados referentes ao ano de 2018. Todavia, é possível que esse conjunto de dados possam não estar 100% fiéis em relação ao Diário Oficial da União. Isso ocorre porque os termos usados para filtrar os resultados e por conseguinte extrair as URLs são variados, e o que vale e contempla um instituto, pode não funcionar com outra, já que as páginas web do Diário Oficial da União (as matérias) podem ser escritas ligeiramente diferentes. Por exemplo, em uma o órgão responsável pode ser “reitoria”, em outro pode ser “gabinete” ou outra variação. E é preciso ter o órgão especificado, pois pode haver co-correspondência e as mesmas URLs serem extraídas para dois institutos diferentes. Então fica a ressalva.

*No arquivo "config.py" há as credenciais para acessar a conta no MongoDB Atlas, plataforma de armazenamento em nuvem, onde os dadods enttão armazenados. *

## Atualização

Uma das facilidades que a ferramenta teria seria a atualização automática da base de dados. Pois diariamente o DOU lança novas matérias e por conseguinte elas seriam armazenadas automaticamente. Todavia, isso não foi feito devido ao tempo. 


## Mais informações

## Mais informações podem ser encontradas nos artigos (parcial e final) da ferramenta.


