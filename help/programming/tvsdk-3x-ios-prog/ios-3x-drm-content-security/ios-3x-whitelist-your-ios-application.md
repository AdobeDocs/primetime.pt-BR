---
description: Você pode adicionar aplicativos iOS à lista de permissões usando a ferramenta de ferramentas da Adobe.
seo-description: Você pode adicionar aplicativos iOS à lista de permissões usando a ferramenta de ferramentas da Adobe.
seo-title: Lista de permissões do aplicativo iOS
title: Lista de permissões do aplicativo iOS
uuid: bc558f5f-d4e6-4c1c-81eb-f8bd61c63016
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Lista de permissões do aplicativo iOS {#whitelist-your-ios-application}

Você pode adicionar aplicativos iOS à lista de permissões usando a ferramenta de ferramentas da Adobe.

Geralmente, ao concluir um aplicativo TVSDK, você pode usar as ferramentas de linha de comando do Adobe Primetime DRM para adicionar o aplicativo à lista de permissões.

>[!TIP]
>
>Você também pode usar essas ferramentas para criar políticas de DRM e criptografar conteúdo.

A lista de permissões do aplicativo garante que o conteúdo protegido só possa ser reproduzido no player de vídeo. No entanto, a lista de permissões de um aplicativo iOS exige que você conclua um procedimento especial que funcione com as políticas de envio de aplicativos da Apple.

Antes de enviar um aplicativo iOS, você precisa assiná-lo e publicá-lo na Apple.

>[!NOTE]
>
>A Apple tira a assinatura do seu desenvolvedor e assina novamente o aplicativo com seu próprio certificado.

Devido à nova assinatura, as informações da lista de permissões geradas antes de serem enviadas para a Apple App Store não podem ser usadas.

Para trabalhar com essa política de envio, a Adobe criou uma `machotools` ferramenta que irá imprimir a impressão digital do aplicativo iOS para criar um valor de compilação, assinar esse valor e inserir esse valor no aplicativo iOS. Após a impressão digital do aplicativo iOS, envie o aplicativo para a Apple App Store. Quando um usuário executa seu aplicativo a partir da App Store, o Primetime DRM faz um cálculo em tempo de execução da impressão digital do aplicativo e o confirma com o valor de compilação anteriormente inserido no aplicativo. Se a impressão digital corresponder, o aplicativo será confirmado como sendo exibido na lista de permissões e o conteúdo protegido poderá ser reproduzido.

A ferramenta Adobe `machotools` está incluída no SDK TVSDK do iOS, no [!DNL [..]pasta /tools/DRM].

Para usar `machotools`:

1. Gere um par de chaves.

   Para usar um utilitário como OpenSSL, abra uma janela de comando e digite o seguinte:

   ```
   openssl genrsa -des3 -out selfsigncert-ios.key 1024
   ```

1. Quando solicitado, digite uma senha para proteger a chave privada.

   As senhas devem conter pelo menos 12 caracteres e os caracteres devem incluir uma mistura de caracteres ASCII maiúsculos e minúsculos.
1. Para usar o OpenSSL para gerar uma senha forte para você, abra uma janela de comando e digite o seguinte:

   ```
   openssl rand -base64 8
   ```

1. Gerar uma solicitação de assinatura de certificado (CSR).

   Para usar o OpenSSL para gerar um CSR, abra uma Janela de Comando e insira o seguinte:

   ```
   openssl req -new -key selfsigncert-ios.key -out selfsigncert-ios.csr -batch
   ```

1. Assine o certificado automaticamente e insira qualquer duração.

   O exemplo a seguir fornece uma expiração de 20 anos:

   ```
   openssl x509 -req -days 7300 -in selfsigncert-ios.csr  
     -signkey selfsigncert-ios.key -out selfsigncert-ios.crt
   ```

1. Converta o certificado autoassinado em um arquivo PKCS#12:

   ```
   openssl pkcs12 -export -out selfsigncert-ios.pfx  
     -inkey selfsigncert-ios.key -in selfsigncert-ios.crt
   ```

   Você pode usar o certificado autoassinado para assinar seu aplicativo iOS.

1. Atualize o local do arquivo PFX e da senha.
1. Antes de criar seu aplicativo no Xcode, vá até **[!UICONTROL Build Phases]** > **[!UICONTROL Run Script]** e adicione o seguinte comando ao script de execução:

   ```
   mkdir -p "${PROJECT_DIR}/generatedRes" "${PROJECT_DIR}/machotools" sign  
     -in "${CODESIGNING_FOLDER_PATH}/${EXECUTABLE_NAME}"  
     -out "${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest"  
     -pfx "${PROJECT_DIR}/selfsigncert-ios.pfx"  
     -pass PASSWORD
   ```

1. Execute [!DNL machotools] para gerar o valor de hash da ID do editor do aplicativo.

   ```
   ./machotools dumpMachoSignature -in ${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest
   ```

1. Crie uma nova Política DRM ou atualize sua política existente para incluir o valor de hash da ID do editor retornado.
1. Usando o [!DNL AdobePolicyManager.jar], crie uma nova Política DRM (atualize sua política existente) para incluir o valor de hash da ID do editor retornado, uma ID do aplicativo opcional e os atributos de versão mín. e máx. no arquivo incluído [!DNL flashaccess-tools.properties] .

   ```
   java -jar libs/AdobePolicyManager.jar new app_whitelist.pol
   ```

1. Compacte o conteúdo usando a nova política de DRM e confirme a reprodução do conteúdo da lista de permissões no aplicativo iOS.