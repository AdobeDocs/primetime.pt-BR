---
description: Você pode lista de permissões seus aplicativos do sistema operacional usando a ferramenta Adobe iMachotools.
title: Lista de permissões seu aplicativo iOS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---


# Lista de permissões seu aplicativo iOS {#allowlist-your-ios-application}

Você pode lista de permissões seus aplicativos do sistema operacional usando a ferramenta Adobe iMachotools.

Geralmente, ao concluir um aplicativo TVSDK, você pode usar as ferramentas de linha de comando do Adobe Primetime DRM para lista de permissões seu aplicativo.

>[!TIP]
>
>Também é possível usar essas ferramentas para criar políticas de DRM e criptografar conteúdo.

Permitir a listagem do aplicativo garante que o conteúdo protegido só possa ser reproduzido no player de vídeo. No entanto, permitir a listagem de um aplicativo iOS requer que você conclua o procedimento especial que funciona com as políticas de envio de aplicativos da Apple.

Antes de enviar um aplicativo iOS, você precisa assiná-lo e publicá-lo na Apple.

>[!NOTE]
>
>A Apple tira a assinatura do desenvolvedor e assina novamente o aplicativo com seu próprio certificado.

Devido à reassinatura, as informações de lista de permissões geradas antes de você enviar para a Apple App Store não podem ser usadas.

Para trabalhar com essa política de envio, o Adobe criou uma ferramenta `machotools` que irá impressões digitais do aplicativo iOS para criar um valor de compilação, assinar esse valor e inserir esse valor no aplicativo iOS. Depois de imprimir a impressão digital do aplicativo iOS, envie o aplicativo para a Apple App Store. Quando um usuário executa seu aplicativo a partir da App Store, o Primetime DRM faz um cálculo em tempo de execução da impressão digital do aplicativo e o confirma com o valor de compilação inserido anteriormente no aplicativo. Se a impressão digital corresponder, o aplicativo é confirmado como permitido e o conteúdo protegido pode ser reproduzido.

A ferramenta Adobe `machotools` está incluída no SDK do TVSDK do iOS, no [!DNL [...Pasta ]/tools/DRM].

Para usar `machotools`:

1. Gere um par de chaves.

   Para usar um utilitário como OpenSSL, abra uma janela de comando e insira o seguinte:

   ```shell
   openssl genrsa -des3 -out selfsigncert-ios.key 1024
   ```

1. Quando solicitado, insira uma senha para proteger a chave privada.

   As senhas devem conter pelo menos 12 caracteres e os caracteres devem incluir uma mistura de caracteres ASCII maiúsculos e minúsculos.
1. Para usar o OpenSSL para gerar uma senha forte para você, abra uma janela de comando e insira o seguinte:

   ```shell
   openssl rand -base64 8
   ```

1. Gere uma solicitação de assinatura de certificado (CSR).

   Para usar o OpenSSL para gerar uma CSR, abra uma Janela de comando e insira o seguinte:

   ```shell
   openssl req -new -key selfsigncert-ios.key -out selfsigncert-ios.csr -batch
   ```

1. Assine o certificado automaticamente e insira qualquer duração.

   O exemplo a seguir fornece uma expiração de 20 anos:

   ```shell
   openssl x509 -req -days 7300 -in selfsigncert-ios.csr  
     -signkey selfsigncert-ios.key -out selfsigncert-ios.crt
   ```

1. Converta o certificado autoassinado em um arquivo PKCS#12:

   ```shell
   openssl pkcs12 -export -out selfsigncert-ios.pfx  
     -inkey selfsigncert-ios.key -in selfsigncert-ios.crt
   ```

   Você pode usar o certificado autoassinado para assinar o aplicativo iOS.

1. Atualize a localização do arquivo PFX e da senha.
1. Antes de criar seu aplicativo no Xcode, vá para **[!UICONTROL Build Phases]** > **[!UICONTROL Run Script]** e adicione o seguinte comando ao script de execução:

   ```shell
   mkdir -p "${PROJECT_DIR}/generatedRes" "${PROJECT_DIR}/machotools" sign  
     -in "${CODESIGNING_FOLDER_PATH}/${EXECUTABLE_NAME}"  
     -out "${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest"  
     -pfx "${PROJECT_DIR}/selfsigncert-ios.pfx"  
     -pass PASSWORD
   ```

1. Execute [!DNL machotools] para gerar o valor de hash da ID do Publicador do aplicativo.

   ```shell
   ./machotools dumpMachoSignature -in ${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest
   ```

1. Crie uma nova Política de DRM ou atualize sua política existente para incluir o valor de hash da ID do editor retornado.
1. Usando o [!DNL AdobePolicyManager.jar], crie uma nova Política de DRM (atualize sua política existente) para incluir o valor de hash da ID do editor retornado, uma ID de aplicativo opcional e os atributos de versão mín. e máx. no arquivo [!DNL flashaccess-tools.properties] incluído.

   ```shell
   java -jar libs/AdobePolicyManager.jar new app_allowlist.pol
   ```

1. Comprima o conteúdo usando a nova política de DRM e confirme a reprodução do conteúdo permitido listado no aplicativo iOS.
