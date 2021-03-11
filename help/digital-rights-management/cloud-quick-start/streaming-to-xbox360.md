---
title: Definir o token XSTS no seu reprodutor
description: Definir o token XSTS no seu reprodutor
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 0%

---


# Streaming para Xbox360 (opcional) {#streaming-to-xboc360}

O DRM do Primetime está disponível na plataforma Xbox360. No entanto, somente o caso de uso de transmissão protegida é suportado, não o conjunto completo de direitos de política de DRM. Não há suporte para direitos de política de DRM que não sejam de transmissão, como Grupos de domínio do dispositivo. O Xbox360 ignora direitos não suportados ao tentar reproduzir conteúdo.

Os direitos da Política de DRM do Primetime suportados para a Xbox são:
* Proteção de saída digital
* Data Final do Cache Offline da Licença
* Data de início da licença
* Data Final da Licença
* Duração da janela de reprodução (segundos)

O conteúdo pode não ter que ser reempacotado para stream para Xbox360, se já tiver sido empacotado para outra plataforma Primetime, como iOS, Android ou Desktop.

Um problema com o Xbox360 é que ele sempre deve alcançar um servidor de chaves sempre que uma tag EXT-X-KEY for encontrada no M3U8. Ao contrário do iOS, onde uma configuração de Política de DRM (policy.requireKeyServer) fará com que o player de vídeo do Primetime do iOS recupere a chave de descriptografia do AES a partir de localhost, o Xbox sempre tentará recuperar a chave de descriptografia de um servidor de chaves remoto . Não há nenhum direito de política de DRM para instruir o aplicativo Xbox a recuperar a descriptografia do AES
chave de localhost. Devido a esse requisito, as entradas EXT-X-KEY devem estar no M3U8 apontando para o endpoint DRM da Primetime Cloud. Esse URL é definido por &lt;key_url> no arquivo de configuração OfflinePackager.jar config_hls.xml.

Se quiser empacotar o conteúdo uma vez e enviá-lo para todos os destinos do Primetime, bem como configurar os dispositivos iOS para não recuperar uma chave de um servidor de chaves remoto, é possível empacotar o conteúdo usando uma política de DRM que tenha a propriedade policy.requireKeyServer=false (como em policy_ios_localkeyserver.pol). Os dispositivos iOS recuperarão a chave AES localmente, enquanto os dispositivos Xbox ignorarão essa propriedade e acessarão o servidor de chaves DRM da Primetime Cloud
para obter uma chave de descriptografia.

>!Nota
>
>Todas as solicitações do Xbox360 devem utilizar Autenticação Personalizada/>Direito.Isso ocorre porque, na plataforma Xbox360, o Xbox Live utiliza um token Xbox Secure Token Server (XSTS) para fins de autenticação.
>O servidor de licenças DRM da Primetime Cloud usa o token XSTS para >validar a integridade do dispositivo Xbox e do usuário que faz a solicitação de licença. No entanto, a validação do token XSTS requer uma chave privada do fornecedor Xbox Live do cliente, que o DRM do Primetime Cloud não armazena. Por causa disso, quando o DRM da Primetime Cloud recebe uma solicitação de licença de um cliente Xbox 360, o DRM da Primetime Cloud enviará o token XSTS para o servidor Back-end do cliente Primetime >Authentication/Entitlement. O servidor do cliente Primetime
>O analisará e validará o token XSTS para garantir que ele foi assinado usando a chave do editor do aplicativo do cliente.
>Para passar um token XSTS do cliente Xbox360, defina o token >de forma síncrona em resposta ao evento MediaPlayer.RequestKeyAttribute > - descrito em mais detalhes aqui: **Defina o token XSTS no seu reprodutor.** Um exemplo de servidor de Autenticação/Direitos Back-End está incluído na versão do software no diretório Autenticação Personalizada > e Direito.A validação dos tokens XSTS é discutida mais detalhadamente aqui:  **Validação do token Xbox Live XSTS.**


## Defina o token XSTS no seu reprodutor {#set-the-xsts-token-in-your-player}

No Xbox360, você define o token de forma assíncrona em resposta ao evento `MediaPlayer.RequestKeyAttribute`.

Defina o token XSTS.

O aplicativo de amostra fornecido com seu software mostra como definir o token XSTS no player. Este é o trecho de código relevante do reprodutor de amostra:

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

Para solicitações XSTS, o campo `customerSpecificAuthToken` conterá o token XSTS codificado em Base64. O código `XSTSValidator` de amostra examina o token decodificado Base64 para a existência do elemento `EncryptedAssertion`; no entanto, você pode usar outros métodos para distinguir entre essas solicitações e solicitações que não são da Xbox. Por exemplo, você pode usar um URL diferente.

A política retornada na mensagem de resposta substituirá a política original nos metadados DRM fornecidos com a solicitação da chave Xbox. Somente um subconjunto de recursos de política é suportado pelo cliente Xbox, e esses campos são os únicos que substituirão a política original.

Há etapas de configuração adicionais necessárias para oferecer suporte à descriptografia e validação de token. Você deve carregar as credenciais [!DNL xsts_partner_cert.pfx] e [!DNL x_secure_token_service.part.xboxlive.com.cer] em um armazenamento de chaves do formato JKS, que você fornece ao servidor de direito de back-end como a propriedade de sistema `xsts-keystore`. Por padrão, o parceiro [!DNL .pfx] tem o alias `xsts` e o certificado de validação do token tem o alias `xsts-verify-cert`. Também é possível substituí-los usando as propriedades do sistema. Finalmente, há uma propriedade do sistema `xsts-keystore-password` que não tem o padrão e que contém a senha do armazenamento de chaves. As propriedades do sistema lidas pelo código `XSTSValidator` são resumidas abaixo:

| Propriedade do sistema | Valor padrão | Comentário |
|---|---|---|
| xsts-keystore | xsts.jks | Armazenamento de chaves do formato JKS usado pelo validador. |
| xsts-keystore-password |  | Senha do repositório de chaves |
| xsts-alias | xsts | Alias usado para recuperar a chave de descriptografia do repositório de chaves |
| xsts-verify-cert-alias | xsts-verify-cert | Alias usado para recuperar o certificado de validação do repositório de chaves |

## Criar JKS para um validador XSTS{#create-jks-for-an-xsts-validator}

1. Descubra o nome alias do certificado privado, localizado no arquivo [!DNL .pfx] do parceiro.

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

1. Coloque [!DNL xsts.jks] no diretório base do Tomcat e defina `-Dxsts-keystore-password=****` para Tomcat.

Se [!DNL xsts_partner_cert.pfx] e [!DNL xsts.jks] estiverem usando senhas diferentes, atualize a senha `xsts` em `jks` para torná-las iguais.

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```
