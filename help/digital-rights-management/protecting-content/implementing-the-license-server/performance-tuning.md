---
title: Ajuste de desempenho
description: Ajuste de desempenho
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# Ajuste de desempenho{#performance-tuning}

Use as seguintes dicas para ajudar a aumentar o desempenho:

* O uso de um HSM de rede pode ser significativamente mais lento do que o uso de um HSM conectado diretamente.
* Para melhorar o desempenho, você pode, opcionalmente, ativar o suporte nativo para operações de criptografia, implantando as bibliotecas específicas da plataforma localizadas no [!DNL thirdparty/cryptoj] pasta do SDK. Para ativar o suporte nativo, adicione a biblioteca da sua plataforma (jsafe.dll para Windows ou libjsafe.so para Linux) ao caminho.

  >[!NOTE]
  >
  >Se você executar várias aplicações Web na mesma instância do Tomcat e tiver `jsafe.dll` no caminho, somente o primeiro aplicativo web que é carregado é capaz de carregar o `jsafe.dll` biblioteca. Portanto, somente a primeira aplicação web obtém o benefício do suporte nativo. Nesses casos, para melhorar o desempenho de todos os aplicativos web, coloque `cryptoj.jar`fora do arquivo WAR. Por exemplo, na variável `<tomcat_installation_folder>/lib` diretório.

* Um sistema operacional de 64 bits, como a versão de 64 bits do Red Hat® ou do Windows, oferece um desempenho muito melhor em relação a um sistema operacional de 32 bits.

## Gerando números aleatórios (Linux) {#section_3E2E936A538F40B7BF8892C65E117907}

Em determinadas condições, os ambientes Linux podem pausar ao realizar operações relacionadas ao Primetime DRM que exigem geração de números aleatórios, incluindo:

* Inicialização do Servidor de Licenças DRM da Adobe Primetime
* Geração de política usando o [!DNL AdobePolicyManager] utilitário
* Empacotamento de conteúdo protegido por DRM com o Adobe Media Server ou o Primetime OfflinePackager

Atrasos durante essas operações geralmente são o resultado de um pool de baixa entropia no servidor Linux.

No Linux, números aleatórios são gerados a partir do pool de entropia do ambiente do servidor. O pool de entropia é normalmente mantido ao receber interrupções de hardware pelo kernel do Linux. Se um servidor for isolado e não receber entradas regulares de recursos de hardware (como mouse ou teclado), a espera para reabastecer o pool de entropia poderá ser estendida. Nesse cenário, as operações que aguardam dados do [!DNL /dev/random] podem pausar.

Você pode usar geradores de número aleatório de hardware em servidores Linux para garantir que seja gerada entropia suficiente. No entanto, se os geradores de número aleatório de hardware não estiverem disponíveis em um determinado cenário de implantação, você poderá usar soluções baseadas em software para aumentar a taxa de atualização do pool de entropia. Uma dessas soluções de software no Linux é [!DNL haveged] (Daemon de coleta e expansão de entropia volátil de hardware).

## Determinação da entropia disponível {#section_686B311FE6144566B6939E9F20915ADC}

Para verificar o número de bits disponíveis no pool de entropia de um determinado servidor durante um atraso inesperado, execute o seguinte comando:

```
cat /proc/sys/kernel/random/entropy_avail 
```

Um sistema Linux saudável com muita entropia disponível retornará perto dos 4.096 bits completos de entropia. Se o valor retornado for menor que 200, o sistema está sendo executado com muito pouca entropia.
