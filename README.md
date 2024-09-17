# Refatoração com Base nos Princípios do SOLID

1. Princípio da Responsabilidade Única (SRP):

* Originalmente, a classe Client tinha a responsabilidade tanto de armazenar informações sobre o cliente quanto de gerar o extrato com os aluguéis. Isso violava o SRP, pois essa classe estava assumindo mais de uma responsabilidade.
* A refatoração separou essas responsabilidades. Agora, uma interface ExtratoGenerator define o contrato para a geração de extratos. Diferentes implementações, como ExtratoTexto e ExtratoHtml, são responsáveis pela geração do extrato em formato de texto ou HTML, respectivamente.

2. Princípio Aberto/Fechado (OCP):

* Por exemplo, para adicionar novos formatos de extrato (como PDF ou JSON), basta criar uma nova classe que implemente a interface ExtratoGenerator, sem alterar as classes existentes.
* Além disso, o cálculo dos preços das fitas foi abstraído em classes de estratégia, como PrecoNormal, PrecoLancamento e PrecoInfantil. Se uma nova regra de cálculo de preços for introduzida, basta criar uma nova classe de preço, sem modificar as classes existentes.

3. Princípio de Substituição de Liskov (LSP):

* As classes que implementam a interface ExtratoGenerator (como ExtratoTexto e ExtratoHtml) podem ser usadas de forma intercambiável, garantindo que, em qualquer lugar onde se espera um ExtratoGenerator, qualquer uma das implementações seja válida, mantendo o comportamento esperado.

4. Princípio da Segregação de Interface (ISP):

* A interface ExtratoGenerator foi desenhada para ser simples, contendo apenas o método necessário para gerar o extrato. Isso garante que as classes que implementam a interface só precisem se preocupar com a geração do extrato.

5. Princípio da Inversão de Dependência (DIP):

* As classes de cliente (Client) não dependem mais de implementações concretas para a geração de extrato. Em vez disso, a geração de extrato é feita por meio da interface ExtratoGenerator. Isso permite maior flexibilidade, pois o cliente pode gerar extratos em diferentes formatos sem alterar seu código.
