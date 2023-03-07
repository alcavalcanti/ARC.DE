# Anti-corruption Layer

###### tags: `acl` `ddd` `anti` `corruption` `layer` `camada` `anticorrupção`

> ###### Esse conteúdo é baseado na abordagem de ACL de [Vaughn Vernon do livro Domain-Driven Design Distilled](https://www.amazon.com.br/Domain-Driven-Design-Distilled-Vaughn-Vernon/dp/0134434420/ref=asc_df_0134434420/?tag=googleshopp00-20&linkCode=df0&hvadid=379735814613&hvpos=&hvnetw=g&hvrand=2005807085629592401&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=1001773&hvtargid=pla-451410218303&psc=1) também conhecido como Green Book.
> ###### Esse conteúdo também é baseado na abordagem de ACL de [Neal Ford do livro Building Evolutionary Architectures (cap. 6 e cap. 7).](https://www.amazon.com.br/Building-Evolutionary-Architectures-Neal-Ford/dp/1491986360/ref=asc_df_1491986360/?tag=googleshopp00-20&linkCode=df0&hvadid=379795170134&hvpos=&hvnetw=g&hvrand=5556893434825774845&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=1001773&hvtargid=pla-380563455104&psc=1)
> ###### Esse conteúdo também é baseado na [documentação oficial de arquiteturas da Microsoft sobre ACL e suas possíveis implementações.](https://docs.microsoft.com/pt-br/azure/architecture/patterns/anti-corruption-layer)
---
#### Índice

[ToC]
## O que é a Anti-corruption Layer (ACL)

Anti-corruption Layer (ACL) é um padrão de arquitetura de abordagem defensiva que tem como proposta isolar um modelo de domínio de todas as suas respectivas integrações (microsserviços de terceiros, monólitos, aplicações de semântica diferentes etc.) movendo todos os recursos destinados a essa integração para uma camada de responsabilidade única que agrupa e gerencia todas as requisições entre as partes, reduzindo ou eliminando o alto acoplamento e dependências desnecessárias existente. **É importante ressaltar que esse desacoplamento também deve ser interpretado a nível de negócio.** Na grande maioria das integrações intersistêmicas existentes atualmente, independente se são internas ou externas a organização não há a necessidade dos negócios estarem atrelados.

### Contexto e possíveis problemas

