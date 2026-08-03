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
