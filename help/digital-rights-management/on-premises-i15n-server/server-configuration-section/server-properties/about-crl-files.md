---
title: Sobre arquivos CRL
description: Sobre arquivos CRL
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '305'
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

As seguintes são CRLs hospedadas externamente usadas apenas pelos Servidores de Licença:

* URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl>]
* Arquivo: [!DNL http___crl2.adobe.com_Adobe_FlashAccessIndividualizationCA.crl]
* Validade: Bom por aproximadamente 3 meses após a criação

* URL: [!DNL <ht<span></span>tps://individualization-crl.primetime.adobe.com/FlashAccessIndividualizationCA.crl>]
* Arquivo: [!DNL http___individualization-crl.primetime.adobe.com_FlashAccessIndividualizationCA.crl]
* Validade: Bom por aproximadamente 3 meses após a criação

* URL: [!DNL <ht<span></span>tps://individualization-crl.s3-website-us-east-1.amazonaws.com/FlashAccessIndividualizationCA.crl]>
* Arquivo: [!DNL http___individualization-crl.s3-website-us-east-1.amazonaws.com_FlashAccessIndividualizationCA.crl]
* Validade: Bom por aproximadamente 3 meses após a criação

Além dos CRLs mencionados anteriormente, você deve criar e manter um CRL adicional. Esta é a CRL da CA de individualização, conforme especificado na seção [Create Individualization CA CRL](../../../on-premises-i15n-server/server-configuration-section/server-properties/create-i15n-ca-crl.md) deste documento.

As CRLs são programadas para serem atualizadas 45 dias antes de expirarem. Isso deve permitir que você tenha tempo adequado para adquirir e instalar CRLs recém-gerados pela Internet. Você deve tomar cuidado para atualizar arquivos CRL antes que eles expirem.
