---
title: Atualizar o arquivo WAR do License Server
description: Atualizar o arquivo WAR do License Server
copied-description: true
exl-id: a70d04e2-24a4-4848-9e9b-97467f2c1749
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# Atualizar o arquivo WAR do License Server{#update-the-license-server-war-file}

Para dar suporte a clientes que se individualizaram por meio de um servidor de Individualização Local, você deve atualizar a raiz de confiança do certificado do Servidor de Licenças para incluir a credencial da Autoridade de Certificação de Individualização recém-adquirida. Um programa em Python ( [!DNL addIndivCert.py]) está incluído na variável [!DNL update_license_server] pasta.

Faça o seguinte para atualizar o License Server:

1. Faça uma cópia dos arquivos WAR a serem atualizados (exemplos: [!DNL flashaccess.war], [!DNL faxsks.war]).
1. Certifique-se de que os arquivos WAR estejam desbloqueados e tenham suas permissões definidas para que possam ser modificados.
1. Execute o [!DNL addIndivCert.py] Script Python para atualizar os arquivos WAR do License Server.

   As entradas para o script são as seguintes:

   * `cert`: arquivo PKCS12 contendo o certificado CA de individualização
   * `war`: arquivo WAR a ser atualizado

   O arquivo de saída é um arquivo WAR atualizado.

   ```
   ./addIndivCert.py -cert NEW_IndivCA.cer -war flashaccess.war
   ```

Os arquivos WAR serão modificados no local. Se necessário, você pode editar o script Python para atender às suas necessidades específicas. Depois de executar as atualizações, você pode implantar os arquivos WAR normalmente.
