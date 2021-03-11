---
title: Ajuste de desempenho
description: Ajuste de desempenho
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---


# Ajuste de desempenho{#performance-tuning}

Use as seguintes dicas para ajudar a aumentar o desempenho:

* O uso de um HSM de rede pode ser significativamente mais lento do que o uso de um HSM conectado diretamente.
* Para melhorar o desempenho, opcionalmente, é possível ativar o suporte nativo para operações criptográficas, implantando as bibliotecas específicas da plataforma localizadas na pasta &quot;thirdparty/cryptoj&quot; do SDK. Para ativar o suporte nativo, adicione a biblioteca para sua plataforma (jsafe.dll para Windows ou libjsafe.so para Linux) ao caminho.

   >[!NOTE]
   >
   >Se você executar várias aplicações Web na mesma instância Tomcat e tiver `jsafe.dll` no caminho, somente o primeiro aplicativo Web que carregar poderá carregar a biblioteca `jsafe.dll`. Portanto, somente a primeira aplicação web obtém o benefício do suporte nativo. Nesses casos, para melhorar o desempenho de todas as aplicações Web, coloque `cryptoj.jar`fora do arquivo WAR. Por exemplo, no diretório `<tomcat_installation_folder>/lib` .

* Um sistema operacional de 64 bits, como a versão de 64 bits do Red Hat® ou do Windows, fornece desempenho muito melhor em relação a um sistema operacional de 32 bits.

