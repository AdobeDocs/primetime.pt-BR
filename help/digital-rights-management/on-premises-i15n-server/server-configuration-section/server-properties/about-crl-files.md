---
seo-title: Sobre arquivos CRL
title: Sobre arquivos CRL
uuid: 672c3ca0-5c5d-4ec7-83b1-f0f8e34c8d09
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Sobre arquivos CRL {#about-crl-files}

Para funcionarem corretamente, os servidores Individualization e License precisam ter vários arquivos CRL (Certificate Revocation List, lista de revogação de certificado) armazenados em cache no disco no servidor de aplicativos em execução (por exemplo, Tomcat). Os novos arquivos CRL devem ser baixados e armazenados em cache em disco regularmente e de forma programada. Se o período de validade dos arquivos CRL no disco for cancelado, o servidor de individualização se recusará a individualizar clientes e o servidor de licença se recusará a emitir licenças.

As CRLs armazenadas em cache no disco devem ter nomes de arquivos que correspondam aos URLs correspondentes. Caracteres especiais como dois pontos &#39;:&#39; e &#39;/&#39; barras são convertidos em sublinhados &#39;_&#39; nos nomes dos arquivos.

Esta é uma lista de CRLs hospedadas externamente usadas pelos Servidores de individuais e de licenças:

* **LCR Intermediário:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl>]
   * Arquivo: [!DNL http___crl2.adobe.com_Adobe_FlashAccessIntermediateCA.crl]
   * Validade: Bom por aproximadamente 12 meses a partir da criação

* **CRL raiz:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessRootCA.crl>]
   * Arquivo: [!DNL http___crl2.adobe.com_Adobe_FlashAccessRootCA.crl]
   * Validade: Bom por aproximadamente 5 anos a partir da criação

* **Última CRL:**

   * URL: [!DNL <ht<span></span>tps://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl>]
   * Arquivo: [!DNL http___crl3.adobe.com_AdobeSystemsIncorporatedFlashAccessRuntime_LatestCRL.crl]
   * Validade: Bom por aproximadamente 3 meses a partir da criação

A seguir estão as CRLs hospedadas externamente usadas somente pelos Servidores de licença:

* URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl>]
* Arquivo: [!DNL http___crl2.adobe.com_Adobe_FlashAccessIndividualizationCA.crl]
* Validade: Bom por aproximadamente 3 meses a partir da criação

* URL: [!DNL <ht<span></span>tps://individualization-crl.primetime.adobe.com/FlashAccessIndividualizationCA.crl>]
* Arquivo: [!DNL http___individualization-crl.primetime.adobe.com_FlashAccessIndividualizationCA.crl]
* Validade: Bom por aproximadamente 3 meses a partir da criação

* URL: [!DNL <ht<span></span>tps://individualization-crl.s3-website-us-east-1.amazonaws.com/FlashAccessIndividualizationCA.crl]>
* Arquivo: [!DNL http___individualization-crl.s3-website-us-east-1.amazonaws.com_FlashAccessIndividualizationCA.crl]
* Validade: Bom por aproximadamente 3 meses a partir da criação

Além das CRLs acima mencionadas, você deve criar e manter uma CRL adicional. Esta é a CRL da CA de individualização, conforme especificado na seção [Criar CRL](../../../on-premises-i15n-server/server-configuration-section/server-properties/create-i15n-ca-crl.md) da CA de personalização deste documento.

As CRLs estão programadas para serem atualizadas 45 dias antes de expirarem. Isso deve permitir que você obtenha e instale CRLs recém-gerados pela Internet. Você deve ter cuidado para atualizar os arquivos CRL antes de expirarem.
