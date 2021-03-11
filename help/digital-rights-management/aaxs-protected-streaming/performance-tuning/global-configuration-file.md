---
title: Arquivo de configuração global
description: Arquivo de configuração global
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---


# Arquivo de configuração global{#global-configuration-file}

O maior impacto no desempenho que você pode fazer é usar configurações no arquivo de configuração global, flashaccess-global.xml. Essas configurações incluem os elementos `<Caching>` e `<Logging>`.

* `<Caching>` O  `<Caching>` elemento controla o armazenamento em cache dos arquivos de configuração na memória. O elemento `<Caching>` tem a seguinte sintaxe:

   ```
   <Caching refreshDelaySeconds="..." numTenants="..."/>
   ```

   * `refreshDelaySeconds` controla a frequência com que o servidor verifica se há atualizações nos arquivos de configuração. Um valor baixo para `refreshDelaySeconds` afeta negativamente o desempenho, enquanto um valor mais alto pode melhorar o desempenho. Para obter mais informações sobre `refreshDelaySeconds`, consulte &quot;[Atualizando arquivos de configuração](../../aaxs-protected-streaming/updating-configuration-files/updating-configuration-files-overview.md)&quot;.

   * `numTenants` especifica o número de locatários. Um valor menor que o número de locatários provavelmente afeta o desempenho porque as solicitações aos locatários restantes resultam em erros de cache. Uma perda de cache para dados de configuração afeta negativamente o desempenho. Portanto, o Adobe recomenda que você defina esse valor superior ao número de locatários configurados para o servidor, a menos que haja limitações de memória a serem consideradas.

* `<Logging>` O  `<Logging>` elemento especifica o nível de log e a frequência com que os arquivos de log são rolados. O elemento `<Logging>` tem a seguinte sintaxe:

   ```
   <Logging level="..." rollingFrequency=""/>
   ```

   * `level` especifica as mensagens a serem registradas. Um valor &quot;DEBUG&quot; gera muitas mensagens de log e pode afetar negativamente o desempenho. O Adobe recomenda uma configuração de &quot;AVISO&quot; para obter o desempenho ideal. No entanto, esse valor corre o risco de perder informações essenciais de tempo de execução, como auditorias de licenças. Para preservar informações valiosas de log com impacto mínimo no desempenho, use um valor &quot;INFO&quot;.
   * `rollingFrequency` especifica a frequência com que os arquivos de log são  *rolados*. O Acumulado é o processo no qual um novo arquivo de log se torna o log ativo, enquanto o arquivo de log anteriormente ativo não é mais gravado e é considerado acumulado. O intervalo acumulado pode ser definido como &quot;MINUTELY&quot;, &quot;HORA&quot;, &quot;DUAS VEZES AO DIA&quot;, &quot;DAILY&quot;, &quot;WEEKLY&quot;, &quot;MONTHLY&quot; ou &quot;NUNCA&quot;.

Consulte *Usar o SDK de acesso ao Adobe para proteger o conteúdo* para obter dicas adicionais sobre como otimizar o desempenho.