Rotineiramente nos deparamos com cenários onde aplicações dependem de outras, seja para enriquecimento de informação ou funcionalidade e por esse motivo estão integradas e consequentemente acopladas, essa dependência pode gerar diversos problemas, alguns deles estão listados abaixo:
 - [Uma API sem versionamento é atualizada pelo fornecedor quebrando o contrato e a compatibilidade.](#Cenário-1---Atualização-de-API-sem-versionamento:)
 - [Um serviço de um terceiro de um terceiro fica indisponível.](#Cenário-2---Serviço-de-terceiros-com-indiponibilidade:)
 - Bibliotecas utilizadas mudam sua interface pública quebrando a compatibilidade.
 - Sistemas modernos precisam se comunicar com sistemas legados ou monólitos, necessitando assim de adaptações, traduções ou ajustes no transporte da informação trocada.
 - Alta dependência entre contextos exigindo sincronização de comunicação que pode gerar gargalos e custos para o alinhamento. 

### Entendendo a solução

Para lidar com os problemas exemplificados anteriormente, posicionamos uma camada anticorrupção entre os domínios, essa camada move as comunicações entre as partes, isolando o domínio e permitindo que ele permaneça inalterado, evitando assim comprometer seu comportamento, design e sua abordagem tecnológica, em resumo, impedindo sua corrupção.

![ACL-2022-06-21-1103](https://user-images.githubusercontent.com/107938412/175965171-8f222065-c95f-4476-8f5b-8ddde9a16d3a.png)

O desenho acima mostra uma representação simplificada da ACL em uma comunicação entre dois domínios, um deles (*Domínio B*) sendo de uma fonte terceira. 


:::info
:bulb: **Dica:** A proposta do pattern da ACL é agrupar toda a lógica de comunicação entre os domínios (Adapters, Façades, Translators etc.) e a camada pode ser implementada como um componente da aplicação ou como um serviço independente.
:::

### Cuidados e considerações
Ao implementar uma camada anticorrupção é preciso estar ciente e tomar alguns cuidados, os mais relevantes estão listados a seguir:

- Considere como a camada anticorrupção será dimensionada.
- A camada anticorrupção, se não for corretamente dimensionada e construída, pode adicionar latência para chamadas feitas entre as partes.
- A camada anticorrupção adiciona outro serviço ao domínio que deve ser gerenciado e mantido.
- Considere se você precisa de mais de uma camada anticorrupção. Em alguns casos pode ser interessante decompor a funcionalidade em vários serviços considerando por exemplo a afinidade das tecnologias ou o uso de linguagens diferentes.
- Considere como a camada anticorrupção será gerenciada em relação a outros aplicativos ou serviços. Por exemplo, como ela será integrada aos processos de monitoramento, versão e configuração da organização.
- Certifique-se de que a transação e a consistência das informações sejam mantidas e que possam ser monitoradas.
- Leve em consideração se a camada anticorrupção precisa lidar com toda a comunicação entre diferentes microsserviços ou apenas com alguns recursos.
- Se a camada anticorrupção fizer parte de uma estratégia de migração, leve em consideração se ela será permanente ou se perderá o sentido depois que todas as funcionalidades herdadas forem migradas.

### Quando utilizar esse padrão

Como diversos outros padrões de arquitetura, não existe uma convenção formal sobre a utilização da ACL. Vaughn Vernon ao abordar o tema no livro Domain Driven Design Distilled, diz que sempre que possível devemos utilizar a ACL entre o downstream model e upstream integration model, pois assim podemos produzir conceitos de modelo do nosso lado da integração que são específicos e se encaixam apenas ao nosso negócio, **provendo assim um isolamento completo de interferências externas**.
Já a abordagem da ACL na documentação de padrões de arquiteturas oficial da Microsoft, são citados cenários bem mais específicos como: ¹ Planos de migrações em estágios, onde integrações precisam ser mantidas e herdadas. ² Situações em que dois ou mais microsserviços com semânticas diferentes precisam se comunicar.

## EXTRA: Representações visuais
Com o intuito de facilitar o entendimento de alguns dos problemas abordados em [Contexto e possíveis problemas](#Contexto-e-possíveis-problemas), criei representações visuais detalhadas abaixo:

### Cenário 1 - Atualização de API sem versionamento
Uma informação consumida pelo nosso domínio está integrada diretamente ao terceiro que a disponibiliza:

![scene1_apiupdate-2022-06-21-1504](https://user-images.githubusercontent.com/107938412/174872002-39e5df16-24b1-4e0c-ade7-95381c168547.png)

O fornecedor da informação decide atualizar a API consumida pelo Domínio A, sem versionamento e muda a estrutura do JSON trafegado adicionando informações que não tem relevância para o nosso negócio:

![scene1_apiupdate_broken-2022-06-21-1504](https://user-images.githubusercontent.com/107938412/174872033-9e82c71a-ba3b-4f6b-b591-813209f318b6.png)

Em uma integração direta podemos observar que os Microsserviços do domínio A, que dependem dessa informação param de funcionar como deveriam por estarem altamente acoplados. Além disso, precisaríamos corrigir esse comportamento em dois Microsserviços distintos, alterando a lógica de ambos para passar a entender a nova estrutura trafegada.

A seguir uma representação do mesmo cenário, porém com uma camada de ACL entre a comunicação das partes:

![scene1_apiupdate_broken_withACL-2022-06-21-1504](https://user-images.githubusercontent.com/107938412/175048096-04aa456c-536a-4486-87ee-d5e2d2bda207.png)
Já nessa situação podemos ver que apenas a camada de ACL é parcialmente afetada, a manutenção fica centralizada em um único ponto, os nossos serviços no Domínio A, permanecem íntegros e conseguimos traduzir ou adaptar essa informação trafegada na ACL para a nossa necessidade interna específica.

[:arrow_left: Voltar para Contexto e possíveis problemas](#Contexto-e-possíveis-problemas)

### Cenário 2 - Serviço de terceiros com indisponibilidade
Uma comunicação entre os nossos serviços e o de um terceiro está diretamente integrada:

![scene2_broken_thid_part_service-2022-06-22-1048](https://user-images.githubusercontent.com/107938412/175966646-1d76a221-c64e-4b8a-abad-dbea5671d270.png)

Agora vamos supor que alguma razão o serviço do terceiro fica indisponível. Observamos que toda a nossa parte que está acoplada àquele serviço será afetada e ficará indisponível:

![scene2_broken_thid_part_service_lost_connection-2022-06-22-1048](https://user-images.githubusercontent.com/107938412/175966629-890d3adc-93a2-46c7-b0dd-d5ab82b6de17.png)

Vamos observar como seria essa situação caso a arquitetura tivesse a camada de ACL implementada:

![scene2_broken_thid_part_service_lost_connection_ACL-2022-06-22-1048](https://user-images.githubusercontent.com/107938412/175965329-6e6960b3-e10f-482b-8f7e-8b1be2689e18.png)

Podemos ver que a ACL isola e protege o nosso lado da integração, assim como no caso anterior a camada é parcialmente afetada, mas nossos serviços no domínio A permanecem de pé.

## Implementando uma ACL

1. Crie uma classe para representar o modelo de dados do sistema externo. Vamos chamar essa classe de ***ExternalSystemData***.

```c#
public class ExternalSystemData
{
    public string Data1 { get; set; }
    public string Data2 { get; set; }
    // ... outras propriedades
}
```

2. Crie uma classe para representar o modelo de dados de seu aplicativo principal. Vamos chamar essa classe de ***InternalData***.

```c#
public class InternalData
{
    public string DataA { get; set; }
    public string DataB { get; set; }
    // ... outras propriedades
}
```
3. Crie uma classe para a ACL. Vamos chamar essa classe de ***AntiCorruptionLayer***. Esta classe terá métodos para transformar dados do modelo de dados do sistema externo para o modelo de dados do aplicativo principal e vice-versa.

```c#
public class AntiCorruptionLayer
{
    public InternalData MapFromExternalSystemData(ExternalSystemData externalSystemData)
    {
        return new InternalData
        {
            DataA = externalSystemData.Data1,
            DataB = externalSystemData.Data2
            // ... mapeie outras propriedades
        };
    }

    public ExternalSystemData MapToExternalSystemData(InternalData internalData)
    {
        return new ExternalSystemData
        {
            Data1 = internalData.DataA,
            Data2 = internalData.DataB
            // ... mapeie outras propriedades
        };
    }
}
```
4. Use a ACL em seu aplicativo principal. Sempre precisar interagir com o sistema externo, use a ACL para transformar os dados entre os dois sistemas.
```scss
AntiCorruptionLayer acl = new AntiCorruptionLayer();

// Faça um de para da informação do sistema externo para o principal
ExternalSystemData externalSystemData = GetDataFromExternalSystem();
InternalData internalData = acl.MapFromExternalSystemData(externalSystemData);

// Faça um de para no sentido oposto, do sistema principal para o externo
InternalData updatedInternalData = GetUpdatedInternalData();
ExternalSystemData updatedExternalSystemData = acl.MapToExternalSystemData(updatedInternalData);
SaveDataToExternalSystem(updatedExternalSystemData); }
}
```

E lembre-se:

Esse é apenas um exemplo simples para demonstrar como você pode criar uma ACL em C#. Em um aplicativo do mundo real, você provavelmente teria modelos de dados e transformações mais complexos. 

A ideia principal é usar a ACL para separar o restante do aplicativo das alterações no modelo de dados do sistema externo, facilitando a manutenção do aplicativo e a adaptação às alterações no sistema externo ao longo do tempo.

[:arrow_left: Voltar para Contexto e possíveis problemas](#Contexto-e-possíveis-problemas)

[:arrow_up: Voltar para o início](#Anti-corruption-Layer)

> Deixem comentários e sugestões! :rocket: [color=#3b75c6]
