---
title: Conteúdo criptografado do pacote
description: Conteúdo criptografado do pacote
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# Conteúdo criptografado do pacote{#package-encrypted-content}

1. Copie o `<Primetime DRM DVD>\Reference Implementation\Command Line Tools\` para o sistema de arquivos local.
1. Em seu local `Command Line Tools\` pasta, atualize o `flashaccesstools.properties` para trabalhar com o servidor.

   Você deve modificar pelo menos as seguintes propriedades:

   * `encrypt.keys.asymmetric.certfile=[license-server-certificate.cer]`: o caminho para o Certificado do License Server (geralmente termina com [!DNL .cer], [!DNL .der] ou [!DNL .pem]).

   * `encrypt.license.serverurl=[license-server-url]`: O URL do servidor de licenças, por exemplo:    `https://<License Server Hostname>:8080/flashaccessserver/sampletenant`.

   * `encrypt.license.servercert=[transport-certificate.cer]`: O caminho para o certificado de transporte (geralmente termina com [!DNL .cer], [!DNL .der]ou [!DNL .pem]).

   * `encrypt.sign.certfile=[packager-credentials.pfx]`: O caminho para o certificado do Packager (termina com [!DNL .pfx]).

   * `encrypt.sign.certpass=[password]`: A senha do certificado do Packager.

   >[!NOTE]
   >
   >Certifique-se de não embaralhar a senha.

1. Criar uma política.

   Em seu local `Command Line Tools\` execute o seguinte comando:

   ```
   java -jar libs/AdobePolicyManager.jar new examplepolicy.pol -n examplepolicy -x
   ```

   Esse comando cria um arquivo de diretiva com o nome [!DNL examplepolicy.pol] que usa autenticação anônima de servidor de licenças (a `-x` opção).
1. Copie o arquivo de vídeo MP4, FLV ou F4V que deseja criptografar em seu local `Command Line Tools\` pasta.
1. Empacotar o conteúdo.

   Digamos que seu arquivo de vídeo de origem seja [!DNL sample.mp4]. Em seu local `Command Line Tools\` execute o seguinte comando:

   ```
   java -jar libs/AdobePackager.jar sample.mp4 sample_encrypted.mp4 -p examplepolicy.pol
   ```

   >[!NOTE]
   >
   >Se quiser incluir conteúdo HLS, HDS ou DASH no pacote, use uma ferramenta de empacotamento diferente, como [Adobe Primetime Offline Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf).

1. Copie os artefatos de arquivo criptografados (neste caso, [!DNL sample_encrypted.mp4] e [!DNL sample_encrypted.mp4.metadata]) para `<Your Content Server - Tomcat Install Dir>\webapps\ROOT`.

Neste ponto, você concluiu a fase de empacotamento do processo.

>[!NOTE]
>
>Para obter informações mais detalhadas sobre as ferramentas de linha de comando para empacotar conteúdo, criar políticas e muito mais, consulte [Ferramentas de linha de comando do Adobe Primetime DRM](../drm-reference-implementations/command-line-tools/command-line-tools-overview.md).
