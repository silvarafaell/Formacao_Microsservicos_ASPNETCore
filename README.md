Curso Formação Microsserviços com ASP.NET Core no nextwave(LuisDEV)

### O que é Monolito
 - Aplicação construída como uma unidade única, sendo um executável único
 - Para se realizar uma alteração, é necessário realizar um build da aplicação toda e depois um deploy da versão atualizada
 - É importante entender as diferenças em diversos aspectos em relação aos microserviços
 - Apresenta alguns desafios, como:
   - Manutenção de código, por ser mais propenso ao Big Ball of Mud, situação onde os desenvolvedores não entendem a aplicação completa
   - Escalabilidade por ser um desafio
   - Dificuldade de se tornar ágil na parte operacional em ambientes de publicações mais frequentes

### Fundamentos de Microsserviços
 - Serviços pequenos e autônomos que trabalham juntos, e que são coesos e desacoplados
 - Separados por contextos (ou bounded countexts)
 - É citado no livro Buiding Microservices, que um microserviço deve ser pequeno o bastante para ser reecrito em 2 semanas, e autônomo para que possa ser alterado e publicado sem afetar outros serviços

### Desafios em Microsserviços
 - Além do nome, ele é uma arquitetura distribuída. Sendo assim, é importante conhecer os desafios desse tipo de arquitetura
 - Desafios
   - Integração e consistência dos dados (especialmente em falhas)
   - Falhas na rede e na comunicação
   - Sobrecarga no gerenciamento (infra)

### Microsserviços vs Monolitos
 - Repositórios
   - Microserviços: Multiplos
   - Monolitos: Único
 - Tecnologias
   - Microserviços: Multiplos
   - Monolitos: Única
 - Publicação
   - Microserviços: Multiplos
   - Monolitos: Única
 - Single Point of Faiture
   - Microserviços: Não
   - Monolitos: Sim
- Manutenção
   - Microserviços: Dificil
   - Monolitos: Facil
- Comunicação
   - Microserviços: Rede
   - Monolitos: In-Process
- Integração
   - Microserviços: Assincrona
   - Monolitos: Sincrona
- Consistencia
   - Microserviços: Eventual
   - Monolitos: Imediata

### Benefícios da Arquitetura de Microsserviços
 - Benefícios
   - Otimizado para escalabilidade horizontal
   - Tolerância a falhas (também reduzindo os Single Point of Faiture)
   - Permitir a heterogeneidade de tecnologias
   - Publicações mais rápidas
   - Maior simplicidade da base de código 
 
### O que é Domain-Driven Design
 - Abordagem de desenvolvimento orientado ao domínio do negócio, alinhado a linguagem utilizada nele ao software produzido
 - Termo apresentado por Eric Evans no livro "Domain-Driven Design: Tackling Complexity in the Heart of Software"
 - Não é uma arquitetura, nem reforça a uma em especifico.
 - É importante não se tornar puritano depois e utilizar os conceitos aprendidos como uma bala de prata. Exemplo: repositório para atualizações mais complexas
 - Diversos componentes são citados nos livros, como Linguage Ubíqua, Contextos Delimitados, Repositórios, Entidade, Agregados, Eventos de Domínio, Serviços de Domínio, e Factories
 - O valor principal do Domain-Driven Design está em modelar software que resolva um problema do negócio, e não apenas que tenha uma estrutura X ou pastas Y
 - É essencial ter contato com especialistas do negócio, visto que na prática a teoria é outra, e achismos dificilmente resultam em funcionalidades úteis para seus usuários

 ### Linguagem Ubíqua
  - Também conhecida como Linguagem Onipresente, é um termo usado por Erick Evans para descrever uma linguagem compartilhada pelo time
  - "Time" envolve desenvolvedores, especialistas do domínio, e outros membros
  - É muito comum, infelizmente, do time de desenvolvimento estar alienado aos requisitos do negócio
  - Assim como os requisitos do negócio, a Linguagem Ubíqua está em constante evolução, junto ao entendimento do time do negocio
  - Em domínios mais complexos a importância dela aumenta mais ainda. Afinal, o DDD é mais recomendado para cenários desse tipo, como E-Commerces
  
