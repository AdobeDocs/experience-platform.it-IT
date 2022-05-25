---
title: Gruppo di campi schema di estensione completa Adobe Analytics ExperienceEvent
description: Questo documento fornisce una panoramica del gruppo di campi dello schema di estensione completa Adobe Analytics ExperienceEvent.
exl-id: b5e17f4a-a582-4059-bbcb-435d46932775
source-git-commit: fb0d8aedbb88aad8ed65592e0b706bd17840406b
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 7%

---

# [!UICONTROL Estensione completa Adobe Analytics ExperienceEvent] gruppo di campi schema

[!UICONTROL Estensione completa Adobe Analytics ExperienceEvent] è un gruppo di campi di schema standard per [[!DNL XDM ExperienceEvent] Classe](../../classes/experienceevent.md), che acquisisce le metriche comuni raccolte da Adobe Analytics.

Questo documento descrive la struttura e il caso d&#39;uso del gruppo di campi dell&#39;estensione Analytics.

>[!NOTE]
>
>A causa delle dimensioni e del numero di elementi ripetuti in questo gruppo di campi, molti dei campi mostrati in questa guida sono stati compressi per risparmiare spazio. Per esplorare l&#39;intera struttura del gruppo di campi, è possibile [cerca nell’interfaccia utente di Platform ](../../ui/explore.md) o visualizza lo schema completo nel [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json).

## Struttura del gruppo di campi

Il gruppo di campi fornisce un singolo `_experience` oggetto di uno schema che contiene un singolo `analytics` oggetto.

