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
