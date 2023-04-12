---
title: Recurso de metadados do usuário
description: Recurso de metadados do usuário
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 0%

---



# Metadados do usuário {#user-metadata}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

</br>
</br>

## Introdução {#intro}

O recurso Metadados do usuário permite que os programadores acessem diferentes tipos de dados específicos do usuário mantidos por MVPDs.  Os tipos de metadados do usuário incluem CEP, classificações dos pais, IDs de usuário e muito mais.  *Usuário* metadados é uma extensão para o disponível anteriormente *estático* metadados (TTL do token de autenticação, TTL do token de autorização e ID do dispositivo).


Pontos principais de metadados do usuário:

- Transmitido ao aplicativo do Programador durante os fluxos de autenticação e autorização
- Os valores são salvos no token
- Os valores podem ser normalizados se diferentes MVPDs fornecerem dados em diferentes formatos
- Alguns parâmetros podem ser criptografados usando a chave do Programador (por exemplo, código postal)
- Valores específicos são disponibilizados pelo Adobe, por meio de uma alteração de configuração

## Obter metadados do usuário {#obtaining}

Os metadados do usuário estão disponíveis para os programadores por meio do AccessEnabler `getMetadata()` e por meio da `/usermetadata` endpoint na API sem cliente.  Consulte a documentação da API da plataforma para obter detalhes sobre como usar o `getMetadata()` e o retorno de chamada correspondente `setMetadataStatus()` (ou para os endpoints e parâmetros usados na API sem cliente).

Os programadores obtêm metadados fornecendo uma chave para o tipo de metadados que desejam obter: `getMetadata(key)`.  

Os metadados são retornados da seguinte maneira: `setMetadataStatus(key, encrypted, data)`:

| Parâmetro | Tipo | Descrição |
| ----------- | ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `key` | String | Especifica o tipo de metadados solicitados |
| `encrypted` | Booleano | Um sinalizador booleano que significa se o &quot;valor&quot; está criptografado ou não. Se isso for &quot;true&quot;, o &quot;valor&quot; será, na verdade, uma representação JSON Web Encrypted do valor real. |
| `data` | Objeto | Um objeto JSON que contém a representação dos metadados |

 

A estrutura do parâmetro de dados, os valores variam entre os tipos:

| Chave | Tipo de valor | Amostra | Descrição |
| --- | --- | --- | --- |
| `zip` | Matriz JSON | \[&quot;77754&quot;, &quot;12345&quot;\] | Código Postal |
| `householdID` | String JSON | &quot;1o7241p&quot; | Identificador da família. Se o MVPD não suportar subcontas, isso será idêntico ao `userID` |
| `maxRating` | Objeto JSON | { MPAA: &quot;NR&quot;, <br>  VCHIP: &quot;X&quot;,  <br>  URL: &quot;http://manage.my/parental&quot; } | Classificação parental máxima para o usuário |
| `userID` | String JSON | &quot;1o7241p&quot; | O identificador do usuário. No caso em que um MVPD suporta subcontas e o usuário não é a conta principal, `userID` será diferente de `householdID`. |
| `channelID` | Matriz JSON | \[&quot;canal-1&quot;, &quot;canal-2&quot; \] | Uma lista de canais que um usuário tem direito a visualizar |
| `is_hoh` | String JSON | &quot;1&quot; | Um sinalizador que identifica se um usuário é chefe de família |
| `encryptedZip` | String JSON | &quot;&quot; | A Comcast expõe o código postal criptografado |
| `typeID` | String JSON | Primário | Um sinalizador que identifica se a conta de usuário é primária/secundária |
| `primaryOID` | String JSON | &quot;uuidd1e19ec9-012c-124f-b520-acaf118d16a0&quot; | Identificador da família. If `typeID` é Primário, conterá o valor da variável `userID` |
| hba_status | Booleano | &quot;true&quot; &quot;false&quot; | Um sinalizador booleano que significa se a autenticação com base em casa está ativada para uma integração específica |
| allowMirroring | Booleano | &quot;true&quot; &quot;false&quot; | Indica se o espelhamento de tela é permitido para este dispositivo ou não |

>[!NOTE]
>
> **Observação:** Se o parâmetro de dados estiver criptografado, como é o caso da variável **chave postal**, a representação da chave de metadados será uma string JSON em vez de uma matriz ou um objeto.


**Importante:** Os metadados de usuário reais disponíveis para um Programador dependem do que um MVPD disponibiliza.  Os contratos legais devem ser assinados com MVPDs antes que metadados de usuário confidenciais (como zipcode) sejam disponibilizados no ambiente de produção.

</br>


| Nome | Detalhes | Requer criptografia | Comentários |
| --- | --- | --- | --- |
| ID de usuário | Conforme fornecido pelo MVPD | Não | Esse é o valor que é então colocado em hash pelo Adobe e exposto no token de mídia e no retorno de chamada sendTrackingData() .<br><br>O hash nesse caso foi feito por motivos históricos<br><br>Essa ID pode ser uma ID de família ou uma ID de subconta. Normalmente não é especificado, é apenas a ID vinculada ao logon que foi usada no momento (que pode ser uma conta primária ou uma subconta) |
| ID de usuário ascendente | Fornecido pelo MVPD para ser usado apenas para fluxos de Monitoramento de Simultaneidade | Não | Esse valor é usado ao impor limites de simultaneidade entre o MVPD e sites e aplicativos do Programador. <br><br>A ID também pode conter políticas de monitoramento de simultaneidade<br><br>Para a maioria dos MVPDs esse valor é igual ao ID do usuário |
| ID de Usuário Doméstico | Fornecido pelo MVPD a utilizar principalmente para os fluxos de controlo parental | Não | ID que permite que os programadores entendam o uso da conta doméstica e da subconta.<br><br>Às vezes, ele é usado como um substituto de Controles dos Pais se as classificações verdadeiras não estiverem disponíveis (Se o usuário tiver feito logon com a conta da família que pode ser assistida, caso contrário, o conteúdo classificado não será exibido)<br><br>Há uma grande variação entre os MVPDs para a forma como isso é representado - ID de usuário doméstico, ID de chefe de família, chefe de pavilhão de família, etc. |
| Chefe de Família | Sinalizador se a conta corrente for o chefe de família ou não | Não | veja acima |
| ID de tipo/ID primária | Identificadores da conta do agregado | Não | Indicadores específicos de AT&amp;T para o chefe de família.<br><br>Tipo ID = Sinalizador que identifica se a conta de usuário é primária/secundária<br><br>OID primário = identificador doméstico. Se TypeID for Primária, conterá o valor de userID |
| Classificação máxima | A classificação máxima permitida para a conta atual | Não | Permite que os Programadores filtrem o conteúdo que não é adequado para a conta.<br><br>Possui classificações MPAA ou VCHIP |
| Linha de Canal para Cima | Lista de canais disponíveis no pacote do usuário | Não | Usado para permitir/remover rapidamente vários canais de portais que agregam várias redes</br></br> *Observe que a autorização de comprovação geralmente permite mais flexibilidade para este caso de uso e deve ser usada* <br><br>A especificação OLCA permite isso como um AttributeStatement na resposta AuthN |
| Status do HBA | Indica se a autenticação ocorreu via HBA | Não |  |
| Código Postal | Código postal de cobrança do usuário | Sim | Usado para transmissão ou eventos esportivos<br><br>Também pode ser fornecido com a resposta AuthZ para atualizações rápidas<br><br>Dados confidenciais, precisam de contratos legais MVPD |
| CEP criptografado | Código postal de cobrança do usuário (Comcast) | Sim | Como acima, mas criptografado por Comcast |
| Idioma | Configurações de idioma do usuário | Não | Usado para exibir mensagens de acordo com as preferências do usuário |
| Permitir Espelhamento | Indica se o espelhamento de tela é permitido para este dispositivo ou não | Não |  |



## Metadados disponíveis {#available_metadata}

A tabela a seguir apresenta o estado atual dos metadados do usuário no ecossistema de autenticação da Adobe Primetime:


|  | **Legal **<br><br>**Acordo **<br><br>**Assinado (somente zip)** | **ID de usuário **<br><br>**no AuthN** | **Zipcode **<br><br>**no AuthN/Z** | **Classificação **<br><br>**no AuthN/Z** | **Famílias **<br><br>**ID em AuthN/Z** | **ID de canal no AuthN** | **Chefe de Família no AuthN** | **Tipo de ID no AuthN** | **OID principal no AuthN** | Idioma | UserID de fluxo **no AuthN** | Status do HBA | OnNet | inHome | Permitir espelhamento no AuthZ | **Notas** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **Nome formal** | n/d | `userID` | `zip` | `maxRating` | `householdID` | `channelID` | is_hoh | typeID | primaryOID | idioma | upstreamUserID | hba_status | onNet | inHome | allowMirroring | 1. Para AuthN - O OiosamlMetadataParser deve ser alterado para que todos os analisadores tenham esse novo atributo ativado <br>2.  Para AuthZ - Não há uma maneira genérica, pois a implementação da autorização é específica do MVPD |
| **Criptografia necessária** | n/d | **Não** | **Sim** | **Não** | **Não** | **Não** | **Não** | **Não** | **Não** | **Não** | **Não** | **Não** | **Não** | **Não** | **Não** |  |
| **Sensível** | n/d | **Não** | **Sim** | **Não** | **Não** | **Não** | **Não** | **Não** | **Não** | **Não** | **Não** | **Não** | **Não** | **Não** |  |  |
| **Adobe IdP** | **Sim** | **Sim** | **Sim (somente AuthN)** | **Sim (somente AuthN)** | **Sim (somente AuthN)** | **Sim** | **Sim** | **Sim** | **Sim** | **Não** | **Sim** | **Não** | **Não** | **Não** | **Não** | Não é necessário nenhum acordo legal, pode ser ativado. |
| **Sincronizador** | **Sim** | **Sim** | **Sim (somente AuthN)** | **Sim (somente AuthN)** | **Sim (somente AuthN)** | **Sim** | **Sim** | **Não** | **Não** | **Não** | **Sim** | **Não** | **Não** | **Não** | **Não** | **Acordo jurídico que não cobre todos os MVPDs proxies.**   <br>Este é um suporte genérico para o Synacor - possivelmente não acumulado em todos os seus MVPDs. |
| Dish | **Não** | **Sim** | **Sim (somente AuthN)** | **Sim (somente AuthN)** | **Sim (somente AuthN)** | **Sim** | **Não** | **Não** | **Não** | **Não** | **Sim** | **Não** | **Não** | **Não** | **Não** | Compartilha a mesma lista de todos os MVPDs de Sinalizador, além de upstreamUserID. |
| Comcast | **Não** | **Sim** | **Não** | **Sim (somente AuthZ)** | **Sim (somente AuthZ)** | **Não** | **Não** | **Não** | **Não** | **Não** | **Sim** | **Sim** | **Não** | **Não** | **Não** |  |
| **AT&amp;T** | **Sim** | **Sim** | **Sim (somente AuthN)** | **Não** | **Sim (somente AuthN)** | **Não** | **Não** | **Sim** | **Sim** | **Não** | **Sim** | **Não** | **Não** | **Não** | **Não** | Acordo jurídico assinado. |
| **Cablevision** | **Sim** | **Sim** | **Sim (somente AuthN)** | **Não** | **Não** | **Sim** | **Não** | **Não** | **Não** | **Não** | **Sim** | **Não** | **Não** | **Não** | **Não** | Acordo jurídico assinado. |
| **HTC** | **Não** | **Sim** | **Não** | **Não** | **Não** | **Sim** | **Não** | **Não** | **Não** | **Não** | **Sim** | **Não** | **Não** | **Não** | **Não** |  |
| **Proxy Massilon** | **Sim** | **Sim** | **Sim (somente AuthN)** | **Não** | **Sim (somente AuthN)** | **Não** | **Não** | **Não** | **Não** | **Não** | **Sim** | **Não** | **Não** | **Não** | **Não** | Acordo jurídico assinado. |
| **Clearleap de Proxy** | **Sim** | **Sim** | **Sim (somente AuthN)** | **Sim (somente AuthZ)** | **Não** | **Não** | **Não** | **Não** | **Não** | **Sim** | **Sim** | **Não** | **Não** | **Não** | **Não** | Acordo jurídico assinado. |
| Rogers | **Não** | **Sim** | **Não** | **Não** | **Não** | **Não** | **Não** | **Não** | **Não** | **Não** | **Sim** | **Não** | **Não** | **Não** | **Não** |  |
| RCN | **Sim** | **Sim** | **Sim (somente AuthN)** | **Sim (somente AuthN)** | **Sim (somente AuthN)** | **Não** | **Não** | **Não** | **Não** | **Não** | **Sim** | **Não** | **Não** | **Não** | **Não** |  |
| Carta | **Sim** | **Sim** | **Sim (somente AuthN)** | **Sim (somente AuthN)** | **Sim (somente AuthN)** | **Não** | **Não** | **Não** | **Não** | **Não** | **Sim** | **Não** | **Não** | **Não** | **Não** |  |
| Verizon | **Não** | **Sim** | **Sim (somente AuthN)** | **Não** | **Não** | **Não** | **Não** | **Não** | **Não** | **Não** | **Sim** | **Sim** | **Não** | **Não** | **Não** |  |
| Eastlink | **Não** | **Sim** | **Sim (somente AuthN)** | **Sim (somente AuthN)** | **Sim (somente AuthN)** | **Sim** | **Não** | **Não** | **Não** | **Não** | **Sim** | **Não** | **Não** | **Não** | **Não** |  |
| GLDS de Proxy | **Não** | **Sim** | **Sim (somente AuthN)** | **Não** | **Não** | **Não** | **Não** | **Não** | **Não** | **Não** | **Sim** | **Não** | **Não** | **Não** | **Não** |  |
| DTV | **Sim** | **Sim** | **Sim (somente AuthN)** | **Não** | **Não** | **Não** | **Não** | **Não** | **Não** | **Não** | **Sim** | **Não** | **Não** | **Não** | **Não** |  |
| COX | **Não** | **Sim** | **Sim (somente AuthN)** | **Não** | **Não** | **Não** | **Não** | **Não** | **Não** | **Não** | **Sim** | **Não** | **Não** | **Não** | **Não** |  |
| Cogeco | **Não** | **Sim** | **Sim (somente AuthN)** | **Não** | **Sim (somente AuthN)** | **Não** | **Não** | **Não** | **Não** | **Não** | **Sim** | **Não** | **Não** | **Não** | **Não** |  |
| Videotron | **Não** | **Sim** | **Sim (somente AuthN)** | **Não** | **Sim*** | **Não** | **Não** | **Não** | **Não** | **Não** | **Sim** | **Não** | **Não** | **Não** | **Não** | Expõe householdID com o mesmo valor de userID |
| Espectro | **Sim** | **Sim** | **Sim (somente AuthN)** | **Sim (somente AuthN)** | **Sim (somente AuthN)** | **Não** | **Não** | **Não** | **Não** | **Não** | **Sim** | **Sim** | **Não** | **Não** | **Sim** |  |
| **Todos os outros **<br><br>**MVPDs** | **Não** | **Sim** | **Não** | **Não** | **Não** | **Não** | **Não** | **Não** | **Não** | **Não** | **Sim** | **Não** | **Não** | **Não** | **Não** | **Nenhum acordo legal ainda, metadados confidenciais não disponíveis para produção.**  <br>Para todos os MVPDs, a ID do usuário está disponível sem trabalho extra. |


A lista de tipos de metadados do usuário será expandida à medida que novos tipos forem disponibilizados e adicionados ao sistema de autenticação da Adobe Primetime.

## Amostras de código {#code_samples}

- [Amostra de código 1](#code_sample1)
- [Amostra de código 2 (Mock getMetadata)](#code_sample2)


### Amostra de código 1 {#code_sample1}

```
    // Assuming a reference to the AccessEnabler has been previously obtained and stored in the "ae" variable
     
    ae.setRequestor("SITE");
    ae.checkAuthentication();
     
    function setAuthenticationStatus(status, reason) {
      if(status ==1) {
        // User is authenticated, request metadata
        ae.getMetadata("zip");
        ae.getMetadata("maxRating");
      } else {
        ...
      }
    }
     
    // Implement the setMetadataStatus() callback
    function setMetadataStatus(key, encrypted, data) {
      if(encrypted) {
        // The metadata value is encrypted
        // Needs to be decrypted by the programmer
         data = decrypt(data);
      }
      alert(key + "=" + data);
    }
```
 

### Amostra de código 2 (Mock getMetadata) {#code_sample2}

```
    // Assuming a reference to the AccessEnabler has been
    //   previously obtained and stored in the "ae" variable
     
    // Mock the getMetadata() method
    var aeMock = {
        getMetadata: function(key) {
          var data = null;
          // Set mock data based on the received key,
          // according to the format in the spec
          switch(key) {
            case 'zip': 
              data = [ "1235", "23456" ];
              break;
            case 'maxRating': 
              data = { "MPAA": "PG-13", "VCHIP": "TV-14" };
              break;
            default:
              break;
          }
          // Call the metadata status just like AccessEnabler does
          setMetadataStatus(key, false, data);
        }
     }
     
    ae.setRequestor("SITE");
    ae.checkAuthentication();
     
    function setAuthenticationStatus(status, reason) {
      if (status == 1) {
        // User is authenticated, request metadata using mock object
        aeMock.getMetadata("zip");
        aeMock.getMetadata("maxRating");
      } else {
        ...
      }
    }
     
    // Implement the  setMetadataStatus() callback
    function setMetadataStatus(key, encrypted, data) {
      if (encrypted) {
        // The metadata value is encrypted, so it
        //   needs to be decrypted by the programmer
         data = decrypt(data);
      }
      alert(key + "=" + data);
    }
```
 

Para obter detalhes sobre sua plataforma específica ou obter informações sobre como os Metadados do usuário são processados no MVPD, consulte o link apropriado em Informações relacionadas abaixo.  

<!---

## Related Information {#related}

- ActionScript - [getMetadata()](#getMeta), [setMetadataStatus()](#setMetaData)
- JavaScript - [getMetadata()](#getMeta), [setMetadataStatus()](#setMetaData)
- iOS - [getMetadata()](#getMeta), [setMetadataStatus()](#setMetaStatus)
- Android - [getMetadata()](#getMetadata), [setMetadataStatus()](#setMetadaStatus)
- Clientless - [AuthN Metadata](#authn_metadata)
- [MVPD Integration Guide: User Metadata Exchange](/help/authentication/mvpd-user-metadata-exchng.md)
-->