![Campi di primo livello per il gruppo di campi di Analytics](../../images/field-groups/analytics-full-extension/full-schema.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `customDimensions` | Oggetto | Acquisisce dimensioni personalizzate tracciate da Analytics. Consulta la sezione [sottosezione](#custom-dimensions) per ulteriori informazioni sul contenuto di questo oggetto. |
| `endUser` | Oggetto | Acquisisce i dettagli dell’interazione web per l’utente finale che ha attivato l’evento. Consulta la sezione [sottosezione](#end-user) per ulteriori informazioni sul contenuto di questo oggetto. |
| `environment` | Oggetto | Acquisisce informazioni sul browser e sul sistema operativo che hanno attivato l’evento. Consulta la sezione [sottosezione](#environment) per ulteriori informazioni sul contenuto di questo oggetto. |
| `event1to100`<br><br>`event101to200`<br><br>`event201to300`<br><br>`event301to400`<br><br>`event401to500`<br><br>`event501to100`<br><br>`event601to700`<br><br>`event701to800`<br><br>`event801to900`<br><br>`event901to1000` | Oggetto | Il gruppo di campi fornisce campi oggetto per acquisire fino a 1000 eventi personalizzati. Consulta la sezione [sottosezione](#events) per ulteriori informazioni su questi campi. |
| `session` | Oggetto | Acquisisce informazioni sulla sessione che ha attivato l’evento. Consulta la sezione [sottosezione](#session) per ulteriori informazioni sul contenuto di questo oggetto. |

{style=&quot;table-layout:auto&quot;}

## `customDimensions` {#custom-dimensions}

`customDimensions` acquisisce dati personalizzati [dimensioni](https://experienceleague.adobe.com/docs/analytics/components/dimensions/overview.html?lang=it) che vengono tracciati da Analytics.

![campo customDimensions](../../images/field-groups/analytics-full-extension/customDimensions.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `eVars` | Oggetto | Un oggetto che acquisisce fino a 250 variabili di conversione ([eVar](https://experienceleague.adobe.com/docs/analytics/components/dimensions/evar.html?lang=it)). Le proprietà dell&#39;oggetto sono codificate `eVar1` a `eVar250` e accetta solo stringhe per il tipo di dati. |
| `hierarchies` | Oggetto | Un oggetto che acquisisce fino a cinque variabili gerarchiche personalizzate ([hier](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/hier.html?lang=it)). Le proprietà dell&#39;oggetto sono codificate `hier1` a `hier5`, che sono essi stessi oggetti con le seguenti sottoproprietà:<ul><li>`delimiter`: Il delimitatore originale utilizzato per generare l’elenco fornito in `values`.</li><li>`values`: Un elenco delimitato di nomi di livello gerarchico, rappresentati da una stringa.</li></ul> |
| `listProps` | Oggetto | Un oggetto che cattura fino a 75 [list props](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html#list-props). Le proprietà dell&#39;oggetto sono codificate `prop1` a `prop75`, che sono essi stessi oggetti con le seguenti sottoproprietà:<ul><li>`delimiter`: Il delimitatore originale utilizzato per generare l’elenco fornito in `values`.</li><li>`values`: Un elenco delimitato di valori per il prop, rappresentato come stringa.</li></ul> |
| `lists` | Oggetto | Un oggetto che acquisisce fino a tre [elenchi](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/list.html). Le proprietà dell&#39;oggetto sono codificate `list1` a `list3`. Ciascuna di queste proprietà contiene un singolo `list` array di [[!UICONTROL Coppia di valori chiave]](../../data-types/key-value-pair.md) tipi di dati. |
| `props` | Oggetto | Un oggetto che cattura fino a 75 [proprietà](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html). Le proprietà dell&#39;oggetto sono codificate `prop1` a `prop75` e accetta solo stringhe per il tipo di dati. |
| `postalCode` | Stringa | CAP fornito dal cliente. |
| `stateProvince` | Stringa | Posizione dello stato o della provincia fornita dal client. |

{style=&quot;table-layout:auto&quot;}

## `endUser` {#end-user}

`endUser` acquisisce i dettagli dell’interazione web per l’utente finale che ha attivato l’evento.

![campo endUser](../../images/field-groups/analytics-full-extension/endUser.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `firstWeb` | [[!UICONTROL Informazioni web]](../../data-types/web-information.md) | Le informazioni relative alla pagina web, al collegamento e al referente del primo evento esperienza per l’utente finale. |
| `firstTimestamp` | Intero | Una marca temporale Unix per il primo ExperienceEvent per questo utente finale. |

## `environment` {#environment}

`environment` acquisisce informazioni sul browser e sul sistema operativo che hanno attivato l’evento.

![campo ambiente](../../images/field-groups/analytics-full-extension/environment.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `browserIDStr` | Stringa | Identificatore Adobe Analytics per il browser utilizzato (altrimenti noto come [dimensione del tipo di browser](https://experienceleague.adobe.com/docs/analytics/components/dimensions/browser-type.html)). |
| `operatingSystemIDStr` | Stringa | Identificatore Adobe Analytics per il sistema operativo utilizzato (altrimenti noto come [dimensione del tipo di sistema operativo](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-system-types.html)). |

## Campi evento personalizzati {#events}

Il gruppo di campi dell’estensione Analytics fornisce dieci campi oggetto che acquisiscono fino a 100 [metriche evento personalizzate](https://experienceleague.adobe.com/docs/analytics/components/metrics/custom-events.html) ciascuno, per un totale di 1000 per il gruppo di campi.

Ogni oggetto evento di livello principale contiene i singoli oggetti evento per il rispettivo intervallo. Ad esempio: `event101to200` contiene gli eventi da `event101` a `event200`.

Ogni oggetto even utilizza [[!UICONTROL Misura]](../../data-types/measure.md) tipo di dati, che fornisce un identificatore univoco e un valore quantificabile.

![Campo evento personalizzato](../../images/field-groups/analytics-full-extension/event-vars.png)

## `session` {#session}

`session` acquisisce informazioni sulla sessione che ha attivato l’evento.

![campo di sessione](../../images/field-groups/analytics-full-extension/session.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `search` | [[!UICONTROL Ricerca]](../../data-types/search.md) | Acquisisce informazioni relative alla ricerca web o mobile per la voce di sessione. |
| `web` | [[!UICONTROL Informazioni web]](../../data-types/web-information.md) | Acquisisce informazioni sui clic sul collegamento, i dettagli della pagina web, le informazioni sul referente e i dettagli del browser per la voce di sessione. |
| `depth` | Intero | Profondità della sessione corrente (ad esempio il numero di pagina) per l’utente finale. |
| `num` | Intero | Numero di sessione corrente per l&#39;utente finale. |
| `timestamp` | Intero | Un timestamp Unix per la voce di sessione. |

## Passaggi successivi

Questo documento ha trattato la struttura e il caso d&#39;uso del gruppo di campi dell&#39;estensione Analytics. Per ulteriori dettagli sul gruppo di campi stesso, consulta [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json).

Se utilizzi questo gruppo di campi per raccogliere dati di Analytics tramite l’SDK per web di Adobe Experience Platform, consulta la guida in [configurazione di un datastream](../../../edge/datastreams/overview.md) per scoprire come mappare i dati su XDM sul lato server.