### Entidades
 - Identificadas geralmente através de substantivo contidos nas descrições de processos de negócio
 - Contém um identificador único, se aceita quem sejam atualizados com o tempo sem perder sua identidade
 - A nível técnico, é recomendado que tenham seus setters privados, para se ter maior controle de regras de negócio e com outros componentes, coo os eventos de domínio.
 
### Value Objects
 - Se diferenciam das entidades ao não terem um identificador único
 - São identificados pelo seus atributos como um todo, não apenas por um único
 - Um exemplo famoso é o endereço. Um endereço é imutável, ele é composto por logradouro, bairro, CEP, etc. Se um desses itens mudarem, estaremos falando de outro endereço completamente diferente

### Agregados
 - Conjunto de entidades e Value Objects que representam uma unidade de consistência. O ponto de entrada é conhecido como Aggregate Root
 - Para exemplificar, considere o exemplo de Pedido. Um pedido contém itens de pedido, e também endereço de entregae/ou pagamento
 - Os itens e endereço de pedido não existem sem o Pedido. Eles devem estar consistentes entre si
 - Em um banco de dados NoSQL orientado a documento, geralmente um agregado vai mapear para uma coleção, já que é possível ter objetos internos (tanto entidade quanto value object)
 - Geralmente haverá um repositório por Agregado, já que não faz muito sentido poder alterar elementos do agregado diretamente sem passar pelo o Aggregate Root
 
### Repositórios
 - Padrão utilizado para a realização de operações em coleções, agnóstico a tecnologia utilizada
 - Geralmente associado a um Agregado
 - Se indica geralmente que sua interface fique no Core, e sua implementação na Infrastrucutre
 - Pode serve como uma fronteira entre o Modelo de Persistência e o de Domínio
 
### Contextos Delimitados
 - Mapeia um subdomínio para uma solução, contendo peculiaridades próprias na linguagem ubíqua para entidades, value objects e outros componentes
 - Um exemplo é o de Cliente. O cliente para um setor de marketing pode ser representado por nome, dados de contato e histórico de compras, para o setor de Entregas apenas por seu nome e endereço, e para o setor de Fidelização, apenas pelos seus dados de compra e contato
 
### Mapeamento de Contextos
 - O mapeamento de contextos auxilia na definição e visualização dos relacionamentos entre contextos delimitados
 - Existem alguns tipos de relacionamentos, como:
   - Shared Kernel: aproveitamento de código entre contextos
   - Partner: evolução em conjunto, mas exige maeios esforço na parte de gestão
   - Customer-Supplier: O Customer (downstream) depende do Supplier (upstream).
   
### Arquitetura Limpa - Camada Core
 - Também chamada de Domain, é a camada central da aplicação, onde não deveria ter dependências em outros projetos
 - Seus principais componentes são (relacionado com DDD):
   - Entities
   - ValueObjects
   - Repositories (interfaces)
   - Enums
   - Serviços de domínio
   - Eventos domínio

### Arquitetura Limpa - Camada Infrastructure
 - É aqui onde são implementadas as integrações com componentes da infra-estrutura ou outros sistemas, como banco de dados, APIs externas, sistemas legados, serviços de Cloud, e etc
 - Seus Principais componentes são:
   - Implementação de Repositórios
   - Serviços de Integração com outros sistemas
   - Serviços de integração Cloud
   - Serviços de integração com Message brokers

### Arquitetura Limpa - Camada Application
 - É aqui onde são implementadas os casos de uso da aplicação, envolvendo os modelos de dados que a aplicação recebe do usuário/mundo exterior
 - Seus principais componentes são:
   - Serviços de aplicação (geralmente 1.1 para funcionalidades)
   - Commands e Queries (se utilizar o padrão CQRS)
   - Modelos de entrada e saída (DTOs)
   - Subscribers/Consumers de eventos

