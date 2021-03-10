---
description: Para implementar o DRM, você precisa de determinados certificados e chaves, incluindo uma chave de criptografia de conteúdo ou CEK para criptografar seu conteúdo, um autenticador do cliente para proteger comunicações com servidores ExpressPlay e CEKSIDs para identificar suas chaves de criptografia de conteúdo como armazenadas em um sistema de gerenciamento de chaves.
title: Chaves, IDs e autenticadores
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 0%

---


# Chaves, IDs e Autenticadores{#keys-ids-and-authenticators}

Para implementar o DRM, você precisa de determinados certificados e chaves, incluindo uma chave de criptografia de conteúdo ou CEK para criptografar seu conteúdo, um autenticador do cliente para proteger comunicações com servidores ExpressPlay e CEKSIDs para identificar suas chaves de criptografia de conteúdo como armazenadas em um sistema de gerenciamento de chaves.

Você precisa destes itens para empacotar, licenciar e reproduzir seu conteúdo protegido:

## Chave de criptografia de conteúdo {#section_8D16D36BAE3B4D1F92A0C43567D782D0}

A Chave de criptografia de conteúdo (CEK) é uma string de 16 bytes usada para criptografar conteúdo.

**O que é o CEK?** - A CEK é a chave que seu empacotador usa para criptografar seu conteúdo. É uma string codificada por hexadecimal de 16 bytes.

**De onde vem o CEK?** - Você (o provedor de conteúdo) cria essa chave por conta própria, usando uma ferramenta como OpenSSL ou Notepad++. Por exemplo:

```
openssl rand 16 -hex > cek_hex_file
```

ou (para o Adobe Offline Packager):

1. Gere a string codificada por hexadecimal de 16 bytes, como acima ou usando alguma outra ferramenta. Será algo como isto:

   ```
   7debe705d938c76bfd886f077b8fa5f7
   ```

1. Abra o Bloco de notas++ e cole na sequência hexadecimal de 16 bytes.
1. Converta esse valor de ASCII hexadecimal pela codificação Base64 do valor para criar seu [!DNL keyfile.bin]. (Isso é abordado em [](../../multi-drm-workflows/quick-start/package-your-content.md).)

**Mesma chave, nome diferente?** - Sim, você pode ver o CEK referido por outros nomes em outros lugares, como:

* ** [!DNL [somefile].bin]** - O Adobe Offline Packager se refere ao CEK como [!DNL [somefile].bin]; Por exemplo, * [!DNL Keyfile.bin]* - Esse é o CEK usado pelo Adobe Offline Packager, no formato de um arquivo no computador usado para empacotar conteúdo.

   Você &quot;Base64&quot; sua sequência hexadecimal CEK aleatória e a salve como um arquivo (por exemplo, [!DNL keyfile.bin]), normalmente localizado no diretório [!DNL creds] abaixo de [!DNL offlinepkgr/]. No arquivo de configuração do Packager (por exemplo, você pode chamá-lo [!DNL widevine.xml] se estiver empacotando para o DRM da Widevine), faça referência ao CEK no arquivo de configuração desta forma:

   ```
   <config>  
     <in_path>sample.mp4</in_path>  
     <out_type>dash</out_type>
     <b><key_file_path>keyfile.bin</key_file_path></b> // This is your CEK  
     […] 
   </config> 
   ```

* **Chave de conteúdo**  - Você também pode ver o CEK referido como uma Chave de conteúdo nas chamadas (  `&contentKey=`), em mensagens de erro, em tíquetes de suporte e em outra documentação.

**Quando / onde devo usá-lo?**

1. Primeiro, você precisa ter o CEK disponível na máquina em que você está fazendo sua embalagem. Sua ferramenta de empacotamento usa seu CEK para criptografar seu conteúdo.
1. Segundo, você precisa armazenar o CEK em alguma forma de KMS (Key Management System), com cada CEK associado a sua própria [Chave de criptografia de conteúdo](../../multi-drm-workflows/glossary/glossary-cek.md). Você pode criar seu próprio KMS ou usar o [Armazenamento de chaves do ExpressPlay](https://www.expressplay.com/developer/key-storage/). Isso permite que sua loja (seu servidor de direito, que lida com a qualificação do cliente e a provisão do Token de licença) extraia um token de licença do cliente do KMS usando uma ID de chave em vez do CEK real (isso é muito mais seguro).

## ID de armazenamento da chave de criptografia de conteúdo {#section_0C94F54970E04BDB82DE3C8A33A62CD4}

A ID de armazenamento da chave de criptografia de conteúdo (CEKSID) identifica exclusivamente a chave armazenada que descriptografa um conteúdo de vídeo criptografado.

**O que é o CEKSID?** - O CEKSID é o identificador exclusivo de uma Chave de criptografia de conteúdo (CEK). O CEK é necessário para desbloquear o conteúdo protegido; O CEKSID é necessário para aceder ao CEK a partir do local onde está armazenado. Ao testar sua configuração, você pode fornecer um CEKSID e um CEK aleatórios no momento do empacotamento, desde que use as mesmas informações para as verificações de licenciamento e reprodução.

**De onde vem?** - Você (o provedor de conteúdo) pode criar essa ID por conta própria ou pode usar um serviço como o  [ExpressPlay Key ](https://www.expressplay.com/developer/key-storage/) Storags para gerar CEKSIDs para cada CEKs (e armazenar ambos). Além disso, você pode usar CEKSIDs gerados aleatoriamente ou empregar um esquema adequado ao seu modelo de negócios. Por exemplo, você pode usar CEKSIDs que são strings significativas em vez de strings hexadecimais (o nome da ID pode consistir em assuntos, datas, horas etc.)

**Como se chama o CEKSID?** - Às vezes, ela é chamada de ID  *de conteúdo*.

## Autenticador de cliente {#section_F9DDBAA54C544D82A42320CBEEB6CD74}

O autenticador de cliente é uma chave obtida do ExpressPlay ao configurar uma conta de administrador lá. O autenticador é usado em comunicações com servidores ExpressPlay.

**Quais são os autenticadores do cliente?** - Os dois autenticadores do cliente compõem o par de IDs — um para teste, um para produção — que o ExpressPlay registra quando você se inscreve no serviço. Eles sempre estão disponíveis para você na página de administração do ExpressPlay:
<!--<a id="fig_c5h_xdl_wv"></a>-->

![](assets/expressplay_admin_dashboard-web.png)

**Quando devo usar isso?** - Você inclui isso em todas as chamadas para servidores ExpressPlay, por exemplo, servidores de licença,  [ExpressPlay Key Storage](https://www.expressplay.com/developer/key-storage/) e outras chamadas.
