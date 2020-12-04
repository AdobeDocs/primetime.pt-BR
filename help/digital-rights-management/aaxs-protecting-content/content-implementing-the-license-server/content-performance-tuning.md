---
seo-title: Ajuste de desempenho
title: Ajuste de desempenho
uuid: bb5321a0-48ef-49cb-aaf0-00d7ab9562fe
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---


# Ajuste de desempenho{#performance-tuning}

Use as seguintes dicas para ajudar a aumentar o desempenho:

* O uso de um HSM de rede pode ser significativamente mais lento do que o uso de um HSM conectado diretamente.
* Para melhorar o desempenho, você pode, opcionalmente, habilitar o suporte nativo para operações criptográficas, implantando as bibliotecas específicas da plataforma localizadas na pasta &quot;thirdparty/cryptoj&quot; do SDK. Para ativar o suporte nativo, adicione a biblioteca para a sua plataforma (jsafe.dll para Windows ou libjsafe.so para Linux) ao caminho.

   >[!NOTE]
   >
   >Se você executar vários aplicativos da Web na mesma instância do Tomcat e tiver `jsafe.dll` no caminho, somente o primeiro aplicativo da Web que carrega poderá carregar a biblioteca `jsafe.dll`. Portanto, somente o primeiro aplicativo da Web obtém o benefício do suporte nativo. Nesses casos, para melhorar o desempenho de todos os aplicativos da Web, coloque `cryptoj.jar`fora do arquivo WAR. Por exemplo, no diretório `<tomcat_installation_folder>/lib`.

* Um sistema operacional de 64 bits, como a versão de 64 bits do Red Hat® ou do Windows, proporciona um desempenho muito melhor em relação a um sistema operacional de 32 bits.

