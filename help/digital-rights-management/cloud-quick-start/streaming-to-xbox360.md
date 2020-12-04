---
description: nulo
seo-description: nulo
seo-title: Defina o token XSTS no player
title: Defina o token XSTS no player
uuid: 8995e029-deee-4e23-9cda-a50de8c4f2c0
translation-type: tm+mt
source-git-commit: c37061c116b8a6bc8ce085dc89dc8aadd0a2e490
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 0%

---


# Transmissão para Xbox360 (opcional) {#streaming-to-xboc360}

O Primetime DRM está disponível na plataforma Xbox360. No entanto, somente o caso de uso do Protected Streaming é suportado, não o conjunto completo de direitos de política de DRM. Não há suporte para direitos de política de DRM sem streaming, como Grupos de domínio de dispositivo. O Xbox360 ignora direitos não suportados ao tentar reproduzir conteúdo.

Os direitos de política de DRM Primetime suportados para Xbox são:
* Proteção de saída digital
* Data Final do Cache Offline da Licença
* Data do Start da licença
* Data de término da licença
* Duração da janela de reprodução (segundos)

Talvez o conteúdo não precise ser reempacotado para transmitir para o Xbox360, se já tiver sido empacotado para outra plataforma Primetime, como iOS, Android ou Desktop.

Um problema com o Xbox360 é que ele sempre deve acessar um servidor de chaves sempre que uma tag EXT-X-KEY for encontrada no M3U8. Diferentemente do iOS, onde uma configuração de Diretiva DRM (policy.requirementsKeyServer) fará com que o player de vídeo do iOS Primetime recupere a chave de decodificação AES do localhost, o Xbox sempre tentará recuperar a chave de decodificação de um servidor de chaves remoto. Não há nenhum direito de política de DRM para instruir o aplicativo Xbox a recuperar a decodificação de AES
chave de localhost. Devido a esse requisito, as entradas EXT-X-KEY devem estar no M3U8 apontando para o endpoint do DRM da Primetime Cloud. Esse URL é definido por &lt;key_url> no arquivo de configuração OfflinePackager.jar config_hls.xml.

Se desejar disponibilizar o conteúdo uma vez e fazer com que ele seja transmitido a todos os públicos alvos Primetime, bem como configurar dispositivos iOS para não recuperar uma chave de um servidor de chaves remoto, você pode disponibilizar o conteúdo usando uma política DRM que tenha a propriedade policy.requirementsKeyServer=false (como em policy_ios_localkeyserver.pol). Os dispositivos iOS recuperarão a chave AES localmente, enquanto os dispositivos Xbox ignorarão essa propriedade e chegarão ao servidor de chaves DRM da Primetime Cloud
para uma chave de decodificação.

>!Nota
>
>Todas as solicitações do Xbox360 devem utilizar Autenticação personalizada/>Direito.Isso ocorre porque na plataforma Xbox360, o Xbox Live >utiliza um token Xbox Secure Token Server (XSTS) para fins de >autenticação.
>O servidor de licenças DRM da Primetime Cloud usa o token XSTS para >validar a integridade do dispositivo Xbox e do usuário que faz a solicitação de licença. No entanto, a validação do token XSTS requer uma chave privada do fornecedor do Xbox Live >do cliente, que o Primetime Cloud DRM >não armazena. Por isso, quando o Primetime Cloud DRM receber >uma solicitação de licença de um cliente Xbox 360, o Primetime Cloud DRM >encaminhará o token XSTS para o servidor Back-End > Authentication/Entitlement do cliente Primetime. O servidor do cliente Primetime
>irá então analisar e validar o token XSTS para garantir que ele foi >assinado usando a chave do editor do aplicativo do cliente.
>Para enviar um token XSTS do cliente Xbox360, defina o token >sincronicamente em resposta ao evento MediaPlayer.RequestKeyAttribute >descrito em mais detalhes aqui: **Defina o token XSTS no player.** Uma amostra do servidor de autenticação back-end/autorização >está incluída na versão do software no diretório Autenticação personalizada >e Direito.A validação dos tokens XSTS é discutida >com mais detalhes aqui:  **Validação do token Xbox Live XSTS.**


