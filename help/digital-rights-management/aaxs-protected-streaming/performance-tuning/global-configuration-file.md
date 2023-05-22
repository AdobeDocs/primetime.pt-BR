---
title: Arquivo de configuração global
description: Arquivo de configuração global
copied-description: true
exl-id: 109e6e5b-4bb5-43dc-b11e-50799a346a28
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# Arquivo de configuração global{#global-configuration-file}

O maior impacto no desempenho que você pode causar é o uso de definições no arquivo de configuração global, flashaccess-global.xml. Essas configurações incluem o `<Caching>` e `<Logging>` elementos.

* `<Caching>` A variável `<Caching>` os controles de elemento armazenam arquivos de configuração em cache na memória. A variável `<Caching>` O elemento tem a seguinte sintaxe:

   ```
   <Caching refreshDelaySeconds="..." numTenants="..."/>
   ```

   * `refreshDelaySeconds` controla a frequência com que o servidor verifica se há atualizações nos arquivos de configuração. Um valor baixo para `refreshDelaySeconds` afeta negativamente o desempenho, enquanto um valor mais alto pode melhorar o desempenho. Para obter mais informações sobre `refreshDelaySeconds`, consulte &quot;[Atualização de arquivos de configuração](../../aaxs-protected-streaming/updating-configuration-files/updating-configuration-files-overview.md)&quot;.

   * `numTenants` especifica o número de locatários. Um valor menor que o número de locatários provavelmente afeta o desempenho, pois as solicitações aos locatários restantes resultam em erros de cache. Uma perda de cache para dados de configuração afeta negativamente o desempenho. Portanto, a Adobe recomenda que você defina esse valor como maior que o número de locatários configurados para o servidor, a menos que haja limitações de memória a serem consideradas.

* `<Logging>` A variável `<Logging>` element especifica o nível de log e a frequência de rolagem dos arquivos de log. A variável `<Logging>` O elemento tem a seguinte sintaxe:

   ```
   <Logging level="..." rollingFrequency=""/>
   ```

   * `level` especifica as mensagens a serem registradas. Um valor &quot;DEBUG&quot; gera muitas mensagens de log e pode afetar negativamente o desempenho. A Adobe recomenda uma configuração de &quot;AVISO&quot; para obter o desempenho ideal. No entanto, esse valor corre o risco de perder informações essenciais de tempo de execução, como auditorias de licença. Para preservar informações valiosas de registro com impacto mínimo no desempenho, use o valor &quot;INFO&quot;.
   * `rollingFrequency` especifica a frequência com que os arquivos de log são *rolados*. Em andamento é o processo no qual um novo arquivo de log se torna o log ativo, enquanto o arquivo de log ativo anteriormente não é mais gravado e é considerado como implantado. O intervalo contínuo pode ser definido como &quot;MINUTELY&quot;, &quot;HOURLY&quot;, &quot;TWICE-DAILY&quot;, &quot;DAILY&quot;, &quot;WEEKLY&quot;, &quot;MONTHLY&quot; ou &quot;NEVER&quot;.

Consulte *Utilização do SDK do Adobe Access para proteção de conteúdo* para obter dicas adicionais sobre como otimizar o desempenho.
