# Domain Driven Design

###### tags: `ddd` `domain` `driven` `design` `domínio`

> ###### Esse conteúdo é baseado no livro de [Vaughn Vernon do livro Domain-Driven Design Distilled](https://www.amazon.com.br/Domain-Driven-Design-Distilled-Vaughn-Vernon/dp/0134434420/ref=asc_df_0134434420/?tag=googleshopp00-20&linkCode=df0&hvadid=379735814613&hvpos=&hvnetw=g&hvrand=2005807085629592401&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=1001773&hvtargid=pla-451410218303&psc=1) também conhecido como Green Book.
> ##### E também no livro [Domain Driven Design: Tackling Complexity in the Heart of Software]() do Eric Evans, o pai do DDD.

---

**Sumário**
- [O que é o Domain Driven Design (DDD)](#o-que-é-o-domain-driven-design-ddd)
    - [O que é um domínio?](#o-que-é-um-domínio)
- [Os três pilares do DDD](#os-três-pilares-do-ddd)
    - [Linguagem ubíqua ](#linguagem-ubíqua)
    - [Contextos delimitados](#contextos-delimitados)
    - [Mapa de contexto](#mapa-de-contexto)
- [O que é o Modelo e qual sua utilidade?](#o-que-é-o-modelo-e-qual-sua-utilidade)
- [O conceito e a aplicação da modelagem evolutiva e mutável](#o-conceito-e-a-aplicação-da-modelagem-evolutiva-e-mutável)
- [Como modelar de maneira efetiva](#como-modelar-de-maneira-efetiva)
- [A arquitetura em camadas do Domain Driven Design](#a-arquitetura-em-camadas-do-domain-driven-design)
- [Vantagens da utilização do DDD](#vantagens-da-utilização-do-ddd)
- [Downsides](#downsides)


## O que é o Domain Driven Design (DDD)
O DDD - Domain Driven Design - é um conceito que foi introduzido à literatura por Eric Evans, em 2004, no seu livro Domain Driven Design: Tackling Complexity in the Heart of Software. Em tradução literal, Domain Driven Design: Atacando as complexidades no coração do software.

Uma das características do DDD, é a sua mutabilidade que pode ser desenvolvida ao longo do tempo. Essa característica fica evidente num contexto de microsserviços por exemplo, em que cada um tem uma responsabilidade definida e que pode ser desenvolvida de forma independente. Um microsserviço pode alterar uma parte do seu contexto sem ser necessária a alteração de todas as aplicações que o utilizam.

> [!NOTE]  
> Se você ainda não está familiarizado com o padrão de microsserviços ou gostaria de saber mais sobre como abordamos esse tema por aqui, recomendamos uma visita a nossa **[arquitetura de referência de Microsserviços!](https://github.com/alcavalcanti/arch-ref/blob/main/Microsservi%C3%A7os.md)**

Como DDD se trata de um conceito, ele pode estar presente em arquiteturas de projeto distintas. No entanto, o fato de seguir o DDD em algumas implementações não significa que se utiliza DDD para toda aplicação. Para isso, é importante entender os seus conceitos e abstraí-los para que seja possível a aplicação na rotina do processo de desenvolvimento da organização.

### O que é um domínio?
O domínio de um software é composto pelo fluxo de atividades realizadas pela pessoa usuária e todas as regras de negócio relacionadas a esse fluxo. 

Assim como sua definição é ampla, um domínio pode ser complexo e possuir subdivisões dentro dele igualmente complexas. 

## Os três pilares do DDD
Os três pilares do DDD são:
1. Linguagem ubíqua (ubiquitous language)
2. Contextos delimitados (bounded contexts)
3. Mapa de contextos (context maps)

Antes nos aprofundarmos nos detalhes dos principais pontos do DDD, é fundamental que consigamos entender de forma clara seus três pilares e como eles se relacionam.

### Linguagem ubíqua
A linguagem ubíqua, do inglês ubiquitous language, é a linguagem de comum entendimento das pessoas experts das regras do negócio e as pessoas desenvolvedoras. Ou seja, todo vocabulário forma um glossário que reflete conceitos comuns para essas pessoas. 

A definição das palavras que compõem esse glossário é feita em conjunto e é essencial para facilitar todo o processo de desenvolvimento e comunicação, pois, uma vez estabelecida, é muito fácil tirar dúvidas das pessoas envolvidas sabendo que se está falando de um mesmo conceito. 

Vamos levar em consideração o contexto em que será construída uma aplicação de aluguel de bicicletas. Considere o glossário: 

**Bicicletas:** Objeto que será alugado, cujas características serão armazenadas na aplicação

**Usuário/Cliente:** Pessoa que alugará a bicicleta, cujos dados serão armazenados na aplicação

**Perfil:** Espaço na aplicação onde a pessoa visualiza seus dados e pode editá-los

**Estação:** Local físico onde a pessoa poderá retirar sua bicicleta, cujos dados ficam armazenados na aplicação

**Localização:** Entidade responsável por verificar a localização da pessoa usuário no momento do aluguel

**Histórico:** Lista o histórico de aluguéis da pessoa usuária com localização da estação de retirada e de entrega e data/hora do aluguel

**Pagamento:** Parte em que o usuário efetua o pagamento do aluguel único da bicicleta

Observe que, com essas palavras fora de contexto, elas podem significar coisas completamente diferentes. Por isso, ao estabelecer a Linguagem Ubíqua, salva-se o tempo de todas as pessoas envolvidas no projeto, além de facilitar todo o processo de comunicação. 

### Contextos delimitados
Os contextos delimitados (Bounded Contexts), são os contextos com fronteiras bem definidas. Cada contexto da aplicação deve ter responsabilidades bem definidas e uma linguagem ubíqua relacionada a ele. Para elaboração das funcionalidades, é importante a descrição detalhada do escopo de cada história. 

Um exemplo para nossa aplicação de aluguel de bicicletas, considerando o caminho feliz apenas, seria: 

1. Criar uma conta na aplicação.
2. Fazer login na aplicação.
3. Adicionar seus dados para salvar em seu Perfil.
4. Habilitar o GPS para compartilhar a localização com a aplicação. 
5. Visualizar uma mensagem de confirmação se a Estação em que se localiza corresponde à captada pelo GPS. 
6. Habilitar a câmera para captar os dados da Bicicleta via QR Code.
7. Visualizar mensagem de confirmação de dados coletados. 
8. Visualizar tela para preenchimento das informações de Pagamento. 
9. Inserir as informações de Pagamento.
10. Visualizar mensagem de confirmação da Bicicleta liberada.

Uma vez que definimos as informações acima é muito mais fácil delimitar os contextos, definir as entidades da aplicação e as ações particulares de cada uma. Isso permite que os envolvidos tenham uma visão geral do produto e assim direcionar o desenvolvimento pelo domínio, ou seja, utilizando o conceito do DDD. 

### Mapa de contexto
Os mapas de contexto (Context Maps), é o mapeamento dos Bounded Contexts.

<p align="center">
  <img src="https://user-images.githubusercontent.com/40603968/193652102-153e6318-242e-4782-a418-36e0284d4452.png">
</p>

Observe que nesse mapa de contexto existe a relação entre domínios principais e domínios genéricos. Os domínios principais são upstream, ou seja, têm prioridade em relação aos genéricos, que são downstream. Isso significa que na ordem de prioridade, quando alguma coisa mudar, prioritariamente deve partir do lado dos domínios genéricos.

Já na relação entre domínios genéricos, a regra é ditada pelo que não temos autonomia para alterar. Por exemplo, no caso dos domínios de Localização e Estação, considerando que vamos utilizar uma API de Localização do Google, só temos controle sobre as requisições a ela, mas não do seu funcionamento de ponta a ponta. Logo, a depender de como a API de Localização funciona, será definido como será a Estação. Esse tipo de relação é denominada relação conformista. 

Caso haja alguma alteração na API de localização, o que podemos fazer para contornar essa alteração é uma camada de anticorrupção (Anticorruption Layer - ACL), cujo nome é auto explicativo: ela garante que o domínio que utiliza dos serviços de outro (no nosso caso Estação) não seja corrompido pelas alterações desse (a API de Localização). Outra situação que podemos empregar a camada de anticorrupção seria na autenticação, caso ela seja via API. 

> [!NOTE]  
> Não conhece ou quer saber mais sobre o conceito de ACL? Basta acessar nosso documento de arquitetura de referência sobre o tema de [Anticorruption Layer](https://github.com/alcavalcanti/arch-ref/blob/main/Anti-corruption%20Layer.md)

Agora, com os três conceitos DDD bem definidos, fica evidente que DDD se baseia no entendimento dos contextos e seus relacionamentos, fortalecidos da linguagem ubíqua estabelecida. Com isso entendido, podemos partir para entender como modelar nossa aplicação. 

## O que é o Modelo e qual sua utilidade?
Segundo Evans, o modelo é uma abstração de um conceito que define o domínio. É uma interpretação da realidade que abstrai alguns aspectos dela para resolver o problema em questão.

Vamos imaginar a partir do nosso exemplo de uma aplicação para aluguel de bicicletas: são coisas intuitivas que fazem parte do nosso domínio e que determinam o nosso modelo. Por exemplo, a pessoa usuária, o seu pagamento e a própria bicicleta, precisam de abstrações dentro do nosso código para refletir a situação real. 

<p align="center">
  <img src="https://user-images.githubusercontent.com/40603968/193652234-462e0b4a-557e-4037-b7bc-861331d24d7f.png">
</p>

São características de um modelo: 

Permitir a comunicação assertiva entre membros do time, pois o conceito do negócio definido dentro da aplicação aliado à linguagem ubíqua permite que todos participem da construção do modelo. 
Garantir que a especificação das características de cada conceito sejam implementadas.
Definir a estrutura dos conceitos da aplicação de maneira que torna possível a abstração por parte das pessoas desenvolvedoras de outras partes do código, relativas às atividades dos modelos, por exemplo. 
Simplificar os conceitos, permitindo a estruturação do conhecimento de todo o domínio

## O conceito e a aplicação da modelagem evolutiva e mutável 
A modelagem de conceitos é evolutiva e mutável. A cada interação entre as pessoas expertas de domínio e as pessoas desenvolvedoras, o modelo se torna mais profundo com relações e aspectos mais ricos. Assim como também outros modelos podem ser criados e definidos a fim de que a aplicação reflita a realidade da forma mais fiel possível. 

À medida que novas funcionalidades são criadas e novas regras de negócio são adicionadas à aplicação, os modelos podem e devem ser alterados para fazer com que o negócio evolua de maneira fiel à realidade. 

## Utilizando blocos de construção
Para manter toda essa dinâmica de construção é necessário não só uma boa comunicação entre os times, como também a adoção dos blocos de construção da Domain Model Patterns, que tem como foco o desenvolvimento de aplicações a partir de seu domínio. São eles: 

**Entities:** Uma entidade é um objeto potencialmente mutável. As entidades têm vida própria no modelo de domínio, o que permite obter um histórico de transição. 
**Value Objects:** Entidades imutáveis, um exemplo é o endereço de uma Estação.
**Aggregate Objects:** São compostos por uma entidade ou um conjunto de entidades e Value Objects que compartilham um mesmo contexto. Por exemplo, o pagamento e uma transação realizada.
**Repositories:** Fazem a comunicação e garantem a persistência com o armazenamento dados (S3, rabbitMQ, etc.).
**Domain Services:** São os serviços de domínio que implementam as lógicas de negócios estabelecidas pela pessoa especialista de domínio
**Factories:** Oferecem uma abstração na construção de objetos. São uma alternativa para a construção de objetos.
**Services:** São objetos sem estado que executam operações específicas de domínio que podem envolver outros objetos de domínio. 
**Domain Event:** Eventos disparados quando acontece alguma alteração do domínio. Isso ocorre para que outras partes tenham conhecimento da alteração que aconteceu.

> [!WARNING]
> Todos esses conceitos são essenciais para definição do DDD mas existem princípios relacionados a eles que, quando presentes, não necessariamente significam que sua organização utiliza o DDD. 


São princípios de arquiteturas e Design Patterns **independentes do DDD** mas que podem auxiliar o desenvolvimento com DDD: 

* Arquitetura de camadas que isola subdomínios da aplicação em camadas.
* Uso de aggregates para monitorar objetos.
* Isolar responsabilidades a partir de representações bem definidas de modelos (entidades, objetos, módulos, factories, repositórios, etc).

## Como modelar de maneira efetiva
Para construir um modelo efetivo, é importante considerar os seguintes fatores: 

* A implementação deve refletir o modelo real de acordo com a necessidade de cada contexto. 
* Construção de um modelo evolutivo, ou seja, que fica mais profundo e rico em conhecimento à medida que são acrescentadas alterações e novas regras ao domínio. 
* Refinar o modelo adicionando e retirando conceitos à medida que necessário, com as mudanças acrescentadas ao domínio. 
* Estabelecer uma linguagem baseada no modelo entre as pessoas especialistas de domínio e pessoas desenvolvedoras, que seja entendida por ambos. A linguagem é desenvolvida desde a primeira interação mas todos ficam fluentes ao longo do processo. 
* Muita experimentação e estratégias de interações entre pessoas desenvolvedoras e experts de domínio. Quanto mais o domínio fica evidente e a linguagem é bem estabelecida entre o time, mais fácil é o processo de desenvolvimento como um todo. 

## A arquitetura em camadas do Domain Driven Design
Apesar de não andarem sempre juntas, é interessante vermos como é uma arquitetura em camadas em DDD. Para isso, vamos considerar uma arquitetura de exemplo em que temos 5 camadas: 

<p align="center">
  <img src="https://user-images.githubusercontent.com/40603968/193652750-20896100-6894-488e-8595-e5ce8d10d71d.png">
</p>

**Apresentação ou User Interface** é a camada visual que representa a interface com a pessoa usuária (UI). Exemplos: Aplicação Desktop, Aplicação Web, Aplicação Mobile. Essa camada tem referência direta às camadas da Aplicação, Domínio e Infraestrutura. 
**Serviços** é a camada que faz comunicação com outras aplicações e APIs. Exemplos: Web API, WebSockets. 
**Aplicação** é a camada responsável por se comunicar diretamente com o domínio e nela estão implementados: as classes dos serviços da aplicação, interfaces (ou contratos), Data Transfer Objects (DTO) e AutoMapper. 
**Domínio** é onde o DDD acontece, e nela estão: entidades, interfaces para serviços e repositórios, classes dos serviços do domínio e validações.
**Infraestrutura** é camada que dá suporte a todas as demais camadas e pode ser dividida em: repositórios, mapeamento e persistência de dados.

## Vantagens da utilização do DDD
Quais as vantagens do Domain Driven Design?
* Iterações (ciclos) de desenvolvimento mais rápidos
* Alta colaboração entre membros do time 
* Torna o código reutilizável, manutenível e legível 
* Facilita a manutenção da complexidade com a definição da complexidade dos limites definidos

## Downsides
Quais as desvantagens do Domain Driven Design? 

Cada situação é única, mas é importante levar em consideração os seguintes fatores:

* **Complexidade técnica** quando as tecnologias envolvidas já são muito complexas e envolve um esforço grande do time para refatorar o que existe com DDD. Ou mesmo quando dividir um domínio exige divisões em serviços que exigem habilidades técnicas distintas, o DDD pode não ser a melhor opção. 
* **Complexidade de domínio** quando existem muitos subdomínios dentro de um outro, e a manutenção de uma funcionalidade simples exige mexer em muitos subdomínios. 

>[!IMPORTANT]
> Lembre-se de que aplicar o DDD não é apenas separar a arquitetura da sua aplicação em camadas, ele envolve todo o processo de desenvolvimento na organização, incluindo entender o domínio do seu problema em questão, elaborar a linguagem ubíqua, definir os contextos, criar um mapa de contexto correto e então começar a trabalhar na modelagem desses conceitos.

[:arrow_up: Voltar para o início](#Domain-Driven-Design)
