# Resiliência

###### tags: `resilience` `resiliencia` `availability` `disponibilidade` `reliability` `confiabilidade`

> ###### Esse conteúdo é baseado nas seguintes fontes: 
> ###### Livro de [Michael T Nygard, Release It!: Design and Deploy Production-Ready Software](https://www.amazon.com.br/Release-Design-Deploy-Production-Ready-Software/dp/1680502395/ref=asc_df_1680502395/?tag=googleshopp00-20&linkCode=df0&hvadid=379726163686&hvpos=&hvnetw=g&hvrand=347469183041638518&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=1001773&hvtargid=pla-380328175883&psc=1).
> ##### Livro [Patterns for Fault Tolerant Software](https://www.amazon.com.br/Patterns-Fault-Tolerant-Software-English-ebook/dp/B00DXK33SK) de Robert S. Hanmer.
> ##### Livro [Continuous Architecture in Practice: Software Architecture in the Age of Agility and Devops](https://www.amazon.com.br/Continuous-Architecture-Practice-Software-Agility/dp/0136523560/ref=asc_df_0136523560/?tag=googleshopp00-20&linkCode=df0&hvadid=379735814613&hvpos=&hvnetw=g&hvrand=13463599606167538282&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=1001773&hvtargid=pla-1209039305209&psc=1) por  Murat Erder, Pierre Pureur, Eoin Woods e assinado por Vaughn Vernon



