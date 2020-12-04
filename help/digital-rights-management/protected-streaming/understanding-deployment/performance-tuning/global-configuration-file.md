---
description: Este tópico descreve as considerações relacionadas ao desempenho. Todas as configurações no arquivo de configuração global chamado flashaccess-global.xml afetam o desempenho.
seo-description: Este tópico descreve as considerações relacionadas ao desempenho. Todas as configurações no arquivo de configuração global chamado flashaccess-global.xml afetam o desempenho.
seo-title: Arquivo de configuração global
title: Arquivo de configuração global
uuid: 254925b5-d441-4a35-ad6f-f99db5de7591
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---


# Ajuste de desempenho {#performance-tuning}

Este tópico descreve as considerações relacionadas ao desempenho. Todas as configurações no arquivo de configuração global chamado flashaccess-global.xml afetam o desempenho.

## Arquivo de configuração global {#global-configuration-file}

O arquivo de configuração inclui os seguintes elementos de configuração:

* `<Caching>` O  `<Caching>` elemento controla o cache de arquivos de configuração na memória. O elemento `<Caching>` suporta a seguinte sintaxe:

```
  <Caching refreshDelaySeconds="..." numTenants="..."/>
```

* `refreshDelaySeconds` Controla a frequência com que o servidor verifica se há atualizações nos arquivos de configuração. Um valor baixo para `refreshDelaySeconds` afeta negativamente o desempenho, enquanto um valor mais alto pode melhorar o desempenho.

   Consulte *Atualizando arquivos de configuração* para obter mais informações sobre `refreshDelaySeconds`.

* `numTenants` especifica o número de inquilinos. Um valor inferior ao número de inquilinos afeta o desempenho, pois as solicitações dos inquilinos restantes resultam em erros de cache. Uma falha de cache em qualquer dado de configuração afeta negativamente o desempenho. Portanto, recomenda-se que você defina esse valor acima do número de locatários configurados para o servidor, a menos que haja limitações de memória que precisam ser consideradas.

* `<Logging>` O  `<Logging>` elemento especifica o nível de log e a frequência com que os arquivos de log são rolados. O elemento `<Logging>` suporta a seguinte sintaxe:

   ```
   <Logging level="..." rollingFrequency="..."/>
   ```

* `<level>`  `level` especifica mensagens a um log. Um valor de `DEBUG` gera muitas mensagens de registro, o que pode afetar negativamente o desempenho. É recomendável aplicar uma configuração de `WARN` para obter o desempenho ideal. No entanto, esse valor pode resultar na perda de informações essenciais do tempo de execução, como auditorias de licença. Se quiser salvar as informações do log com impacto mínimo no desempenho, é necessário aplicar um valor de `INFO`.

* `<rollingFrequency>`  `rollingFrequency` especifica a frequência com que os arquivos de log são  *rolados*. *`Rolling`* é um processo que designa qualquer novo arquivo de log como um log ativo. Portanto, o arquivo de log anteriormente ativo não pode mais ser modificado e é considerado *`rolled`*. Você pode definir o intervalo de rolagem como `MINUTELY`, `HOURLY`, `TWICE-DAILY`, `DAILY`, `WEEKLY`, `MONTHLY` ou `NEVER`.

Consulte *Usando o Adobe Primetime DRM SDK para Proteção de Conteúdo* para obter dicas sobre como otimizar o desempenho.