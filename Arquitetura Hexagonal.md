
# Arquitetura Hexagonal

###### tags: `hexagonal` `arquitetura` `architecture` 

> ###### Esse conteúdo é baseado no artigo do Alistair Cockburn [Hexagonal Architecture](https://www.amazon.com.br/Domain-Driven-Design-Distilled-Vaughn-Vernon/dp/0134434420/ref=asc_df_0134434420/?tag=googleshopp00-20&linkCode=df0&hvadid=379735814613&hvpos=&hvnetw=g&hvrand=2005807085629592401&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=1001773&hvtargid=pla-451410218303&psc=1) criador do padrão de arquitetura hexagonal.
> ###### Também interpretamos conceitos abordados no livro [Engenharia de Software Moderna](https://www.amazon.com.br/gp/product/6500019504) de Marco Tulio Valente.

---
#### Índice

**Sumário**
- [O que é o padrão de arquitetura hexagonal](#o-que-é-o-padrão-de-arquitetura-hexagonal)
    - [Como identificar os atores](#como-identificar-os-atores)
    - [O centro do hexágono](#o-centro-do-hexágono)
    - [Lado esquerdo do hexágono](#lado-esquerdo-do-hexágono)
    - [Lado direito do hexágono](#lado-direito-do-hexágono)
    - [Adaptadores e portas](#adaptadores-e-portas)
- [Implementando a arquitetura hexagonal](#implementando-a-arquitetura-hexagonal)


## O que é o padrão de arquitetura hexagonal

O padrão de Arquitetura Hexagonal também é comumente conhecido como o padrão de portas e adaptadores.
Uma das razões citadas por Alistair para a proposta foi delegar a infra-estrutura e user interface (UI) parte do projeto, concentrar-se nas regras de negócios e torná-las tangíveis e funcionais, além de prover isolamento entre as partes, ou seja, **em uma Arquitetura Hexagonal, classes de domínio não devem depender de classes relacionadas com infraestrutura, tecnologias ou sistemas externos**. A vantagem dessa divisão é desacoplar esses dois tipos de classes.

> [!NOTE]
> Crie sua aplicação para trabalhar sem uma UI ou banco de dados, assim você pode executar testes automáticos de regressão, implementar quando o banco de dados não estiver disponível e conectar aplicações sem acopla-las. (Alistair Cockburn)

Assim, as classes de domínio não conhecem as tecnologias – bancos de dados, interfaces com usuário e quaisquer outras bibliotecas – usadas pelo sistema. Consequentemente, mudanças de tecnologia podem ser feitas sem impactar as classes de domínio. Talvez ainda mais importante, as classes de domínio podem ser compartilhadas por mais de uma tecnologia. Por exemplo, um sistema pode ter diversas interfaces (Web, mobile, etc).

Visualmente, a arquitetura é representada por meio de dois hexágonos concêntricos (veja figura). No hexágono interno, ficam as classes do domínio (ou classes de negócio, se você preferir). No hexágono externo, ficam os adaptadores. Por fim, as classes de interface com o usuário, classes de tecnologia ou de sistemas externos ficam fora desses dois hexágonos.

<p align="center">
  <img  src="https://user-images.githubusercontent.com/40603968/184912008-4ae23df5-c060-4538-836d-79fff5327d4c.png">
</p>

Agora que entendemos mais sobre o desenho e a proposta hexagonal, podemos subdividir o conceito em três partes:

* [Centro do Hexágono](#O-centro-do-hexágono)
* [Lado esquerdo do hexágono](#Lado-esquerdo-do-hexágono)
* [Lado direito do hexágono](#Lado-direito-do-hexágono)

Neste subdivisão temos os atores que irão interagir com o centro do hexágono:

O ator principal, que iniciará e conduzirá uma ação;
O ator secundário a ser liderado.

### Como identificar os atores
A identificação dos atores é mais simples do que parece. O **ator principal**, é a parte protagonista do fluxo, quem o inicia e a causa para que demais ações sejam tomadas, por exemplo o usuário, pressionando um botão na nossa aplicação. Já o **ator secundário** é a parte secundária do fluxo, é a consequência, quem realiza as ações necessárias para atender o que o ator principal requisitou.

### O centro do hexágono
É onde estão localizados os modelos, domínios e regras de negócios da nossa aplicação. É um ambiente que deve ser totalmente isolado, em termos de não ser afetado por ocorrências externas, por exemplo, o banco de dados que será utilizado, framework frontend, etc.

### Lado esquerdo do hexágono
É o lado do ator principal, o responsável por iniciar o fluxo, não importa se é uma pessoa, outro sistema, um script em bash que chama seu adapter, se dispara um gatilho que chama o core business de sua aplicação, então ele é o ator principal.

### Lado direito do hexágono
É o lado do ator secundário, o ator que será conduzido a realizar uma determinada ação que o ator primário tenha desencadeado. Pode ser gravar dados, registrar logs, ou mesmo chamar uma terceira aplicação e obter uma resposta, retornando uma resposta ao ator primário.

### Adaptadores e portas
Em uma Arquitetura Hexagonal, o termo porta designa as interfaces usadas para comunicação com as classes de domínio (veja que interface aqui significa interface de programação; por exemplo, uma interface de .Net).

Existem dois tipos de portas:

**Portas de entrada:** são interfaces usadas para comunicação de fora para dentro, isto é, quando uma classe externa precisa chamar um método de uma classe de domínio. Logo, essas portas declaram os serviços providos pelo sistema, isto é, serviços que o sistema oferece para o mundo exterior.

**Portas de saída:** são interfaces usadas para comunicação de dentro para fora, isto é, quando uma classe de domínio precisa chamar um método de uma classe externa. Logo, essas portas declaram os serviços requeridos pelo sistema, isto é, serviços do mundo exterior que são necessários para o funcionamento do sistema.

> [!IMPORTANT]
> É importante lembrar que as portas são independentes de tecnologia. Portanto, elas estão localizadas no hexágono central, o núcleo.

**Adapters:**
Os adaptadores são os usuários das portas. Para cada porta que seu hexágono possui, um adaptador deve ser criado, portanto, você tem a liberdade de modificá-lo e apagá-lo dinamicamente. Em portas e adaptadores, temos também o conceito de portas primárias e secundárias, e o conceito é o mesmo utilizado com os atores.

Nos atores primários de nossa aplicação temos os condutores da ação, que utilizarão os adaptadores primários, e isto "baterá" nas portas primárias. Assim, as portas secundárias e os adaptadores conduzirão a ação até o ator secundário no fluxo contínuo da aplicação.

Por outro lado, os sistemas externos, normalmente, usam alguma tecnologia, seja ela de comunicação (REST, gRPC, GraphQL, etc), de bancos de dados (SQL, noSQL, etc), de interação com o usuário (Web, mobile, etc), etc.

Daí a necessidade de componentes localizados no hexágono mais externo da arquitetura **os adaptadores**, os quais atuam de um dos dois modos a seguir:

Eles recebem chamadas de métodos vindas de fora do sistema e encaminham essas chamadas para métodos adequados das portas de entrada.

Eles recebem chamadas vindas de dentro do sistema, isto é, das classes de domínio, e as direcionam para um sistema externo, tais como um banco de dados, um outro sistema da organização ou mesmo de terceiros.


Um exemplo um pouco mais elaborado de uma aplicação completa:

![hexagonal_full_application_sample](https://user-images.githubusercontent.com/40603968/188504321-8e7eae39-9a79-4637-9893-533658232704.png)

## Implementando a arquitetura hexagonal

Veja como poderíamos estruturar uma aplicação metereologica seguindo o padrão Ports and Adapters:

**Ports:**
Definimos uma interface ***WeatherDataProvider*** que descreve os métodos que nosso aplicativo precisa para recuperar dados meteorológicos.

```c#
public interface IWeatherDataProvider
{
    WeatherData GetWeatherData(string location);
}
```

**Adapters:**
Criamos uma implementação do ***WeatherDataProvider*** que recupera dados da API remota. Vamos chamá-lo de ***RemoteWeatherDataProvider***.

```c#
public class RemoteWeatherDataProvider : IWeatherDataProvider
{
    public WeatherData GetWeatherData(string location)
    {
        // Code to retrieve data from the remote API
    }
}
```

**Core application:**
Nosso aplicativo principal depende apenas da interface ***WeatherDataProvider*** e pode usar qualquer implementação dela, incluindo ***RemoteWeatherDataProvider*** ou qualquer outra.

```c#
public class WeatherApp
{
    private readonly IWeatherDataProvider _weatherDataProvider;

    public WeatherApp(IWeatherDataProvider weatherDataProvider)
    {
        _weatherDataProvider = weatherDataProvider;
    }

    public void DisplayWeather(string location)
    {
        WeatherData weatherData = _weatherDataProvider.GetWeatherData(location);
        // Code to display the weather data
    }
}
```

Essa estrutura nos permite alterar a implementação do ***WeatherDataProvider***, por exemplo, para um provedor de dados local, sem alterar a aplicação principal. Além disso, torna mais fácil testar nossa aplicação principal usando uma implementação diferente do ***WeatherDataProvider*** que retorna dados predefinidos.

Observe que este é um exemplo muito simples para ilustrar o conceito de arquitetura de portas e adaptadores. Em uma aplicação do mundo real, você pode e provavelmente terá várias portas e a implementação dos adaptadores consequentemente também será mais complexa.

[:arrow_up: Voltar para o início](#o-que-é-o-padrão-de-arquitetura-hexagonal)
