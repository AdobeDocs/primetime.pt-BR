---
title: Sobre arquivos CRL
description: Sobre arquivos CRL
copied-description: true
exl-id: 126a323d-9433-4a1e-a617-2d3bbf717cce
source-git-commit: 6a00df9c061da43f6efa49d927873db629568597
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# Sobre arquivos CRL {#about-crl-files}

Para funcionar corretamente, os servidores de Individualização e Licença precisam ter vários arquivos da Lista de Revogação de Certificados (CRL) armazenados em cache no disco no servidor de aplicativos em execução (por exemplo, Tomcat). Os novos arquivos CRL devem ser baixados e armazenados em cache no disco regularmente e de forma programada. Se o período de validade dos arquivos CRL no disco puder diminuir, o Servidor de individualização se recusará a individualizar clientes e o License Server se recusará a emitir licenças.

As CRLs armazenadas em cache no disco devem ter nomes de arquivo que correspondam aos URLs correspondentes. Caracteres especiais, como dois pontos &#39;:&#39; e barras &#39;/&#39; são convertidos em sublinhados &#39;_&#39; nos nomes dos arquivos.

Esta é uma lista de CRLs hospedadas externamente usadas pelos Servidores de Individualização e Licença:

* **CRL intermediário:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl>]
   * Arquivo: [!DNL http___crl2.adobe.com_Adobe_FlashAccessIntermediateCA.crl]
   * Validade: Bom por aproximadamente 12 meses após a criação

* **CRL raiz:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessRootCA.crl>]
   * Arquivo: [!DNL http___crl2.adobe.com_Adobe_FlashAccessRootCA.crl]
   * Validade: Bom por aproximadamente 5 anos após a criação

* **CRL mais recente:**

   * URL: [!DNL <ht<span></span>tps://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl>]
   * Arquivo: [!DNL http___crl3.adobe.com_AdobeSystemsIncorporatedFlashAccessRuntime_LatestCRL.crl]
   * Validade: Bom por aproximadamente 3 meses após a criação

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

Além das CRLs hospedadas externamente, você pode criar e manter uma CRL adicional. Esta é a CRL da CA de individualização, conforme especificado na variável [Criar CRL da CA de individualização](../../../on-premises-i15n-server/server-configuration-section/server-properties/create-i15n-ca-crl.md) seção deste documento.

As CRLs são programadas para serem atualizadas 45 dias antes de expirarem. Isso deve permitir que você tenha tempo adequado para adquirir e instalar CRLs recém-gerados pela Internet. Você deve tomar cuidado para atualizar arquivos CRL antes que eles expirem.
