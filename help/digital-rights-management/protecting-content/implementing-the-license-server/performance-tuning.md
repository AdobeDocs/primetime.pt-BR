---
seo-title: Ajuste de desempenho
title: Ajuste de desempenho
uuid: db8889c7-ecf5-4551-a6fc-1d3ab992b9ff
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Ajuste de desempenho{#performance-tuning}

Use as seguintes dicas para ajudar a aumentar o desempenho:

* O uso de um HSM de rede pode ser significativamente mais lento do que o uso de um HSM conectado diretamente.
* Para melhorar o desempenho, você pode, opcionalmente, habilitar o suporte nativo para operações criptográficas ao implantar as bibliotecas específicas da plataforma localizadas na [!DNL thirdparty/cryptoj] pasta do SDK. Para ativar o suporte nativo, adicione a biblioteca para a sua plataforma (jsafe.dll para Windows ou libjsafe.so para Linux) ao caminho.

   >[!NOTE] {class=&quot;- tópico/observação &quot;}
   >
   >Se você executar vários aplicativos da Web na mesma instância do Tomcat e tiver `jsafe.dll` no caminho, somente o primeiro aplicativo da Web que carrega é capaz de carregar a `jsafe.dll` biblioteca. Portanto, somente o primeiro aplicativo da Web obtém o benefício do suporte nativo. Nesses casos, para melhorar o desempenho de todos os aplicativos da Web, coloque-o `cryptoj.jar`fora do arquivo WAR. Por exemplo, no `<tomcat_installation_folder>/lib` diretório.

* Um sistema operacional de 64 bits, como a versão de 64 bits do Red Hat® ou do Windows, proporciona um desempenho muito melhor em relação a um sistema operacional de 32 bits.

## Gerando números aleatórios (Linux) {#section_3E2E936A538F40B7BF8892C65E117907}

Em determinadas condições, os ambientes Linux podem pausar ao realizar operações relacionadas ao DRM Primetime que exigem geração aleatória de números, incluindo:

* Inicialização do Adobe Primetime DRM License Server
* Geração de políticas usando o [!DNL AdobePolicyManager] utilitário
* Acondicionamento de conteúdo protegido por DRM com o Adobe Media Server ou o Primetime OfflinePackager

Os atrasos durante essas operações são geralmente o resultado de um pool de baixa entropia no servidor Linux.

No Linux, números aleatórios são gerados a partir do pool de entropia do ambiente do servidor. O pool de entropia normalmente é mantido recebendo interrupções de hardware pelo kernel do Linux. Se um servidor estiver isolado e não receber entradas regulares de recursos HW (como um mouse ou teclado), as esperas para reabastecer o pool de entropia poderão ser estendidas. Nesse cenário, as operações que aguardam dados de [!DNL /dev/random] podem pausar.

Você pode usar geradores de números aleatórios de hardware em servidores Linux para garantir que seja gerada entropia suficiente. Entretanto, se os geradores de números aleatórios de hardware não estiverem disponíveis em um determinado cenário de implantação, você poderá usar soluções baseadas em software para aumentar a taxa de atualização do pool de entropia. Uma dessas soluções de software no Linux é [!DNL haveged] (daemon HArdware Volatile Entropy Entropy Gathering and Expansion).

## Determinando a Entropia Disponível {#section_686B311FE6144566B6939E9F20915ADC}

Para verificar o número de bits disponíveis em um determinado pool de entropia do servidor durante um atraso inesperado, execute o seguinte comando:

```
cat /proc/sys/kernel/random/entropy_avail 
```

Um sistema Linux saudável com muita entropia disponível retornará perto dos 4.096 bits completos de entropia. Se o valor retornado for menor que 200, o sistema estará em execução com muito pouca entropia.
