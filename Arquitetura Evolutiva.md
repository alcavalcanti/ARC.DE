# Arquitetura Evolutiva

###### tags: `arquitetura` `evolutiva` `architecture` `evolutionary` 

> ###### Esse conteúdo é baseado nas seguintes fontes: 
> ###### Livro de [Neal Ford, Building Evolutionary Architectures: Support Constant Change](https://www.amazon.com.br/Building-Evolutionary-Architectures-Neal-Ford/dp/1491986360).


**Sumário**
- [O que é arquitetura evolutiva](#o-que-é-a-arquitetura-evolutiva)
    - [Os princípios chave da arquitetura evolutiva](#os-principios-chave-da-arquitetura-evolutiva)
    - [Os benefícios da utilização](#os-beneficios-da-utilização)
    - [Quando adotar a abordagem de arquitetura evolutiva](#quando-adotar-a-abordagem-da-arquitetura-evolutiva)
- [Implementando a arquitetura evolutiva](#implementando-a-arquitetura-evolutiva)

## O que é arquitetura evolutiva

Arquitetura Evolutiva refere-se a uma abordagem de desenvolvimento de software em que a arquitetura de um sistema é aprimorada de forma incremental ao longo do tempo, com base no feedback das partes interessadas, usuários e mercado. Essa abordagem é caracterizada por seu foco na flexibilidade, adaptabilidade e melhoria contínua, e é vista como uma alternativa às abordagens tradicionais de "grande design inicial" que visam definir todos os aspectos da arquitetura antes do início da implementação.

Em uma abordagem de arquitetura evolutiva, a arquitetura do sistema é vista como uma entidade viva que evolui em resposta a mudanças de requisitos e tecnologias. Essa abordagem é particularmente adequada para sistemas complexos e dinâmicos que estão sujeitos a requisitos e tecnologias que mudam rapidamente, pois permite que a arquitetura se adapte em resposta a essas mudanças.

### Os princípios chave da arquitetura evolutiva

* **Melhoria incremental:** A arquitetura é continuamente refinada ao longo do tempo, com base no feedback das partes interessadas, usuários e mercado. Isso permite que a arquitetura evolua em resposta a requisitos e tecnologias em constante mudança, em vez de ficar presa a um design fixo.

* **Projeto modular:** A arquitetura é dividida em vários módulos altamente coesos e fracamente acoplados. Isso permite que os componentes da arquitetura sejam atualizados e aprimorados de forma independente, sem afetar o restante do sistema.
 
* **Microsserviços:** A arquitetura é baseada em microsserviços, que são pequenos serviços implementáveis de forma independente que executam funções específicas. Isso permite que o sistema seja dividido em componentes menores e mais gerenciáveis e que evolua e se adapte mais rapidamente em resposta às mudanças de requisitos e tecnologias.
 
* **Integração e entrega contínuas:** a arquitetura é integrada e implantada usando um pipeline de integração e entrega contínuas (CI/CD). Isso permite que as alterações sejam implantadas com rapidez e segurança, sem interromper o sistema geral.
 
* **Escalabilidade:** A arquitetura é projetada para ser escalável, tanto em termos de capacidade quanto de funcionalidade. Isso permite que o sistema cresça e mude em resposta a mudanças na demanda e novos requisitos.

* **Resiliência:** A arquitetura é projetada para ser resiliente, para que possa continuar operando mesmo diante de falhas ou interrupções. Isso é particularmente importante para sistemas críticos, que devem manter altos níveis de disponibilidade e confiabilidade.
 
* **Desenvolvimento orientado por feedback:** O feedback das partes interessadas, dos usuários e do mercado é usado para conduzir o desenvolvimento e a melhoria contínua da arquitetura. Isso permite que a arquitetura evolua em resposta às necessidades e requisitos em constante mudança.

* **Abertura à mudança:** A arquitetura é projetada para ser aberta à mudança, de modo que possa ser facilmente adaptada e evoluída em resposta a requisitos e tecnologias em constante mudança.

Além desses princípios, a arquitetura evolutiva também enfatiza a importância da comunicação, colaboração e aprendizado contínuo. A comunicação eficaz entre as partes interessadas, desenvolvedores e usuários é crucial para o sucesso de uma abordagem de arquitetura evolutiva, assim como uma cultura de aprendizado e melhoria contínua.

### Os benefícios da utilização

Ao adotar a arquitetura evolutiva na organização em contrapartida ao esforço de mudanças de cultura e visão técnica existem pontos positivos, os principais podem ser observados a seguir:

* **Tempo de lançamento no mercado mais rápido:** Ao focar em melhorias incrementais, a Arquitetura Evolucionária permite um tempo de lançamento no mercado mais rápido em comparação com as metodologias tradicionais de "grande projeto inicial".

* **Maior flexibilidade:** A arquitetura evolutiva permite uma arquitetura mais flexível e adaptável que pode evoluir e mudar ao longo do tempo em resposta a mudanças nos requisitos e avanços tecnológicos.

* **Alinhamento aprimorado com os requisitos de negócios:** Ao envolver as partes interessadas no processo de desenvolvimento da arquitetura, a Arquitetura Evolucionária garante que a arquitetura esteja alinhada com os requisitos de negócios e evoluindo de maneira a apoiar os objetivos da organização.

* **Confiabilidade e disponibilidade aprimoradas:** O foco na resiliência e escalabilidade na Arquitetura Evolucionária garante que a arquitetura possa continuar a operar de forma eficaz, mesmo diante de falhas ou interrupções.

### Quando adotar a abordagem de arquitetura evolutiva

A Arquitetura Evolutiva é uma abordagem adequada em situações onde as seguintes condições estão presentes:

**Requisitos complexos e que mudam rapidamente:** Os requisitos de um sistema são complexos, mudam rapidamente ou são difíceis de prever, uma abordagem evolutiva da arquitetura permite uma solução mais flexível e adaptável que pode evoluir e mudar ao longo do tempo em resposta aos requisitos em constante mudança.

**Alto grau de incerteza:** Se houver um alto grau de incerteza nos requisitos ou no cenário tecnológico, uma abordagem evolutiva pode permitir prototipagem e experimentação mais rápidas, o que pode reduzir o risco de desenvolver uma solução que não seja adequada ao propósito.

**Sistemas grandes e complexos:** O sistema que está sendo desenvolvido for grande e complexo, uma abordagem evolutiva pode permitir que a arquitetura seja desenvolvida de forma incremental, reduzindo o risco de desenvolver uma solução excessivamente complexa ou difícil de gerenciar.

**Ambientes com várias partes interessadas:** Se houver várias partes interessadas envolvidas no desenvolvimento de um sistema, como clientes, desenvolvedores e equipes de operações, uma abordagem evolutiva pode permitir um melhor alinhamento e colaboração entre essas partes interessadas.

**Concentre-se no tempo de lançamento no mercado:** Se houver necessidade de obter uma solução para o mercado o mais rápido possível, uma abordagem evolutiva pode permitir um tempo de lançamento no mercado mais rápido em comparação com as metodologias tradicionais de "grande projeto inicial".

Em resumo, a Arquitetura Evolucionária é adequada em situações em que os requisitos são complexos e mudam rapidamente, há um alto grau de incerteza, o sistema que está sendo desenvolvido é grande e complexo, há várias partes interessadas envolvidas ou há foco no *time-to-market*.

É importante ressaltar também que isso não é uma receita de bolo e a organização não precisa atender perfeitamente à todos os requisitos listados acima, inerente a adoção da cultura da arquitetura evolutiva existe muito esforço para mudanças de cultura, adequações técnicas, planejamento e etc. que devem ser consideradas e condizentes com a realidade da companhia. É como diz aquele velho ditado: *"Cada caso é um caso."*

## Implementando a arquitetura evolutiva

Agora que entendemos o que é o principio da arquitetura evolutiva, vamos ao que interessa, como implementamos e sustentamos isso em uma organização?

**Defina a arquitetura inicial:** Comece definindo a arquitetura inicial, que deve incluir uma compreensão clara dos componentes, relacionamentos e processos que compõem o sistema. A arquitetura inicial deve ser flexível e adaptável, com foco em design modular e microsserviços.

**Implemente a arquitetura inicial:** Uma vez definida a arquitetura inicial, implemente-a construindo os componentes e integrando-os no sistema geral.

**Obtenha feedback continuamente:** Colete feedback das partes interessadas, usuários e do mercado para entender os pontos fortes e fracos da arquitetura. Esse feedback deve ser usado para melhorar continuamente a arquitetura ao longo do tempo.

**Faça melhorias incrementais:** Faça pequenas melhorias incrementais na arquitetura com base no feedback recebido. Isso pode incluir adicionar novos componentes, refinar os existentes ou alterar as relações entre os componentes.

**Use pipelines de CI/CD:** Implemente um pipeline de integração e entrega contínuas (CI/CD) para implantar alterações na arquitetura com rapidez e segurança. Isso ajuda a garantir que a arquitetura esteja sempre atualizada e atenda às necessidades do negócio.

**Monitore e meça o desempenho:** Monitore e meça regularmente o desempenho da arquitetura para identificar áreas de melhoria. Isso pode ser obtido usando métricas de desempenho, como tempos de resposta e disponibilidade, para rastrear o desempenho da arquitetura ao longo do tempo.

**Repita o ciclo:** Repita continuamente o ciclo de coletar feedback, fazer melhorias e implantar alterações para evoluir continuamente a arquitetura ao longo do tempo.

**Adapte-se às mudanças de requisitos e tecnologias:** finalmente, esteja preparado para adaptar a arquitetura às mudanças de requisitos e tecnologias à medida que elas surgirem. Isso pode envolver mudanças significativas na arquitetura, como substituição de componentes ou adição de novos, para garantir que ela continue atendendo às necessidades do negócio.