**Sumário**
- [As definições de disponibilidade e confiabilidade](#as-definições-de-disponibilidade-e-confiabilidade)
    - [Disponibilidade](#disponibilidade)
    - [Confiabilidade](#confiabilidade)
    - [Como ser disponível](#como-ser-disponível)
    - [Como ser confiável](#como-ser-confiável)
- [Conhecendo mais sobre falhas, erros e defeitos](#conhecendo-mais-sobre-falhas-erros-e-defeitos)
- [Reconhecendo que falhas são inevitáveis](#reconhecendo-que-falhas-são-inevitáveis)
- [Resiliência depende de contenção de falhas](#resiliência-depende-de-contenção-de-falhas)
- [Identificando a ocorrência de falhas](#identificando-a-ocorrência-de-falhas)
    - [Health Checks](#health-checks)
    - [Watchdogs](#watchdogs)
- [Estratégias para contenção de falhas](#estratégias-para-contenção-de-falhas)
    - [Comunicação assíncrona](#comunicação-assíncrona)
    - [Bulkheads](#bulkheads)
- [Estratégias para prevenção de falhas](#estratégias-para-prevenção-de-falhas)
    - [Back pressure](#back-pressure)
    - [Load shedding](#load-shedding)
    - [Timeout](#timeout)
    - [Proxy para componentes que apresentam riscos](#proxy-para-componentes-que-apresentam-riscos)
    - [Circuit breaker](#circuit-breaker)


## As definições de disponibilidade e confiabilidade
### Disponibilidade 
É um atributo de qualidade mensurável, que indica a relação entre o tempo em que um sistema ou componente está disponível e o tempo em que ele poderia (ou deveria) estar. Entendendo-se, nesse contexto, que um sistema está disponível quando funciona com a performance para qual foi projetada.

### Confiabilidade
Também um atributo de qualidade mensurável, implica que, além de disponível, um sistema ou componente opere sem erros e defeitos.

Para ser confiável, um sistema ou componente precisa se manter disponível. Entretanto, nem todo sistema disponível é confiável.

### Como ser disponível
Historicamente, disponibilidade é obtida através de clusterização e replicação. A ideia é tentar reduzir o impacto de saturação de alguma instância de componente, distribuindo corretamente as cargas.

### Como ser confiável
Devido aos custos de escala e a fragmentação crescente de componentes (como em arquiteturas baseadas em microsserviços), ultimamente tem-se adotado, outro termo: resiliência.

Para ser resiliente, um componente precisa adaptar seu comportamento, reconhecendo eventuais erros ou defeitos nos demais, tolerando problemas como latência, eventualmente implantando mecanismos de retentativas, circuit-break, reinicialização automática, entre outros. **Sistemas resilientes não são, necessariamente, mais disponíveis, mas, sem dúvidas, são mais confiáveis.**

## Conhecendo mais sobre falhas, erros e defeitos
Em sistemas de software, falhas são uma espécie de rachadura pequena que, se não forem contidas, eventualmente, se propagam e acabam tornando-se defeitos.

Pequenas falhas – como bugs ou validações insuficientes em entradas de informação fornecidas por usuários, por exemplo – deixam o sistema em estado inconsistente, o que, ocasionalmente, dá origem a erros, ou seja, comportamentos indesejados do software que culminam em defeitos e possivelmente indisponibilidades.

Falhas provocam erros que provocam defeitos. Por exemplo, consultas SQL mal escritas são falhas que, eventualmente, geram lentidão no banco para responder outras consultas que, por sua vez, causam o aumento nas filas de requisições que, se prolongadas, “topam” memória que, finalmente, tornam um sistema indisponível.

## Reconhecendo que falhas são inevitáveis
Sistemas estão ficando maiores, logo, mais complexos nos últimos anos. Esse crescimento associado a novas tecnologias como a nuvem, conduziram ao desenvolvimento de soluções com cada vez mais granularidade, mais fáceis de manter e distribuir. Entretanto, seguindo as leis do *trade off*, sempre existem downsides, maior fragmentação também significa maiores riscos e uma maior complexidade atrelada principalmente à manutenibilidade.

![img1_disponibilidade](https://user-images.githubusercontent.com/107938412/205654625-de843da9-5917-4d8e-b626-4cfca0396864.png)

Estatisticamente é fácil demonstrar que quanto mais componentes formam um sistema, maiores são as chances da ocorrência de incidentes com potencial para gerar instabilidade. Em termos simples, falhas, além de inevitáveis devem ocorrer com frequência cada vez maior.

## Resiliência depende de contenção de falhas
A estratégia mais efetiva para evitar defeitos é impedir que falhas acabem se tornando erros. Para isso, é importante, tentar minimizá-las e impedir que suas consequências eventualmente se espalhem.

Em sistemas complexos, sem o devido cuidado, falhas em um componente se propagam rapidamente gerando erros em componentes que possuem acoplamento mais alto. Por isso, sob ponto de vista arquitetural é importante cuidar dos pontos de integração com atenção especial adotando estratégias que mitiguem impactos de falhas, erros ou defeitos.

>***Note*** Uma abordagem interessante sobre contenções e mitigação de impactos de falhas em ponto de integração é a [**Anti-corruption Layer (ACL)**]()

As falhas em componentes remotos podem assumir diversas formas, incluindo falhas de comunicação ou comportamento. Componentes remotos podem se tornar inesperadamente indisponíveis ou, o que é muito pior, incrivelmente lentos. Por isso, é essencial que práticas defensivas sejam adotadas.

## Identificando a ocorrência de falhas
### Health Checks
A melhor forma de saber que um componente está funcionando bem é *perguntando* para ele. Sob o ponto de vista arquitetural, isto implica em adicionar uma função de verificação de saúde em cada componente, geralmente acessível através de um endpoint específico.

![img2_healthcheck](https://user-images.githubusercontent.com/107938412/205654656-6ea1ca65-e99a-457a-b0f0-ebcd285ba32a.png)

A idéia, essencialmente, é fazer com que cada componente execute alguma rotina de auto-verificação, preferencialmente alguma atividade sem efeitos colaterais duradouros, retornando um valor que se comporte como um indicador do seu nível de saúde. Obviamente, caso o componente não consiga processar a requisição, isso indica um problema.
As health checks devem ser utilizadas tanto por load balancers, orquestradores de contêineres e por ferramentas de monitoramento.

Eventualmente, as verificações podem incluir as principais dependências dos componentes, como bancos de dados, serviços remotos, etc.

É importante configurar adequadamente funções de health check com intervalos e alguma estrutura utilizando caching para evitar sobrecargas desnecessárias.

### Watchdogs
Enquanto health checks operam passivamente, fornecendo informações sobre a saúde dos componentes, watchdogs tem uma atuação ativa, muitas vezes acionando health checks sob determinadas circunstâncias e disparando algum tipo de ação.

Um watchdog é um programa geralmente associado a ferramentas de APM e métricas de infraestrutura. Seu objetivo é detectar automaticamente possíveis problemas de aplicativo e infraestrutura, observando continuamente tendências e padrões nas métricas e procurando comportamento atípico.

Watchdogs devem ser planejados na arquitetura, mas raramente são implementados dentro de casa. Os fornecedores da nuvem oferecem alternativas altamente configuráveis e flexíveis.

## Estratégias para contenção de falhas
### Comunicação assíncrona
Substituir chamadas diretas por trocas de mensagens é, provavelmente, a medida mais eficiente para aumentar a resiliência de sistemas de software. A ideia é substituir chamadas a componentes potencialmente instáveis por mecanismos de mensageria comprovadamente sólidos e estáveis.

![img3_async](https://user-images.githubusercontent.com/107938412/205654667-f442f707-8547-4280-a814-b6792b17c9fb.png)


A abordagem mais simples é utilizar filas point-to-point. Uma alternativa mais sofisticada e com menor acoplamento é a adoção do modelo de pub/sub.

![img7_pubsub](https://user-images.githubusercontent.com/107938412/207679107-0b55a77a-0cc8-4a63-a10c-1ec6183da925.png)

A alternativa tradicional é utilizar estratégias de alta-disponibilidade com replicações e load balancers.

>***Warning*** É importante ter consciência e cuidado com o uso de filas e tópicos. Eles existem para auxiliar na construção de um ecossistema mais assíncrono mas ainda existem diversas situações onde o síncrono é necessário e não deve ser substituido, o uso de filas e tópicos também implica em maior complexidade, o que também significa que implementar mensageria desordenadamente é extremamente prejudicial, sem fundamento e não trás benefícios para aplicações. Vale ressaltar também que, a mensageria não tem como propósito ser um redirecionador de responsabilidades, a resiliência cabe à aplicação e não deve ser transferida para serviços de mensageria como uma maneira preguiçosa de falsas garantias.

### Bulkheads
A ideia é basicamente criar instâncias dedicadas de determinados componentes para alguns cenários de uso. Dessa forma, impedindo que falhas ou eventos em um contexto de consumo se propaguem para os demais.

![img4_bulkhead](https://user-images.githubusercontent.com/107938412/205654685-e096b605-8482-4e43-95b1-dbadf229273f.png)

## Estratégias para prevenção de falhas
### Back pressure
Sempre que a intensidade de tráfego for desfavorável para um componente, o comportamento ideal é que ele passe a recusar novas demandas (usando load shedding ou rate limit), devolvendo a pressão para o cliente que deverá implementar e se munir de estratégias de retenção ou reduzindo o volume de demandas.

Do ponto de vista do componente que está adotando back pressure, a implementação é restrita a alguma resposta de sinalização (talvez retornando 429 – Too many requests) para o cliente indicando a condição. Caberá ao cliente adotar a estratégia apropriada conforme a resposta obtida na requisição.

>***Note*** Existem também estratégias para redução do volume de demandas citado anteriormente, são geralmente conhecidas como estratégias de degradação ou gracefully degradation.

### Load shedding
Assim como um rate limiter, um componente de load shedding opera como um middleware que monitora os recursos computacionais necessários da aplicação ou algum outro componente específico, bem como das dependências, e recusa ativamente novas requisições até que níveis saudáveis pré-determinados sejam restaurados.

### Timeout
Pior do que componentes que param de responder são aqueles que passam a operar com lentidão incomum. Estabelecer timeouts é importante para impedir que componentes clientes esperem tempo demais, seja para solicitações síncronas quanto assíncronas.
Embora não haja uma receita de bolo para escolher um timeout correto, eles devem ser relativamente curtos. A recomendação segura é 150% do tempo médio de resposta do serviço.

### Proxy para componentes que apresentam riscos
Todo componente que não está sob controle do time de desenvolvimento interno e que precisa estar em conformidade com as táticas de resiliência, deve estar envelopada por um proxy.

![img5_proxy](https://user-images.githubusercontent.com/107938412/205654702-5e5a5ca2-5d88-4c67-841e-004440124973.png)

O proxy (Envoy, PgBound, HAProxy, etc) consegue resolver regras como load shedding, time outs, entre outros.

### Circuit breaker
Circuit breaker é uma instância de máquina de estados implementada entre dois componentes, um cliente e o outro servidor. O objetivo de um Circuit breaker é proteger o servidor de requisições enquanto este estiver enfrentando dificuldades (ou uma potencial saturação).

O funcionamento da máquina de estados é o seguinte:


1. Circuito fechado
    1.1. Toda requisição do cliente deve ser encaminhada ao servidor
    1.2. Se houverem mais falhas do que o aceitável dentro de um intervalo de tempo, então o circuito deve abrir.
2. Circuito aberto
    2.1. Nenhuma requisição do cliente deve ser encaminhada ao servidor, falhando imediatamente
    2.2. Transcorrido um determinado tempo, o circuito deve ficar meio aberto
3. Circuito meio aberto
    3.1. Algumas requisições devem ser encaminhadas para o servidor,  outras negadas
    3.2. Se as falhas persistirem, o circuito deverá abrir novamente
    3.4. Se as falhas não ocorrerem mais, o circuito deverá fechar.

![img5_circuitbreaker](https://user-images.githubusercontent.com/107938412/205654693-975bad3f-2a1b-49a4-a688-a1915e53b564.png)
