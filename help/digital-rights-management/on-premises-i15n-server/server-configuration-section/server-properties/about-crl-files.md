---
title: Sobre Arquivos CRL
description: Sobre Arquivos CRL
copied-description: true
exl-id: 126a323d-9433-4a1e-a617-2d3bbf717cce
source-git-commit: 6a00df9c061da43f6efa49d927873db629568597
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# Sobre Arquivos CRL {#about-crl-files}

Para funcionar corretamente, os servidores de Individualização e Licença precisam ter vários arquivos da Lista de Revogação de Certificados (CRL) armazenados em cache no disco no servidor de aplicativos em execução (por exemplo, Tomcat). Os novos arquivos CRL devem ser baixados e armazenados em cache no disco regularmente e de acordo com uma programação. Se o período de validade dos arquivos CRL no disco expirar, o Servidor de individualização se recusará a individualizar os clientes e o Servidor de licenças se recusará a emitir licenças.

As CRLs armazenadas em cache no disco devem ter nomes de arquivo que correspondam às URLs correspondentes. Caracteres especiais, como dois pontos &#39;:&#39; e barras &#39;/&#39; são convertidos em sublinhados &#39;_&#39; nos nomes de arquivo.

Veja a seguir uma lista de CRLs hospedadas externamente que são usadas pelos Servidores de Individualização e de Licença:

* **CRL Intermediária:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl>]
   * Arquivo: [!DNL http___crl2.adobe.com_Adobe_FlashAccessIntermediateCA.crl]
   * Validade: bom por aproximadamente 12 meses a partir da criação

* **CRL Raiz:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessRootCA.crl>]
   * Arquivo: [!DNL http___crl2.adobe.com_Adobe_FlashAccessRootCA.crl]
   * Validade: bom por aproximadamente 5 anos a partir da criação

* **Lista de Certificados Revogados Mais Recente:**

   * URL: [!DNL <ht<span></span>tps://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl>]
   * Arquivo: [!DNL http___crl3.adobe.com_AdobeSystemsIncorporatedFlashAccessRuntime_LatestCRL.crl]
   * Validade: bom por aproximadamente 3 meses a partir da criação

Para saber mais sobre as CRLs hospedadas externamente que podem ser usadas pelos Servidores de Licença, entre em contato com o Suporte do Adobe.

<!---

Commenting out because of a security vulnerability reported in Jira PSIRT-20689. 

The following are externally hosted CRLs that are used only by the License Servers:

* URL: `https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl`

* File: `http___crl2.adobe.com_Adobe_FlashAccessIndividualizationCA.crl`

* Validity: Good for approximately 3 months from creation

* URL: `https://individualization-crl.primetime.adobe.com/FlashAccessIndividualizationCA.crl`

* File: `http___individualization-crl.primetime.adobe.com_FlashAccessIndividualizationCA.crl`

* Validity: Good for approximately 3 months from creation

* URL: `https://individualization-crl.s3-website-us-east-1.amazonaws.com/FlashAccessIndividualizationCA.crl`

* File: `http___individualization-crl.s3-website-us-east-1.amazonaws.com_FlashAccessIndividualizationCA.crl`

* Validity: Good for approximately 3 months from creation

--->

Além das CRLs hospedadas externamente, você pode criar e manter uma CRL adicional. Esta é a CRL de CA de individualização, conforme especificado na [Criar CRL de CA de Individualização](../../../on-premises-i15n-server/server-configuration-section/server-properties/create-i15n-ca-crl.md) seção deste documento.

As CRLs devem ser atualizadas 45 dias antes da expiração. Isso deve permitir que você tenha tempo adequado para adquirir e instalar CRLs recém-geradas da Internet. Atualize os arquivos CRL com cautela antes que eles expirem.