## Defina o token XSTS no player {#set-the-xsts-token-in-your-player}

No Xbox360, você define o token de forma assíncrona em resposta ao evento `MediaPlayer.RequestKeyAttribute`.

Defina o token XSTS.

O aplicativo de amostra fornecido com seu software mostra como definir o token XSTS no player. Este é o trecho de código relevante do player de amostra:

```
   MediaPlayer mMediaPlayer;  
 
mMediaPlayer.RequestKeyAttribute += Player_RequestKeyAttribute;  
 
private void Player_RequestKeyAttribute(object sender, RequestKeyAttributeEventArgs args) {  
    string token = "";  
    // XBOX XSTS Token...  
    KeyAttribute keyAttribute = new KeyAttribute(System.Text.Encoding.UTF8.GetBytes(token), null);  
    mMediaPlayer.SetKeyAttribute(args.RequestIdentifier, keyAttribute);  
} 
```

## Validação de token Xbox Live XSTS {#xbox-live-xsts-token-validation}

Para solicitações XSTS, o campo `customerSpecificAuthToken` conterá o token XSTS codificado em Base64. O código de amostra `XSTSValidator` examina o token decodificado Base64 quanto à existência do elemento `EncryptedAssertion`; no entanto, você pode usar outros métodos para distinguir entre essas solicitações e solicitações que não sejam do Xbox. Por exemplo, você pode usar um URL diferente.

A política retornada na mensagem de resposta substituirá a política original nos metadados DRM fornecidos com a solicitação de chave Xbox. Somente um subconjunto de recursos de política é suportado pelo cliente Xbox e esses campos são os únicos que substituirão a política original.

Existem etapas de configuração adicionais necessárias para suportar a decodificação e validação de token. Você deve carregar as credenciais [!DNL xsts_partner_cert.pfx] e [!DNL x_secure_token_service.part.xboxlive.com.cer] em um armazenamento de chave no formato JKS, que você fornece ao servidor de direito de back-end como a propriedade do sistema `xsts-keystore`. Por padrão, o parceiro [!DNL .pfx] tem o alias `xsts` e o certificado de validação do token tem o alias `xsts-verify-cert`. Também é possível substituí-los usando as propriedades do sistema. Finalmente, há uma propriedade do sistema `xsts-keystore-password` que não tem padrão e que contém a senha do armazenamento de chaves. As propriedades do sistema lidas pelo código `XSTSValidator` são resumidas abaixo:

| Propriedade do sistema | Valor padrão | Comentário |
|---|---|---|
| xsts-keystore | xsts.jks | Armazenamento de chave no formato JKS usado pelo validador. |
| xsts-keystore-password |  | Senha para o armazenamento de chaves |
| xsts-alias | xsts | Alias usado para recuperar a chave de decodificação do armazenamento de chaves |
| xsts-verify-cert-alias | xsts-verify-cert | Alias usado para recuperar o certificado de validação do armazenamento de chaves |

## Criar JKS para um validador XSTS{#create-jks-for-an-xsts-validator}

1. Descubra o nome alias do certificado privado, localizado no arquivo parceiro [!DNL .pfx].

   ```
   keytool -list -storetype pkcs12 -keystore xsts_partner_cert.pfx -v 
   ```

1. Converta [!DNL .pfx] em [!DNL .jks].

   ```
   keytool -importkeystore -srckeystore xsts_partner_cert.pfx -srcstoretype PKCS12 \  
           -keystore xsts.jks -srcalias  
   <alias> -destalias xsts
   ```

   (onde `<alias>` é o nome alias do certificado privado que você descobriu na Etapa 1.)
1. Importe [!DNL x_secure_token_service.part.xboxlive.com.cer].

   ```
   keytool -importcert -alias xsts-verify-cert -keystore xsts.jks \  
           -file x_secure_token_service.part.xboxlive.com.cer 
   ```

1. Coloque [!DNL xsts.jks] em seu diretório inicial Tomcat e defina `-Dxsts-keystore-password=****` para Tomcat.

Se [!DNL xsts_partner_cert.pfx] e [!DNL xsts.jks] estiverem usando senhas diferentes, atualize a senha `xsts` em `jks` para torná-las iguais.

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```
