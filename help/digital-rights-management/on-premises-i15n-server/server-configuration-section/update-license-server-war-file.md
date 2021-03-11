---
title: Atualizar o arquivo WAR do License Server
description: Atualizar o arquivo WAR do License Server
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---


# Atualizar o arquivo WAR do License Server{#update-the-license-server-war-file}

Para oferecer suporte a clientes que se individualizaram por meio de um servidor de individualização no local, é necessário atualizar a raiz de confiança do certificado do License Server para incluir a credencial da autoridade de certificação de individualização recém-adquirida. Um script Python ( [!DNL addIndivCert.py]) está incluído na pasta [!DNL update_license_server].

Faça o seguinte para atualizar o License Server:

1. Faça uma cópia dos arquivos WAR a serem atualizados (exemplos: [!DNL flashaccess.war], [!DNL faxsks.war]).
1. Certifique-se de que os arquivos WAR estejam desbloqueados e tenham suas permissões definidas para que possam ser modificados.
1. Execute o script [!DNL addIndivCert.py] Python para atualizar os arquivos WAR do License Server.

   As entradas para o script são as seguintes:

   * `cert`: Arquivo PKCS12 contendo o certificado da AC de individualização
   * `war`: Arquivo WAR a ser atualizado

   O arquivo de saída é um arquivo WAR atualizado.

   ```
   ./addIndivCert.py -cert NEW_IndivCA.cer -war flashaccess.war
   ```

Os arquivos WAR serão modificados. Se necessário, você pode editar o script Python para atender às suas necessidades específicas. Após executar as atualizações, é possível implantar os arquivos WAR normalmente.
