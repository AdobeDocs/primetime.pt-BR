---
seo-title: Conteúdo criptografado pelo pacote
title: Conteúdo criptografado pelo pacote
uuid: 1e271167-107d-41df-8a7c-3075cb3acc0c
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Conteúdo criptografado pelo pacote{#package-encrypted-content}

1. Copie o `<Primetime DRM DVD>\Reference Implementation\Command Line Tools\` diretório para o sistema de arquivos local.
1. Na sua `Command Line Tools\` pasta local, atualize o `flashaccesstools.properties` arquivo para trabalhar com o servidor.

   Você deve modificar pelo menos as seguintes propriedades:

   * `encrypt.keys.asymmetric.certfile=[license-server-certificate.cer]`: O caminho para o Certificado do License Server (normalmente termina com [!DNL .cer], [!DNL .der] ou [!DNL .pem]).

   * `encrypt.license.serverurl=[license-server-url]`: URL do servidor de licenças, por exemplo:    `https://<License Server Hostname>:8080/flashaccessserver/sampletenant`.

   * `encrypt.license.servercert=[transport-certificate.cer]`: O caminho para o certificado de Transporte (normalmente termina com [!DNL .cer], [!DNL .der]ou [!DNL .pem]).

   * `encrypt.sign.certfile=[packager-credentials.pfx]`: O caminho para o certificado do Packager (termina com [!DNL .pfx]).

   * `encrypt.sign.certpass=[password]`: A senha do seu certificado do Packager.
   >[!NOTE]
   >
   >Certifique-se de não colocar a senha em ordem.

1. Criar uma política.

   Na sua `Command Line Tools\` pasta local, execute o seguinte comando:

   ```
   java -jar libs/AdobePolicyManager.jar new examplepolicy.pol -n examplepolicy -x
   ```

   Esse comando cria um arquivo de política chamado [!DNL examplepolicy.pol] que usa autenticação de servidor de licença anônima (a `-x` opção).
1. Copie o arquivo de vídeo MP4, FLV ou F4V que você deseja criptografar na sua `Command Line Tools\` pasta local.
1. Empacote seu conteúdo.

   Digamos que seu arquivo de vídeo de origem esteja [!DNL sample.mp4]. Na sua `Command Line Tools\` pasta local, execute o seguinte comando:

   ```
   java -jar libs/AdobePackager.jar sample.mp4 sample_encrypted.mp4 -p examplepolicy.pol
   ```

   >[!NOTE]
   >
   >Se quiser disponibilizar conteúdo HLS, HDS ou DASH, você deve usar uma ferramenta Packager diferente, como o [Adobe Primetime Offline Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf).

1. Copie os artefatos de arquivo criptografados (neste caso [!DNL sample_encrypted.mp4] e [!DNL sample_encrypted.mp4.metadata]) para `<Your Content Server - Tomcat Install Dir>\webapps\ROOT`.

Nesse ponto, você concluiu a fase de empacotamento do processo.

>[!NOTE]
>
>Para obter informações mais detalhadas sobre ferramentas de linha de comando para empacotar conteúdo, criar políticas e muito mais, consulte Ferramentas [de linha de comando do DRM do](../drm-reference-implementations/command-line-tools/command-line-tools-overview.md)Adobe Primetime.
