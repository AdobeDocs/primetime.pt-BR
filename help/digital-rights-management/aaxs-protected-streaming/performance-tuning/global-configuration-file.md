---
seo-title: Arquivo de configuração global
title: Arquivo de configuração global
uuid: 48c45f56-55c2-4526-b854-5552caf21541
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---


# Arquivo de configuração global{#global-configuration-file}

O maior impacto no desempenho que você pode fazer é usar as configurações no arquivo de configuração global flashaccess-global.xml. Essas configurações incluem os elementos `<Caching>` e `<Logging>`.

* `<Caching>` O  `<Caching>` elemento controla o cache de arquivos de configuração na memória. O elemento `<Caching>` tem a seguinte sintaxe:

   ```
   <Caching refreshDelaySeconds="..." numTenants="..."/>
   ```

   * `refreshDelaySeconds` controla a frequência com que o servidor verifica se há atualizações nos arquivos de configuração. Um valor baixo para `refreshDelaySeconds` afeta negativamente o desempenho, enquanto um valor mais alto pode melhorar o desempenho. Para obter mais informações sobre `refreshDelaySeconds`, consulte &quot;[Atualizando arquivos de configuração](../../aaxs-protected-streaming/updating-configuration-files/updating-configuration-files-overview.md)&quot;.

   * `numTenants` especifica o número de inquilinos. Um valor inferior ao número de locatários provavelmente afeta o desempenho porque as solicitações dos locatários restantes resultam em erros de cache. Uma falha no cache para dados de configuração afeta negativamente o desempenho. Portanto, o Adobe recomenda que você defina esse valor acima do número de locatários configurados para o servidor, a menos que haja limitações de memória a serem consideradas.

* `<Logging>` O  `<Logging>` elemento especifica o nível de log e a frequência com que os arquivos de log são rolados. O elemento `<Logging>` tem a seguinte sintaxe:

   ```
   <Logging level="..." rollingFrequency=""/>
   ```

   * `level` especifica as mensagens a serem registradas. Um valor de &quot;DEBUG&quot; gera muitas mensagens de log e pode afetar negativamente o desempenho. O Adobe recomenda uma configuração de &quot;WARN&quot; para obter um desempenho ótimo. No entanto, esse valor corre o risco de perder informações essenciais do tempo de execução, como auditorias de licenças. Para preservar informações valiosas de log com impacto mínimo no desempenho, use um valor de &quot;INFO&quot;.
   * `rollingFrequency` especifica a frequência com que os arquivos de log são  *rolados*. Rolling é o processo no qual um novo arquivo de log se torna o log ativo, enquanto o arquivo de log anteriormente ativo não é mais gravado e é considerado como rolado. O intervalo de rolagem pode ser definido como &quot;MINUTELY&quot;, &quot;HOURLY&quot;, &quot;DUAS VEZES POR DIA&quot;, &quot;DAILY&quot;, &quot;WEEKLY&quot;, &quot;MONTHLY&quot; ou &quot;NUNCA&quot;.

Consulte *Usar o SDK de acesso ao Adobe para proteger conteúdo* para obter dicas adicionais sobre como otimizar o desempenho.