### Arquitetura Limpa - Camada API
 - É aqui onde outros sistemas se integram com a aplicação/API. Esses sistemas podem ser front-end, desktop ou mesmo outras APIs
 - Seus principais componentes são:
   - Controllers
   - Startup (que orquestra a configuração da aplicação)

### O que é CQRS
 - Sigla para Command Query Responsibility Segregation, é um padrão que separa a responsabilidade de escrita e leitura
 - É um padrão bastante utilizada não somente por promover uso de modelos/bancos de dados diferentes mas por melhorar a legibilidade, testabilidade e manutenção
 - Seus principais componentes são: Commands e Queries, e seus respectivos Handlers.

### Commands e Queries
- Commands
  - Comandos representam alterações no estado do sistema, sendo nomeados de acordo com a ação realizada pelo usuário
  - Geralmente ficam na camada de Application, já que correspondem a um caso de uso, como AddProduct, RegisterParticipant, DeactivateAccount
  - Eles contém os modelos de dados da operação, e são então tratados pelos seus respectivos Handlers
- Queries
  - Consultas representam..consultas no sistema, ou seja, supostamente não deveriam alterar o sistema (embora em alguns casos, como registro de data de leitura, alterem o sistema)
  - Geralmente ficam ou na camada de Application, ou na camada de Infractructure. Isso pode ocorrer pois em alguns casos, a eficiência na consulta dos dados específicos é mais importante do que o perfeccionismo do padrão
  - Contém os dados de consulta, que são tratados pelo o Handler 
 
### Padrão Mediator
 - Padrão utilizado para desacoplar classes das que eles dependem diretamente
 - Ao invés de conhecer as regras de instância de outras, a classe "pediria" ao objeto Mediator para "entregar" o objeto
 - Este padrão funciona muito bem com o padrão CQRS, já que cada controller precisaria delegar o Command ou Query ao seu Handler
 - Uma biblioteca utilizada bastante para isso é o MediatR, que mapeia os Handlers, com as classes de dados (Commands ou Queries) e de saída (View Model)
 - Com isso, o MediatR permite, passando o Command ou Query, econtrar o seu Handler respectivo e delegar o processamento dos dados
 - Isso resulta em uma estrutura desacoplada e simples a nível do Controller, com novos Handlers sendo adicionados sem complexidade

### O que é MongoDB
 - Banco de dados NoSQL não são tabulares, armazenando dados em modelos diferentes do que as tabelas ralacionais
 - Os tipos principais de bancos de dados NoSQL são:
   - Chave-Valor(Redis)
   - Documentos (MongoDB, RavenDB)
   - Grafos (Neo4j)
   - Orientados a colunas (Cassandra)
 - MongoDB
   - Bando de dados NoSQL orientado a documentos, com um formato semelhante ao Json (chamado BSON)
   - Os documentos são armazenados em coleções (collections), o que seria análogo as tabelas em bancos de dados relacionais
   - É um banco de dados de alta performance, e por ter suporte a objetos relacionados, facilita a modelagem de dados
   - O pacote oficial para .NET é o MongoDB.Driver, de fácil utilização
   - É possível armazenar um Agregado completo como documento, por ele ter suporte a objetos relacionados
   - A chave primária de um documento é o campo _id(por convenção a propriedade Id da classe é usada), e atualizações são feitas no objeto inteiro
   
### Comunicação Tradicional
 - O jeito tradicional de comunicação entre sistemas é o chamado request-response
 - Nele, um cliente (computador ou aplicação) realiza uma requisição, e o servidor response com os dados pedidos
 - Enquanto o servidor tiver capacidade de responder as requisições, esse modelo atende muito bem
 - Porém, se o volume de tráfego aumentar muito, ele pode rapidamente se tornar um gargalo
 - Se o sistema falhar sob uma alta carga de requisições, ou mesmo tiver uma falha interna, o fluxo de comunicação vai falhar e parar
 - Imagine uma rede de dependência entre serviços envolvendo ele diretamente. Requisições vão resultar em timeout se não forem tratadas, e isso pode cascadear
