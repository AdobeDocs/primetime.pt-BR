---
title: Definir o token XSTS no reprodutor
description: Definir o token XSTS no reprodutor
copied-description: true
exl-id: 1b83baac-e6a6-4e84-8ea5-07bd7e4afd9d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 0%

---

# Streaming para o Xbox360 (opcional) {#streaming-to-xboc360}

O Primetime DRM está disponível na plataforma Xbox360. No entanto, somente o caso de uso de transmissão protegida é compatível, não o conjunto completo de direitos de política de DRM. Os direitos de política DRM de não transmissão, como Grupos de domínio do dispositivo, não são compatíveis. O Xbox 360 ignora direitos não suportados ao tentar reproduzir conteúdo.

Os direitos de DRM com suporte do Primetime para o Xbox são:
* Proteção de saída digital
* Data de término do armazenamento em cache offline da licença
* Data de início da licença
* Data de término da licença
* Duração da janela de reprodução (segundos)

O conteúdo talvez não precise ser reempacotado para transmitir para o Xbox 360, se já tiver sido empacotado para outra plataforma do Primetime, como iOS, Android ou Desktop.

Um problema com o Xbox360 é que ele deve sempre alcançar um servidor chave sempre que uma tag EXT-X-KEY for encontrada no M3U8. Ao contrário do iOS, onde uma configuração de Política DRM (policy.requireKeyServer) fará com que o player de vídeo do iOS Primetime recupere a chave de descriptografia AES do host local, o Xbox sempre tentará recuperar a chave de descriptografia de um servidor de chaves remoto . Não há direito de política DRM para instruir o aplicativo Xbox a recuperar a chave de descriptografia AES do host local. Devido a esse requisito, as entradas EXT-X-KEY devem estar no M3U8 que aponta para o ponto de extremidade DRM do Primetime Cloud. Este URL é definido via &lt;key_url> no arquivo de configuração OfflinePackager.jar config_hls.xml.

Se você quiser criar um pacote de conteúdo uma vez e fazer com que ele seja transmitido para todos os destinos do Primetime, bem como configurar dispositivos iOS para não recuperar uma chave de um servidor de chaves remoto, será possível criar o pacote do conteúdo usando uma política DRM que tenha a propriedade policy.requireKeyServer=false (como em policy_ios_localkeyserver.pol). Os dispositivos iOS recuperarão a chave AES localmente, enquanto os dispositivos Xbox ignorarão essa propriedade e acessarão o servidor de chaves DRM do Primetime Cloud para obter uma chave de descriptografia.

>!Nota
>
>Todas as solicitações do Xbox360 devem utilizar Autenticação Personalizada/>Direitos.Isso ocorre porque, na plataforma Xbox360, o Xbox Live >utiliza um token do Servidor de Token Seguro do Xbox (XSTS) para >fins de autenticação.
>O servidor de licença DRM da Primetime Cloud usa o token XSTS para validar a integridade do dispositivo Xbox e do usuário que está fazendo a solicitação de licença. No entanto, a validação do token XSTS requer uma chave privada do fornecedor do Xbox Live do cliente, que o DRM do Primetime Cloud não armazena. Por causa disso, quando o DRM do Primetime Cloud recebe uma solicitação de licença de um cliente Xbox 360, o DRM do Primetime Cloud encaminhará o token XSTS para o servidor Back-End do cliente do Primetime >Autenticação/Direito. O servidor do cliente do Primetime
>O analisará e validará o token XSTS para garantir que ele foi assinado usando a chave do editor do aplicativo do cliente.
>Para enviar um token XSTS do cliente Xbox360, defina o token de forma síncrona em resposta ao evento MediaPlayer.RequestKeyAttribute - descrito com mais detalhes aqui: **Defina o token XSTS no reprodutor.** Um exemplo de servidor de Autenticação/Autenticação de back-end é incluído com a versão do software no diretório Autenticação personalizada e Qualificação.A validação de tokens XSTS é discutida mais detalhadamente aqui: **Validação de token XSTS do Xbox Live.**


## Definir o token XSTS no reprodutor {#set-the-xsts-token-in-your-player}

No Xbox360, você define o token de forma assíncrona em resposta ao `MediaPlayer.RequestKeyAttribute` evento.

Defina o token XSTS.

O aplicativo de amostra fornecido com seu software mostra como definir o token XSTS no reprodutor. Este é o trecho de código relevante do reprodutor de amostra:

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

## Validação de token XSTS do Xbox Live {#xbox-live-xsts-token-validation}

Para solicitações XSTS, a variável `customerSpecificAuthToken` conterá o token XSTS codificado na Base64. A amostra `XSTSValidator` O código examina o token decodificado Base64 para a existência do `EncryptedAssertion` elemento; no entanto, você pode usar outros métodos para distinguir entre essas solicitações e solicitações que não são do Xbox. Por exemplo, você pode usar um URL diferente.

A política retornada na mensagem de resposta substituirá a política original nos metadados DRM fornecidos com a solicitação de chave do Xbox. Somente um subconjunto de recursos de política é suportado pelo cliente Xbox, e esses campos são os únicos que substituirão a política original.

Há etapas de configuração adicionais necessárias para oferecer suporte à descriptografia e validação de tokens. Você deve carregar o [!DNL xsts_partner_cert.pfx] e [!DNL x_secure_token_service.part.xboxlive.com.cer] em um armazenamento de chaves no formato JKS, que você fornece ao servidor de direitos de back-end como a propriedade do sistema `xsts-keystore`. Por padrão, o parceiro [!DNL .pfx] tem o alias `xsts`e o certificado de validação de token tem o alias `xsts-verify-cert`. Também é possível substituí-los usando propriedades do sistema. Finalmente, há uma propriedade do sistema `xsts-keystore-password` que não tem padrão e que contém a senha do keystore. As propriedades do sistema lidas pelo `XSTSValidator` estão resumidos abaixo:

| Propriedade do sistema | Valor padrão | Comentário |
|---|---|---|
| xsts-keystore | xsts.jks | Armazenamento de chaves no formato JKS usado pelo validador. |
| xsts-keystore-password |  | Senha para o keystore |
| xsts-alias | existe | Alias usado para recuperar a chave de descriptografia do keystore |
| xsts-verify-cert-alias | xsts-verify-cert | Alias usado para recuperar o certificado de validação do armazenamento de chaves |

## Criar JKS para um validador XSTS{#create-jks-for-an-xsts-validator}

1. Descubra o nome do alias do certificado privado, localizado no parceiro [!DNL .pfx] arquivo.

   ```
   keytool -list -storetype pkcs12 -keystore xsts_partner_cert.pfx -v 
   ```

1. Converter [!DNL .pfx] para [!DNL .jks].

   ```
   keytool -importkeystore -srckeystore xsts_partner_cert.pfx -srcstoretype PKCS12 \  
           -keystore xsts.jks -srcalias  
   <alias> -destalias xsts
   ```

   (onde `<alias>` é o nome de alias do certificado privado descoberto na Etapa 1.)
1. Importar [!DNL x_secure_token_service.part.xboxlive.com.cer].

   ```
   keytool -importcert -alias xsts-verify-cert -keystore xsts.jks \  
           -file x_secure_token_service.part.xboxlive.com.cer 
   ```

1. Put [!DNL xsts.jks] no diretório inicial do Tomcat e defina `-Dxsts-keystore-password=****` para Tomcat.

Se [!DNL xsts_partner_cert.pfx] e [!DNL xsts.jks] estiverem usando senhas diferentes, atualize o `xsts` senha em `jks` para torná-las iguais.

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```
