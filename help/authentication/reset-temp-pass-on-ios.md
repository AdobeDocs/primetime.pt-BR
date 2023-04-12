---
title: Redefinir aprovação temporária no iOS
description: Redefinir aprovação temporária no iOS
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 0%

---


# Redefinir aprovação temporária no iOS {#reset-temp-pass-on-ios}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

</br>

O aplicativo de demonstração do iOS inclui uma tela dedicada para redefinir o TTL de passagem temporária. As seguintes informações são necessárias para a operação de redefinição:

- **Ambiente:** especifica o ponto de extremidade do servidor de passagem Adobe Pay-TV que receberá a chamada de rede Temp Pass de redefinição. Valores possíveis: **Prequal** (*mgmt-prequal.auth-staging.adobe.com*), **Versão** (*mgmt.auth.adobe.com*) ou **Personalizado** (reservado para teste interno de Adobe).
- **Token do portador OAuth2:** o token OAuth2 é necessário para autorizar o Programador para autenticação Adobe Pay-TV. Esse token pode ser obtido a partir do terminal OAuth2 de autenticação Pay-TV dedicado (por exemplo, *curl -u &quot;\&lt;consumer _key=&quot;&quot;>:\&lt;consumer _secret=&quot;&quot; _key=&quot;&quot;>*&quot; *&quot;https://mgmt.auth.adobe.com/oauth2/permanent\_access stoken?grant\_type=client\_credentials&quot;*).
- **ID do solicitante:** a ID exclusiva do programador atual. Esse valor é lido da tela principal do Demo App (o campo do solicitante).
- **ID de aprovação temporária:** a ID exclusiva para o MVPD de aprovação de modelo.
- **ID do dispositivo:** ID de dispositivo com hash calculada pelo aplicativo de demonstração.
- **Chave genérica:** alguns MVPDs de passagem temporária (ou seja, a próxima funcionalidade de passagem temporária extensível) são compatíveis com uma chave genérica para redefinir a passagem temporária (junto com a ID do dispositivo).

Todos os parâmetros acima (exceto o *Chave genérica*) são obrigatórias. Este é um exemplo de parâmetros e a chamada de rede associada que será executada pelo Demo App (o exemplo está no formato de um comando *curl *):

- **Ambiente:** Versão (*mgmt.auth.adobe.com*)
- **Token do portador OAuth2:** H4j7cF3GtJX81BrsgDa10GwSizVz
- **ID do programador:** REF
- **ID de aprovação temporária:** TempPassREF
- **ID do dispositivo:** f23804a37802993fdc8e28a7f244dfe088b6a9ea21457670728e6731fa6399 91º 
- **Chave genérica:** null (nenhum valor fornecido)

```curl
curl -X DELETE -H "Authorization:Bearer* *H4j7cF3GtJX81BrsgDa10GwSizVz" "https://mgmt.auth.adobe.com/reset-tempass/v2.1/reset?device_id=f23804a37802993fdc8e28a7f244dfe088b6a9ea21457670728e6731fa639991&requestor_id=REF&mvpd_id=TempPassREF"
```

será feita uma solicitação DELETE HTTP para **/reset** endpoint, transmitindo a variável *Token de portador OAuth2* no cabeçalho Autorização e na *ID do dispositivo*, *ID do solicitante* e *ID de Passe Temp (ID MVPD)* como parâmetros.

Se o Programador fornecer um valor para a variável *Chave genérica*, outra chamada HTTP será executada (desta vez para o **/reset/generic** endpoint), transmitindo o *Chave genérica* dentro do *key* parâmetro de solicitação.

Por exemplo, definir a variável *Chave genérica* para um hash de endereço de email (para MVPDs de passagem temporária que oferecem suporte a esse tipo de funcionalidade) produzirá a seguinte chamada HTTP (o email é `user@domain.com` seu hash SHA-256 é `f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7`):

```curl
curl -X DELETE -H "Authorization:Bearer H4j7cF3GtJX81BrsgDa10GwSizVz"
"https://mgmt.auth.adobe.com/reset-tempass/v2.1/reset/generic?key=f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7&requestor_id=REF&mvpd_id=TempPassREF"
```

É importante enfatizar que a redefinição do Temp Pass no Aplicativo de demonstração pode não ter o mesmo efeito para um aplicativo programador no mesmo dispositivo. Isso se deve ao fato de que a ID do dispositivo (como calculada pelo aplicativo de demonstração e pelo AccessEnabler) pode não ser a mesma para todos os aplicativos no dispositivo:

- iOS 6 e inferior: a ID do dispositivo é calculada usando o endereço MAC (exclusivo para todos os aplicativos), portanto, redefinir a aprovação de modelo no aplicativo de demonstração redefinirá em todos os outros aplicativos do programador no dispositivo.

- iOS 7 e superior: a ID do dispositivo é calculada com base no valor IDFV (ID para fornecedor), que é exclusivo para todos os aplicativos que têm o mesmo prefixo de ID do pacote (ou seja, todos os componentes exceto o último). Como o aplicativo de demonstração e um aplicativo programador têm IDs de pacote diferentes, a redefinição do Temp Pass no aplicativo de demonstração não terá efeito em um aplicativo programador.

O último caso de uso (iOS 7 e superior) é o mais comum, portanto, vamos ver como os programadores podem redefinir o Temp Pass para seus aplicativos nesta situação. Há várias opções:

1. Coloque o código do aplicativo Demo no aplicativo programador. O *TempPassResetViewController* e *DeviceIdDemoApp* As classes contêm a lógica principal para redefinir o Temp Pass, e podem ser facilmente modificadas e incluídas no aplicativo Programador.

1. Execute a solicitação HTTP para redefinir o Temp Pass com *curl*. O parâmetro device\_Id pode ser obtido calculando o IDFV do aplicativo Programador e aplicando um hash SHA-256 sobre ele (código de amostra no *DeviceIdDemoApp* classe ).

1. Basta executar a redefinição no aplicativo de demonstração especificando o IDFV com hash do aplicativo do programador como *Chave genérica*. Isso resultará em duas chamadas de rede: um para redefinir o Temp Pass for the Demo App (irrelevante para o programador) e outro para redefinir o Temp Pass for the Programmer app.

Todas as opções acima são semelhantes, depende do Programador escolher uma, dependendo da facilidade de implementação. 

