---
title: Registro do aplicativo iOS/tvOS
description: Registro do aplicativo iOS/tvOS
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---


# Registro do aplicativo iOS/tvOS {#iostvos-application-registration}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Introdução {#Intro}

A partir da versão 3.0 do SDK do iOS/tvOS AccessEnabler, estamos alterando o mecanismo de autenticação com servidores Adobe. Em vez de usar uma chave pública e um sistema secreto para assinar a ID do solicitante, estamos introduzindo o conceito de uma string de declaração do software que pode ser usada para obter um token de acesso que é usado posteriormente para todas as chamadas que o SDK faz para nossos servidores. Além de uma declaração de software, você também precisará de um esquema de URL personalizado para seu aplicativo.

Para obter mais informações, consulte [Registro dinâmico de clientes](/help/authentication/dynamic-client-registration.md)

## O que é uma declaração de software? {#Soft_state}

Uma Declaração de software é um token JWT que contém informações sobre seu aplicativo. Cada aplicativo deve ter uma declaração de software exclusiva que é usada por nossos servidores para identificar o aplicativo no sistema Adobe. A instrução de software precisa ser transmitida ao inicializar o SDK do AccessEnabler e será usada para registrar o aplicativo no Adobe. Após o registro, o SDK receberá uma ID do cliente e um segredo do cliente que será usado para obter um token de acesso. Qualquer chamada feita pelo SDK para nossos servidores exigirá um token de acesso válido. O SDK é responsável por registrar o aplicativo, obter e atualizar o token de acesso.

**Observação:** Uma Declaração de Software é específica do aplicativo e a mesma instrução de software não pode ser usada em mais de um aplicativo. Observe que as instruções de software do nível do Programador também seguem o mesmo, ou seja, elas só podem ser usadas para um único aplicativo - seja canal único ou multicanal. Esta limitação também se aplica ao regime personalizado.

## Como obter uma declaração de software? {#obtain}

### Se você tiver acesso ao Painel Adobe TVE:

- Abra o navegador e acesse <https://console.auth.adobe.com>
- Navegar para `Channels` e selecione seu canal.
- Navegar para `Registered Applications` Guia.
- Clique em `Add new application`.
- Forneça um nome e uma versão para o seu aplicativo e selecione as plataformas nas quais ele estará disponível. iOS/tvOS no nosso caso.
- Encaminhe suas alterações para o servidor e navegue de volta para a guia Aplicativos registrados do canal.
- Você deve ver uma lista com todos os aplicativos registrados. Clique no botão   `Download` no aplicativo que você acabou de criar. Pode ser necessário aguardar alguns minutos antes do seu Extrato de software estar pronto para download.
- Um arquivo de texto será baixado. Use seu conteúdo como sua Declaração de software.

Para obter mais informações, consulte [Gerenciamento dinâmico de registros de clientes](/help/authentication/dynamic-client-registration-management.md).

### Se você não tiver acesso ao Adobe do Painel VE:

Enviar um tíquete para <tve-support@adobe.com>. Inclua todas as informações necessárias, como canal, nome do aplicativo, versão e plataformas. Alguém da nossa equipe de suporte criará uma declaração de software para você.

## Como usar a Declaração de software? {#use}

Depois de obter sua Declaração de software, você precisa passá-la como um parlamentar no construtor do Ativador de acesso. Recomendamos hospedar a Declaração de software em um local remoto. Dessa forma, você pode facilmente revogar e alterar o Software Statement sem lançar uma nova versão do seu aplicativo.

## Gerar um esquema de URL personalizado para seu aplicativo {#generating}

### Se você tiver acesso ao Painel Adobe TVE:

- Abra o navegador e acesse <https://console.auth.adobe.com>
- Navegar para `Channels` e selecione seu canal.
- Navegar para `Custom Schemes` Guia.
- Clique em `Generate a new custom scheme`.
- Um novo esquema personalizado será gerado para seu aplicativo. Ex: `adbe.1JqxQsYhQOCIrwPjaooY8w://`
- Encaminhe as alterações para o servidor.

### Se você não tiver acesso ao Adobe do Painel VE:

Enviar um tíquete para <tve-support@adobe.com>. Inclua a ID do canal e alguém da nossa equipe de suporte criará um esquema personalizado para você.

## Como usar o esquema personalizado {#use_custom}

No `info.plist` adicione o seguinte código ao arquivo :

```plist
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>adbe.u-XFXJeTSDuJiIQs0HVRAg</string> // replace this with your custom scheme
            </array>
        </dict>
    </array>
```
