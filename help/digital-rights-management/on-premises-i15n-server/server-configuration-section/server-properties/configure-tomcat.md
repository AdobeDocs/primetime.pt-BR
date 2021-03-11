---
title: Configurar Tomcat
description: Configurar Tomcat
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---


# Configurar Tomcat{#configure-tomcat}

No servidor de individualização, modifique o arquivo [!DNL conf/server.xml] do Tomcat para incluir informações adicionais no log de acesso. Você pode usar essas informações para fins de relatório.

1. Localize a configuração para `AccessLogValve` em [!DNL server.xml] e modifique o padrão como mostrado aqui:

   ```
   <Valve className="org.apache.catalina.valves.AccessLogValve" 
   directory="logs" prefix="localhost_access_log." suffix=".txt" 
   pattern="%h %{x-forwarded-for}i %l %u %t &quot;%r&quot; %s %b 
   %{request-id}r" resolveHosts="false"/>
   ```

   `%{x-forwarded-for}i` registrará o valor do  `x-forwarded-for` cabeçalho. Se você usar um proxy reverso do Apache para encaminhar solicitações ao servidor Tomcat, esse cabeçalho conterá o endereço IP do cliente original, enquanto `%h` registrará o endereço IP do servidor Apache. `%{request-id}r` O registrará o identificador de solicitação, que corresponde à ID de solicitação contida no log de aplicativo de individualização.

1. Edite [!DNL conf/server.xml] e defina a propriedade `unpackwars` como false.

   Para os servidores de Individualização e Geração de Chave, convém editar [!DNL conf/server.xml] e definir a propriedade `unpackwars` como `false`. Caso contrário, ao atualizar as WARs, talvez seja necessário limpar as pastas WAR descompactadas também.

>[!NOTE]
>
>Os futuros clientes de DRM exigirão que você ative e configure o filtro CORS (Cross-Origin Resource Sharing) que está disponível para o Tomcat. Atualmente, nenhum cliente DRM tem esse requisito.

