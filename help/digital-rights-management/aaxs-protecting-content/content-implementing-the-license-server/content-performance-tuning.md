---
title: Ajuste de desempenho
description: Ajuste de desempenho
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# Ajuste de desempenho{#performance-tuning}

Use as seguintes dicas para ajudar a aumentar o desempenho:

* O uso de um HSM de rede pode ser significativamente mais lento do que o uso de um HSM conectado diretamente.
* Para melhorar o desempenho, você pode ativar o suporte nativo para operações de criptografia implantando as bibliotecas específicas da plataforma localizadas na pasta &quot;thirdparty/cryptoj&quot; do SDK. Para ativar o suporte nativo, adicione a biblioteca da sua plataforma (jsafe.dll para Windows ou libjsafe.so para Linux) ao caminho.

  >[!NOTE]
  >
  >Se você executar várias aplicações Web na mesma instância do Tomcat e tiver `jsafe.dll` no caminho, somente o primeiro aplicativo web que é carregado é capaz de carregar o `jsafe.dll` biblioteca. Portanto, somente a primeira aplicação web obtém o benefício do suporte nativo. Nesses casos, para melhorar o desempenho de todos os aplicativos web, coloque `cryptoj.jar`fora do arquivo WAR. Por exemplo, na variável `<tomcat_installation_folder>/lib` diretório.

* Um sistema operacional de 64 bits, como a versão de 64 bits do Red Hat® ou do Windows, oferece um desempenho muito melhor em relação a um sistema operacional de 32 bits.
