# Refatoração com Base nos Princípios do SOLID

*1. Princípio da Responsabilidade Única (SRP):*

* Originalmente, a classe Client tinha a responsabilidade tanto de armazenar informações sobre o cliente quanto de gerar o extrato com os aluguéis. Isso violava o SRP, pois essa classe estava assumindo mais de uma responsabilidade.
* A refatoração separou essas responsabilidades. Agora, uma interface ExtratoGenerator define o contrato para a geração de extratos. Diferentes implementações, como ExtratoTexto e ExtratoHtml, são responsáveis pela geração do extrato em formato de texto ou HTML, respectivamente.

*2. Princípio Aberto/Fechado (OCP):*

* Por exemplo, para adicionar novos formatos de extrato (como PDF ou JSON), basta criar uma nova classe que implemente a interface ExtratoGenerator, sem alterar as classes existentes.
* Além disso, o cálculo dos preços das fitas foi abstraído em classes de estratégia, como PrecoNormal, PrecoLancamento e PrecoInfantil. Se uma nova regra de cálculo de preços for introduzida, basta criar uma nova classe de preço, sem modificar as classes existentes.

*3. Princípio de Substituição de Liskov (LSP):*

* As classes que implementam a interface ExtratoGenerator (como ExtratoTexto e ExtratoHtml) podem ser usadas de forma intercambiável, garantindo que, em qualquer lugar onde se espera um ExtratoGenerator, qualquer uma das implementações seja válida, mantendo o comportamento esperado.

*4. Princípio da Segregação de Interface (ISP):*

* A interface ExtratoGenerator foi desenhada para ser simples, contendo apenas o método necessário para gerar o extrato. Isso garante que as classes que implementam a interface só precisem se preocupar com a geração do extrato.

*5. Princípio da Inversão de Dependência (DIP):*

* As classes de cliente (Client) não dependem mais de implementações concretas para a geração de extrato. Em vez disso, a geração de extrato é feita por meio da interface ExtratoGenerator. Isso permite maior flexibilidade, pois o cliente pode gerar extratos em diferentes formatos sem alterar seu código.

# Resposta as Perguntas

*1. O que acontece se o extrato de um cliente deve agora retornar no formato HTML, ao invés de String?*

-> Com a refatoração aplicada, o código já está preparado para suportar diferentes formatos de extrato. O sistema utiliza a interface ExtratoGenerator, que define o método para gerar o extrato. Atualmente, existem implementações para extrato em formato de texto e HTML. Se o extrato precisar ser retornado em HTML, basta alterar a implementação usada, substituindo ExtratoTexto por ExtratoHtml. Essa mudança não requer alterações na classe Client ou no restante da lógica, já que o cliente agora depende de uma abstração e não de uma implementação concreta.

*2. O que ocorre se as regras de cálculo e preço mudarem?*

-> Como o cálculo de preços foi abstraído para as classes de estratégia (PrecoNormal, PrecoLancamento, PrecoInfantil), é possível modificar as regras de cálculo de forma simples. Se as regras de preço mudarem, é necessário criar novas classes que implementem essas regras ou alterar os valores referentes a classe que mudou.

*3. Se a classificação das fitas mudar toda semana?*

-> Com a refatoração, a classificação das fitas (NORMAL, LANCAMENTO, INFANTIL) é controlada por diferentes classes de preço, associadas a cada instância de Tape. Se a classificação mudar frequentemente, basta alterar ou substituir a estratégia de preço da fita.

*4. Se o esquema de pontos de alugador puder mudar a qualquer hora?*

-> O cálculo de pontos do cliente está isolado no método responsável por essa funcionalidade dentro da classe Rent. Isso permite que, se o esquema de pontos mudar, as novas regras sejam aplicadas sem modificar outras partes do código.
