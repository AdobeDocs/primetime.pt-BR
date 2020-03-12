---
seo-title: Atualize o arquivo WAR do License Server
title: Atualize o arquivo WAR do License Server
uuid: 0cde53d6-185d-4bf2-84fc-0c31d17904a8
translation-type: tm+mt
source-git-commit: 1547eb3dd220fafc08df923f40504736c16a866c

---


# Atualize o arquivo WAR do License Server{#update-the-license-server-war-file}

Para dar suporte aos clientes que se individualizaram por meio de um servidor de Individualização no Local, é necessário atualizar a raiz de confiança do certificado do License Server para incluir a credencial da AC de Individualização recém-adquirida. Um script Python ( [!DNL addIndivCert.py]) está incluído na [!DNL update_license_server] pasta.

Faça o seguinte para atualizar o License Server:

1. Faça uma cópia dos arquivos WAR a serem atualizados (exemplos: [!DNL flashaccess.war], [!DNL faxsks.war]).
1. Certifique-se de que os arquivos WAR estejam desbloqueados e tenham suas permissões definidas para que possam ser modificados.
1. Execute o script [!DNL addIndivCert.py] Python para atualizar os arquivos WAR do License Server.

   As entradas para o script são as seguintes:

   * `cert`: Arquivo PKCS12 contendo o certificado da AC de personalização
   * `war`: Arquivo WAR a ser atualizado
   O arquivo de saída é um arquivo WAR atualizado.

   ```
   ./addIndivCert.py -cert NEW_IndivCA.cer -war flashaccess.war
   ```

Os arquivos WAR serão modificados no lugar. Se necessário, você pode editar o script Python para atender às suas necessidades específicas. Depois de executar as atualizações, você pode implantar os arquivos WAR normalmente.
