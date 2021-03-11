---
title: Conteúdo criptografado do pacote
description: Conteúdo criptografado do pacote
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---


# Conteúdo criptografado do pacote{#package-encrypted-content}

1. Copie o diretório `<Primetime DRM DVD>\Reference Implementation\Command Line Tools\` para o sistema de arquivos local.
1. Na pasta `Command Line Tools\` local, atualize o arquivo `flashaccesstools.properties` para funcionar com o servidor.

   Você deve modificar pelo menos as seguintes propriedades:

   * `encrypt.keys.asymmetric.certfile=[license-server-certificate.cer]`: O caminho para o Certificado do License Server (normalmente termina com  [!DNL .cer],  [!DNL .der] ou  [!DNL .pem]).

   * `encrypt.license.serverurl=[license-server-url]`: O URL do servidor de licenças, por exemplo:     `https://<License Server Hostname>:8080/flashaccessserver/sampletenant`.

   * `encrypt.license.servercert=[transport-certificate.cer]`: O caminho para seu certificado de transporte (normalmente termina com  [!DNL .cer],  [!DNL .der], ou  [!DNL .pem]).

   * `encrypt.sign.certfile=[packager-credentials.pfx]`: O caminho para seu certificado do Packager (termina com  [!DNL .pfx]).

   * `encrypt.sign.certpass=[password]`: A senha do seu certificado do Packager.
   >[!NOTE]
   >
   >Certifique-se de não colocar a senha no comando.

1. Crie uma política.

   Na pasta local `Command Line Tools\`, execute o seguinte comando:

   ```
   java -jar libs/AdobePolicyManager.jar new examplepolicy.pol -n examplepolicy -x
   ```

   Este comando cria um arquivo de política chamado [!DNL examplepolicy.pol] que usa autenticação de servidor de licença anônimo (a opção `-x`).
1. Copie o arquivo de vídeo MP4, FLV ou F4V que você deseja criptografar na pasta `Command Line Tools\` local.
1. Compacte seu conteúdo.

   Digamos que o arquivo de vídeo de origem é [!DNL sample.mp4]. Na pasta local `Command Line Tools\`, execute o seguinte comando:

   ```
   java -jar libs/AdobePackager.jar sample.mp4 sample_encrypted.mp4 -p examplepolicy.pol
   ```

   >[!NOTE]
   >
   >Se quiser empacotar conteúdo HLS, HDS ou DASH, use uma ferramenta de empacotador diferente, como [Adobe Primetime Offline Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf).

1. Copie os artefatos do arquivo criptografado (neste caso [!DNL sample_encrypted.mp4] e [!DNL sample_encrypted.mp4.metadata]) para `<Your Content Server - Tomcat Install Dir>\webapps\ROOT`.

Neste ponto, você concluiu a fase de empacotamento do processo.

>[!NOTE]
>
>Para obter informações mais detalhadas sobre ferramentas de linha de comando para empacotar conteúdo, criar políticas e muito mais, consulte [Ferramentas de linha de comando do Adobe Primetime DRM](../drm-reference-implementations/command-line-tools/command-line-tools-overview.md).
