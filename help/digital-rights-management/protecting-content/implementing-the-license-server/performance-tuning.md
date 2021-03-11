---
title: Ajuste de desempenho
description: Ajuste de desempenho
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# Ajuste de desempenho{#performance-tuning}

Use as seguintes dicas para ajudar a aumentar o desempenho:

* O uso de um HSM de rede pode ser significativamente mais lento do que o uso de um HSM conectado diretamente.
* Para melhorar o desempenho, opcionalmente, é possível ativar o suporte nativo para operações criptográficas, implantando as bibliotecas específicas da plataforma, localizadas na pasta [!DNL thirdparty/cryptoj] do SDK. Para ativar o suporte nativo, adicione a biblioteca para sua plataforma (jsafe.dll para Windows ou libjsafe.so para Linux) ao caminho.

   >[!NOTE]
   >
   >Se você executar várias aplicações Web na mesma instância Tomcat e tiver `jsafe.dll` no caminho, somente o primeiro aplicativo Web que carregar poderá carregar a biblioteca `jsafe.dll`. Portanto, somente a primeira aplicação web obtém o benefício do suporte nativo. Nesses casos, para melhorar o desempenho de todas as aplicações Web, coloque `cryptoj.jar`fora do arquivo WAR. Por exemplo, no diretório `<tomcat_installation_folder>/lib` .

* Um sistema operacional de 64 bits, como a versão de 64 bits do Red Hat® ou do Windows, fornece desempenho muito melhor em relação a um sistema operacional de 32 bits.

## Gerando números aleatórios (Linux) {#section_3E2E936A538F40B7BF8892C65E117907}

Em determinadas condições, os ambientes Linux podem pausar ao realizar operações relacionadas a DRM do Primetime que exigem geração de número aleatório, incluindo:

* Inicialização do servidor de licença Adobe Primetime DRM
* Geração de política usando o utilitário [!DNL AdobePolicyManager]
* Empacotando conteúdo protegido por DRM com o Adobe Medium Server ou o Primetime OfflinePackager

Os atrasos durante essas operações geralmente são o resultado de um pool de baixa entropia no servidor Linux.

No Linux, números aleatórios são gerados a partir do pool de entropia do ambiente de servidor. O pool de entropia é normalmente mantido pelo recebimento de interrupções de hardware pelo kernel do Linux. Se um servidor for isolado e não receber entradas regulares de recursos de hardware (como um mouse ou teclado), a espera para recarregar o pool de entropia poderá ser estendida. Nesse cenário, as operações que aguardam dados de [!DNL /dev/random] podem pausar.

Você pode usar geradores de números aleatórios de hardware em servidores Linux para garantir que seja gerada entropia suficiente. No entanto, se geradores de números aleatórios de hardware não estiverem disponíveis em um determinado cenário de implantação, você poderá usar soluções baseadas em software para aumentar a taxa de atualização do pool de entropia. Uma dessas soluções de software no Linux é [!DNL haveged] (HArdware Volatile Entropy Entropy Gathering and Expansion daemon).

## Determinando a Entropia Disponível {#section_686B311FE6144566B6939E9F20915ADC}

Para verificar o número de bits disponíveis em um determinado pool de entropia do servidor durante um atraso inesperado, execute o seguinte comando:

```
cat /proc/sys/kernel/random/entropy_avail 
```

Um sistema Linux saudável com muita entropia disponível retornará perto dos 4.096 bits completos de entropia. Se o valor retornado for menor que 200, o sistema estará executando com muito pouca entropia.
