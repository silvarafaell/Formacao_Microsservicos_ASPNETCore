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
