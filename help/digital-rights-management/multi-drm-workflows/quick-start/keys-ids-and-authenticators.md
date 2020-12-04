---
description: Para implementar o DRM, você precisa de certificados e chaves específicos, incluindo uma chave de criptografia de conteúdo ou CEK para criptografar seu conteúdo, um autenticador do cliente para proteger comunicações com servidores ExpressPlay e CEKSIDs para identificar suas chaves de criptografia de conteúdo como armazenadas em um sistema de gerenciamento de chaves.
seo-description: Para implementar o DRM, você precisa de certificados e chaves específicos, incluindo uma chave de criptografia de conteúdo ou CEK para criptografar seu conteúdo, um autenticador do cliente para proteger comunicações com servidores ExpressPlay e CEKSIDs para identificar suas chaves de criptografia de conteúdo como armazenadas em um sistema de gerenciamento de chaves.
seo-title: Teclas, IDs e autenticadores
title: Teclas, IDs e autenticadores
uuid: 9e5b1a64-b4e9-442f-ac15-26831aaf585d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 0%

---


# Teclas, IDs e Autenticadores{#keys-ids-and-authenticators}

Para implementar o DRM, você precisa de certificados e chaves específicos, incluindo uma chave de criptografia de conteúdo ou CEK para criptografar seu conteúdo, um autenticador do cliente para proteger comunicações com servidores ExpressPlay e CEKSIDs para identificar suas chaves de criptografia de conteúdo como armazenadas em um sistema de gerenciamento de chaves.

Você precisa destes itens para disponibilizar, licenciar e reproduzir seu conteúdo protegido:

## Chave de criptografia de conteúdo {#section_8D16D36BAE3B4D1F92A0C43567D782D0}

A CEK (Content Encryption Key) é uma string de 16 bytes usada para criptografar conteúdo.

**O que é o CEK?** - O CEK é a chave que seu empacotador usa para criptografar seu conteúdo. É uma string codificada por hexadecimal de 16 bytes.

**De onde vem o CEK?** - Você mesmo (o provedor de conteúdo) cria essa chave usando uma ferramenta como OpenSSL ou Notepad++. Por exemplo:

```
openssl rand 16 -hex > cek_hex_file
```

ou (para o Adobe Offline Packager):

1. Gere a string codificada por hexadecimal de 16 bytes, como acima ou usando outra ferramenta. Será algo como isto:

   ```
   7debe705d938c76bfd886f077b8fa5f7
   ```

1. Abra o Bloco de notas++ e cole na string hexadecimal de 16 bytes.
1. Converta esse valor de ASCII hexadecimal pela codificação Base64 do valor para criar [!DNL keyfile.bin]. (Isso é abordado em [](../../multi-drm-workflows/quick-start/package-your-content.md).)

**Mesma chave, nome diferente?** - Sim, você pode ver o CEK referido por outros nomes em outros lugares, como:

* ** [!DNL [somefile].bin]** - O Adobe Offline Packager refere-se ao CEK como [!DNL [somefile].bin]; por exemplo, * [!DNL Keyfile.bin]* - Este é o CEK utilizado pelo Adobe Offline Packager, na forma de um arquivo no computador usado para empacotar conteúdo.

   Você &quot;Base64&quot; sua sequência hexadecimal CEK aleatória e salva-a como um arquivo (por exemplo, [!DNL keyfile.bin]), normalmente localizado no diretório [!DNL creds] abaixo de [!DNL offlinepkgr/]. No arquivo de configuração do Packager (por exemplo, você pode chamá-lo [!DNL widevine.xml] se estiver empacotando o DRM do Widevine), consulte seu CEK no arquivo de configuração desta forma:

   ```
   <config>  
     <in_path>sample.mp4</in_path>  
     <out_type>dash</out_type>
     <b><key_file_path>keyfile.bin</key_file_path></b> // This is your CEK  
     […] 
   </config> 
   ```

* **Chave**  de conteúdo - Você também pode ver o CEK chamado de Chave de conteúdo em chamadas (  `&contentKey=`), mensagens de erro, tíquetes de suporte e em outra documentação.

**Quando / onde eu o uso?**

1. Primeiro, você precisa ter o CEK disponível na máquina na qual você está fazendo sua embalagem. Sua ferramenta de empacotamento usa seu CEK para criptografar seu conteúdo.
1. Em segundo lugar, é necessário armazenar o CEK em alguma forma do Key Management System (KMS), com cada CEK associado à sua própria [Chave de criptografia de conteúdo](../../multi-drm-workflows/glossary/glossary-cek.md). Você pode criar seu próprio KMS ou usar [Armazenamento-chave do ExpressPlay](https://www.expressplay.com/developer/key-storage/). Isso permite que o storefront (seu servidor de direito, que lida com o direito do cliente e o fornecimento do token de licença) extraia um token de licença para o cliente do KMS usando uma ID de chave em vez do CEK real (isso é muito mais seguro).

## ID do Armazenamento da chave de criptografia de conteúdo {#section_0C94F54970E04BDB82DE3C8A33A62CD4}

A ID de Armazenamento da chave de criptografia de conteúdo (CEKSID) identifica de forma exclusiva a chave armazenada que descriptografa uma parte criptografada do conteúdo de vídeo.

**O que é o CEKSID?** - O CEKSID é o identificador exclusivo de uma Chave de criptografia de conteúdo (CEK). O CEK é necessário para desbloquear o conteúdo protegido; o CEKSID é necessário para aceder ao CEK a partir do local onde é armazenado. Ao testar sua configuração, você pode fornecer um CEKSID e um CEK aleatórios no momento da embalagem, desde que use as mesmas informações para as verificações de licenciamento e reprodução.

**De onde vem?** - Você (o provedor de conteúdo) pode criar essa ID por conta própria ou pode usar um serviço como o  [ExpressPlay&#39;s Key ](https://www.expressplay.com/developer/key-storage/) Storagage para gerar CEKSIDs para cada CEKs (e armazenar ambos). Além disso, você pode usar CEKSIDs gerados aleatoriamente, ou empregar um esquema adequado ao seu modelo de negócios. Por exemplo, você pode usar CEKSIDs que são strings significativas em vez de strings hexadecimais aleatórias (o nome da ID pode consistir de assuntos, datas, horas etc.)

**Como se chama o CEKSID?** - Às vezes, é chamada de ID ** de conteúdo.

## Autenticador do cliente {#section_F9DDBAA54C544D82A42320CBEEB6CD74}

O autenticador do cliente é uma chave obtida do ExpressPlay quando você configura uma conta de administrador lá. O autenticador é usado em comunicações com servidores ExpressPlay.

**Quais são os autenticadores do cliente?** - Os dois autenticadores de clientes constituem o par de IDs — um para testes, um para produção. esse ExpressPlay se registra quando você se inscreve no serviço. Eles estão sempre disponíveis para você na página de administração do ExpressPlay:
<!--<a id="fig_c5h_xdl_wv"></a>-->

![](assets/expressplay_admin_dashboard-web.png)

**Quando eu uso isso?** - Isso é incluído em todas as chamadas para os servidores ExpressPlay. por exemplo, servidores de licença, Armazenamento [ ](https://www.expressplay.com/developer/key-storage/) ExpressPlay Key e outras chamadas.
