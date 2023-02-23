# Microsserviços

###### tags: `micro` `services` `serviços` `serviço` `service` `microsserviços` `microservices` 

> ###### Esse conteúdo é amplamente baseado nos conceitos de microsserviços apresentados no livro [Criando Microsserviços de Sam Newman](https://www.amazon.com.br/Criando-Microsservi%C3%A7os-Projetando-Componentes-Especializados/dp/6586057884/ref=asc_df_6586057884/?tag=googleshopp00-20&linkCode=df0&hvadid=379748659420&hvpos=&hvnetw=g&hvrand=8981600790354988445&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=1001773&hvtargid=pla-1646134392410&psc=1).

---
#### Índice

[ToC]
## A arquitetura de microsserviços

Uma arquitetura de microsserviços consiste em uma coleção de pequenos serviços autônomos. Cada serviço é independente e deve implementar uma única funcionalidade em um contexto limitado. Um contexto limitado é uma divisão natural em uma organização e possui uma fronteira bem definida onde um modelo de domínio existe.

![microsservices](https://user-images.githubusercontent.com/40603968/185422994-49797c99-4a8f-4789-900b-a4e65bef18c3.png)

### O que são os microsserviços?

Comecemos a nossa interpretação dos conceitos abordados comumente em torno do tema de microsserviços com uma frase que deve ser o nosso evangélio/mantra ao trabalhar com esse padrão:

**Um microsserviço, é um serviço pequeno que tem apenas uma responsabilidade vinculada ao negócio e a executa muito bem.**

Dito isso, podemos entrar em mais detalhes e listar características importantes que devem acompanhar a adoção desse modelo arquitetural.

Os microsserviços são *pequenos*, altamente especializados, independentes e com baixo acoplamento. Em um modelo de trabalho ideal, uma única equipe pequena de desenvolvedores deve ser capaz de escrever e manter um microsserviço. Isso também significa que as equipes podem atualizar um serviço existente sem recompilar e reimplantar todo um ecossistema por inteiro.

::: warning
:warning: É extremamente importante ressaltar que **pequeno não significa nano**, um microsserviço deve ser independente e executar muito bem a função para qual foi escrito e é responsável. Nano serviços só devem ser usados em cenários muito específicos, pois adicionam muita complexidade ao ecossistema, entre elas complexidade de troubleshooting, entendimento e leitura e de sustentação e manutenção da aplicação.
:::

Os serviços são responsáveis por manter seus próprios *dados** ou estado,  . Diferente do modelo tradicional, em que uma camada de dados separada lida com toda a persistência de dados. 

:::info
:bulb: Em dados devemos entender como um contexto de dados relevantes para aquele microsserviço específico, um contexto de dados pode ser uma base, uma tabela ou até mesmo uma coluna, o que é importante termos conciência é que entrelaçamento ou overlap de contexto dedados não deve ocorrer.
:::

A comunicação entre os serviços acontece por meio de contratos bem definidos e de forma padronizada (OAS3 e Avro). Detalhes da implementação interna de cada serviço ficam isolados dos demais.

Vale a pena explicitar também que essa independência se expande até o ponto de suportar microsserviços escritos em linguagens diferentes se comunicando normalmente e também o uso de tecnologias voltadas a repositórios e banco de dados. Resumidamente, eles são independentes também tecnologicamente. O mesmo conceito se aplica as bibliotecas e estruturas de cada um deles.

Como sabemos, o tema de microsserviços é bastante amplo e flexível, dessa maneira podemos encontrar um universo de aplicabilidades, para manter a documentação mais eficiente e objetiva vamos nos ater a detalhar adiante alguns dos componentes mais importantes encontrados em uma implementação típica de microsserviços.

### Gerenciamento ou orquestração
Esse componente é responsável por colocar serviços em nós, identificar falhas, rebalancear esses nós quando necessário. Atualmente, encontramos diversas tecnologias amplamente utilizadas e muito eficientes no mercado prontas para uso. Dentro do contexto da Neon é altamente recomendado o uso de orquestradores de containers e de k8s ==como no documento xxxx (indicar algum documento de pipelinde de deploy de engenharia).==

### Gateway de API 
O gateway de API é o ponto de entrada para os clientes. Em vez de chamar serviços diretamente, os clientes chamam o gateway de API, que encaminha a chamada para os serviços adequados no back-end.

A seguir listamos algumas vantagens do uso de um Gateway:

* Desacoplar os clientes dos serviços.
* Os serviços podem usar protocolos de mensagens que não sejam amigáveis à Web, como AMQP.
* Utilização de protocolos de comunicação interna como GRPC.
* O Gateway de API pode executar outras funções abrangentes, como autenticação, registro em log, terminação SSL e balanceamento de carga.
* Políticas prontas para uso, como para limitação, cache, transformações ou validações.
* Autenticação e autorização com Open ID Connection.

## Porque e quando utilizar a arquitetura de microsserviços
Se uma das premissas da organização é agilidade. Já que os microsserviços são implantados de forma independente, é mais fácil gerenciar correções de bugs e lançamentos de recursos. As atualizações são mais rapidas e aplicadas apenas aos pontos específicos, assim como as reverções quando algo der errado. Em muitas aplicações tradicionais, quando um bug é encontrado em uma parte do sistema, ele pode bloquear todo o processo de lançamento.

Times reduzidos e focados. Um microsserviço deve ser pequeno o suficiente para que possa ser criado, testado e implantado por uma única equipe. Equipes menores promovem maior agilidade. Times grandes costumam ser menos produtivos, porque a comunicação é mais lenta, a sobrecarga de gerenciamento aumenta e a agilidade diminui.

Base de código pequena. Em uma aplicação monolítica, existe uma tendência de que, ao longo do tempo, as dependências de código fiquem confusas e se tornem um emaranhado. Adicionar novos recursos e features passam a requerer a alteração do código em muitos lugares. Não compartilhando código nem armazenamentos de dados, uma arquitetura de microsserviços minimiza as dependências e o acoplamento, mitigando ou até evitando problemas desse tipo.

Se combinações de tecnologias são necessárias ou estrategicamente interessantes para a organização. Os times tem liberdade para escolher a tecnologia mais adequada para seu microsserviço e deixando a organização livre para escolher uma combinação de tecnologias mais eficientes e apropriadas para o negócio.

Isolamento a falhas. Se um microsserviço individual se tornar indisponível, e o upstream esteja corretamente projetado para lidar com falhas, ele não interromperá toda a aplicação.

Escalabilidade é um fator importante. Os serviços podem ser dimensionados de maneira independente, permitindo que você escale horizontalmente e de maneira mais precisamente subsistemas que exigem mais recursos, sem necessidade de escalar a aplicação inteira. Usando um orquestrador, como o Kubernetes ou o Service Fabric, você pode empacotar uma densidade maior de serviços em um único host, que permite a utilização mais eficiente de recursos.

Isolamento da camada de dados. É muito mais fácil executar atualizações de esquema, porque apenas um microsserviço é afetado.


## Downsides e considerações
Os benefícios de microsserviços têm um ônus. Veja alguns dos desafios a serem considerados antes de embarcar em uma arquitetura de microsserviços.

* **Complexidade:** Uma aplicação construída utilizando a arquitetura de microsserviços possui mais partes flexíveis que precisam ser gerenciadas do que uma aplicação monolítica equivalente. Cada serviço unitariamente é mais simples, mas a aplicação como um todo é mais complexa.

* **Desenvolvimento e teste:** Escrever um pequeno serviço que funcione como uma engranagem exige uma abordagem diferente da escrita de uma aplicação monolítica ou baseada em camadas. Refatorar entre os limites dos microsserviços pode ser difícil. Também pode ser um desafio testar as dependências de serviço, especialmente quando o aplicativo está evoluindo em um rítmo muito acelerado. Atualmente já contamos com frameworks e ferramentas mais voltadas para esses cenários mas que também exige que os desenvolvedores ampliem seus conhecimentos e elevem o nível de complexidade que lidam no dia a dia.

* **Integridade de dados:** Cada microsserviço deve ser responsável pela própria persistência de dados. Dessa maneira a consistência dos dados pode se tornar um desafio. Uma estratégia interessante para lidar com esse contratempo pode ser adotar a consistência eventual em alguns casos.

* **Latência:** O uso de muitos serviços granulares pequenos muito provavelmente resultará em mais comunicação entre serviços. Quando essa comunicação não for bem dimensionada e gerenciada a latência poderá se tornar um problema. Você precisará projetar os recursos com cuidado. Evite por exemplo, *APIs* excessivamente prolixas e preferêncialmente use padrões de comunicação assíncrona, como o nível de carregamento baseado em mensageria.

:::info
:bulb: Quer saber mais sobre APIs e o padrão REST que utilizamos? Disponibilizamos um treinamento muito rico e de altíssima qualidade que pode ser acessado aqui!
:::

* **Deployment:** O deployment também é um ponto sensível que precisa de atenção, existem diversas soluções maduras e difundidas no mercado para nos assistir nessa etapa do processo, recomendamos o uso do deployment canário.

* **Controle de versão:** As atualizações de um serviço não devem interromper os serviços que dependerem delas. Vários serviços podem ser atualizados a qualquer momento, portanto, sem design cuidadoso, você pode ter problemas com compatibilidade com versões anteriores ou futuras.

* **Falta de governança**: A abordagem descentralizada para compilar microsserviços tem vantagens, mas também pode causar problemas. Você pode acabar com muitos linguagens, tecnologias e estruturas diferentes o que acaba dificultando a manutenção. É importante estabelecer alguns padrões para todo o projeto, sem restringir excessivamente a flexibilidade das equipes.

* **Gerenciamento:** Ter êxito com microsserviços requer uma cultura DevOps madura. Registro em log (principalmente logs correlacionados) entre serviços pode ser desafiador. Atente-se para essa necessidade, a observabilidade, rastreio e registro correto da aplicação é de grande relevância e deve ser valorizada, ela pode impactar em muitas áreas, entre elas troubleshoot, auditorias, entendimento sistêmico, etc.

## O caminho a ser seguido
Como ja elucidamos os ganhos e desafios que orbitam no entorno do universo da arquitetura de microsserviços, separamos também a seguir alguns pontos listados que são convencionalmente boas práticas para se atentar quando formos construir uma aplicação baseada nesse padrão.

Modele os serviços nas fronteiras de domínio da empresa.

**Descentralizar é a chave**. Times individuais são responsáveis por projetar e criar serviços. O cross, com algumas exceções é claro, majoritariamente atrapalha e dificulta a agilidade e independência.

**O armazenamento de dados deve ser privado para o serviço que é o proprietário dos dados.** Use o melhor armazenamento para cada serviço e tipo de dados. O mercado hoje oferece uma vasta gama nesse sentido, **em caso de dúvidas procure a arquitetura de dados**.

**Os serviços comunicam-se por meio de contratos bem definidos**. Evite o vazamento de detalhes das implementações. Os contratos devem modelar o domínio, não a implementação interna do serviço.

**Evite acoplamento entre os microsserviços**. Causas comuns de acoplamento por exemplo são, comunicações muito rígidos e esquemas de banco de dados compartilhados.

Transfira a responsabilidade e preocupações colaterais como autenticação e SSL para o gateway, deixe o caminho livre para focar no que é estrategicamente importante e gera valor para o negócio.

Mantenha o conhecimento de domínio fora do gateway. O gateway deve tratar e rotear solicitações de cliente sem qualquer conhecimento das regras de negócios ou da lógica do domínio. Caso contrário, o gateway se tornará dependente e poderá ser mais um obstáculo e um gerador de acoplamento entre os microsserviços.

**Os serviços devem ter um acoplamento flexível e alta coesão funcional. Funções que provavelmente mudarão juntas devem ser empacotadas e implantadas juntas.** Se residirem em serviços separados, esses serviços acabarão sendo fortemente acoplados, porque uma alteração em um serviço exigirá atualizar outro. Uma comunicação excessivamente prolixa entre dois serviços pode ser um sintoma de alto acoplamento e coesão baixa e isso não é legal.

**Isole as falhas**. Use abordagens de *resiliência* para impedir que falhas em um microsserviço se propaguem e saiam do controle.

:::info
:bulb: Quer saber mais sobre resiliência? Nos aprofundamos mais nesse assunto na documentação disponível aqui!
:::


[:arrow_up: Voltar para o início](#Microsserviços)


> Deixem comentários e sugestões! :rocket: [color=#3b75c6]
