---
title: Registro do aplicativo Amazon FireOS
description: Registro do aplicativo Amazon FireOS
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---


# Registro do aplicativo Amazon FireOS {#amazon-fireos-application-registration}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

</br>

## Introdução {#intro}

A partir da versão 3.0 do SDK do FireOS AccessEnabler, estamos alterando o mecanismo de autenticação com servidores Adobe. Em vez de usar uma chave pública e um sistema secreto para assinar a ID do solicitante, estamos introduzindo o conceito de uma sequência de caracteres da Declaração de Software que pode ser usada para obter um token de acesso que é usado posteriormente para todas as chamadas que o SDK faz para nossos servidores. Além de uma Declaração de software, você também precisará criar um deep link para seu aplicativo.

Mais informações, consulte [Registro dinâmico de clientes](/help/authentication/dynamic-client-registration.md)

## O que é uma declaração de software? {#what}

Uma Declaração de software é um token JWT que contém informações sobre seu aplicativo. Cada aplicativo deve ter uma Declaração de Software exclusiva que é usada por nossos servidores para identificar o aplicativo no sistema Adobe. A instrução de software precisa ser transmitida ao inicializar o SDK do AccessEnabler e será usada para registrar o aplicativo no Adobe. Após o registro, o SDK receberá uma ID do cliente e um segredo do cliente que será usado para obter um token de acesso. Qualquer chamada feita pelo SDK para nossos servidores exigirá um token de acesso válido. O SDK é responsável por registrar o aplicativo, obter e atualizar o token de acesso.

**Observação:** Declarações de software são específicas do aplicativo e uma Declaração de software individual não pode ser usada para mais de um aplicativo. Observe que isso também se aplica a aplicativos que oferecem acesso a vários canais.

## Como obter uma declaração de software? {#how-to}

### Se você tiver acesso ao Painel Adobe TVE:

- Abra o navegador e acesse <https://console.auth.adobe.com>
- Navegar para `Channels` e selecione seu canal.
- Navegar para `Registered Applications` Guia.
- Clique em `Add new application`.
- Forneça um nome e uma versão para o seu aplicativo e selecione as plataformas nas quais ele estará disponível (por exemplo, Android no nosso caso).
- Forneça um Nome de Domínio escolhendo em uma lista de domínios já configurados para seu Programador.
- Encaminhe suas alterações para o servidor e navegue de volta para a guia Aplicativos registrados do canal.
- Você deve ver uma lista com todos os aplicativos registrados. Clique no botão `Download` no aplicativo que você acabou de criar. Observação: talvez seja necessário esperar alguns minutos até que a sua Declaração de software esteja pronta para download.
- Um arquivo de texto será baixado. Use seu conteúdo como sua Declaração de software.

Mais informações, consulte [Dynamic Client Registration Management](/help/authentication/dynamic-client-registration-management.md)

### Se você não tiver acesso ao Adobe do Painel VE:

Enviar um tíquete para <tve-support@adobe.com>. Inclua todas as informações necessárias, incluindo canal, nome do aplicativo, versão e plataformas. Alguém da nossa equipe de suporte criará uma declaração de software para você.

## Como usar a Declaração de software? {#use}

Depois de obter sua Declaração de software, você precisa passá-la como um parlamentar no construtor do Ativador de acesso. Recomendamos hospedar a Declaração de software em um local remoto. Dessa forma, você pode facilmente revogar e alterar o Software Statement sem lançar uma nova versão do seu aplicativo.

## Como usar a Declaração de Software {#use-both}

No arquivo de recursos do aplicativo `strings.xml` adicione o seguinte código:

```XML
<string name="software_statement">softwarestatement value</string>
```
