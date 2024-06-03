---
title: Gruppo di campi dello schema di estensione completa Adobe Analytics ExperienceEvent
description: Scopri il gruppo di campi schema Estensione completa Adobe Analytics ExperienceEvent.
exl-id: b5e17f4a-a582-4059-bbcb-435d46932775
source-git-commit: 5eb15a7dfff7e6d8ba815ae4f89142ba50166620
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 5%

---

# [!UICONTROL Estensione completa Adobe Analytics ExperienceEvent] gruppo di campi schema

[!UICONTROL Estensione completa Adobe Analytics ExperienceEvent] è un gruppo di campi di schema standard per [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md), che acquisisce le metriche comuni raccolte da Adobe Analytics.

Questo documento descrive la struttura e il caso d’uso del gruppo di campi dell’estensione Analytics.

>[!NOTE]
>
>A causa delle dimensioni e del numero di elementi ripetuti in questo gruppo di campi, molti dei campi mostrati in questa guida sono stati compressi per risparmiare spazio. Per esplorare l’intera struttura di questo gruppo di campi, puoi [Cercarlo nell’interfaccia utente di Platform](../../ui/explore.md) o visualizzare lo schema completo nel [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json).

## Struttura del gruppo di campi

Il gruppo di campi fornisce un singolo `_experience` oggetto a uno schema, che contiene un singolo `analytics` oggetto.

![Campi di primo livello per il gruppo di campi di Analytics](../../images/field-groups/analytics-full-extension/full-schema.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `customDimensions` | Oggetto | Acquisisce dimensioni personalizzate tracciate da Analytics. Consulta la [sottosezione successiva](#custom-dimensions) per ulteriori informazioni sul contenuto di questo oggetto. |
| `endUser` | Oggetto | Acquisisce i dettagli dell’interazione web per l’utente finale che ha attivato l’evento. Consulta la [sottosezione successiva](#end-user) per ulteriori informazioni sul contenuto di questo oggetto. |
| `environment` | Oggetto | Acquisisce informazioni sul browser e sul sistema operativo che hanno attivato l’evento. Consulta la [sottosezione successiva](#environment) per ulteriori informazioni sul contenuto di questo oggetto. |
| `event1to100`<br><br>`event101to200`<br><br>`event201to300`<br><br>`event301to400`<br><br>`event401to500`<br><br>`event501to100`<br><br>`event601to700`<br><br>`event701to800`<br><br>`event801to900`<br><br>`event901to1000` | Oggetto | Il gruppo di campi fornisce campi oggetto per acquisire fino a 1000 eventi personalizzati. Consulta la [sottosezione successiva](#events) per ulteriori informazioni su questi campi. |
| `session` | Oggetto | Acquisisce informazioni sulla sessione che ha attivato l’evento. Consulta la [sottosezione successiva](#session) per ulteriori informazioni sul contenuto di questo oggetto. |

{style="table-layout:auto"}

## `customDimensions` {#custom-dimensions}

`customDimensions` acquisisce dati personalizzati [dimensioni](https://experienceleague.adobe.com/docs/analytics/components/dimensions/overview.html) tracciati da Analytics.

![campo customDimensions](../../images/field-groups/analytics-full-extension/customDimensions.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `eVars` | Oggetto | Un oggetto che acquisisce fino a 250 variabili di conversione ([eVar](https://experienceleague.adobe.com/docs/analytics/components/dimensions/evar.html?lang=it)). Le proprietà di questo oggetto sono codificate `eVar1` a `eVar250` e accetta solo stringhe per il relativo tipo di dati. |
| `hierarchies` | Oggetto | Oggetto che acquisisce fino a cinque variabili gerarchiche personalizzate ([hiers](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/hier.html?lang=it)). Le proprietà di questo oggetto sono codificate `hier1` a `hier5`, che sono a loro volta oggetti con le seguenti sottoproprietà:<ul><li>`delimiter`: delimitatore originale utilizzato per generare l’elenco fornito in `values`.</li><li>`values`: elenco delimitato di nomi di livello gerarchico, rappresentati da una stringa.</li></ul> |
| `listProps` | Oggetto | Un oggetto che cattura fino a 75 [prop elenco](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html#list-props). Le proprietà di questo oggetto sono codificate `prop1` a `prop75`, che sono a loro volta oggetti con le seguenti sottoproprietà:<ul><li>`delimiter`: delimitatore originale utilizzato per generare l’elenco fornito in `values`.</li><li>`values`: elenco delimitato di valori per il prop, rappresentato da una stringa.</li></ul> |
| `lists` | Oggetto | Un oggetto che acquisisce fino a tre [elenchi](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/list.html). Le proprietà di questo oggetto sono codificate `list1` a `list3`. Ognuna di queste proprietà contiene un singolo `list` array di [[!UICONTROL Coppia chiave-valore]](../../data-types/key-value-pair.md) tipi di dati. |
| `props` | Oggetto | Un oggetto che cattura fino a 75 [prop](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html?lang=it). Le proprietà di questo oggetto sono codificate `prop1` a `prop75` e accetta solo stringhe per il relativo tipo di dati. |
| `postalCode` | Stringa | Codice postale o CAP fornito dal cliente. |
| `stateProvince` | Stringa | Stato o località della provincia fornito dal client. |

{style="table-layout:auto"}

## `endUser` {#end-user}

`endUser` acquisisce i dettagli dell’interazione web per l’utente finale che ha attivato l’evento.

![campo endUser](../../images/field-groups/analytics-full-extension/endUser.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `firstWeb` | [[!UICONTROL Informazioni Web]](../../data-types/web-information.md) | Le informazioni relative alla pagina web, al collegamento e al referente del primo evento esperienza per questo utente finale. |
| `firstTimestamp` | Intero | Una marca temporale Unix per il primo ExperienceEvent per questo utente finale. |

## `environment` {#environment}

`environment` acquisisce informazioni sul browser e sul sistema operativo che hanno attivato l’evento.

![campo ambiente](../../images/field-groups/analytics-full-extension/environment.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `browserIDStr` | Stringa | L’identificatore Adobe Analytics del browser utilizzato (altrimenti noto come [dimensione tipo di browser](https://experienceleague.adobe.com/docs/analytics/components/dimensions/browser-type.html)). |
| `operatingSystemIDStr` | Stringa | L’identificatore Adobe Analytics del sistema operativo utilizzato (altrimenti noto come [dimensione tipo di sistema operativo](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-system-types.html)). |

## Campi evento personalizzati {#events}

Il gruppo di campi dell’estensione Analytics fornisce dieci campi oggetto che acquisiscono fino a 100 [metriche evento personalizzate](https://experienceleague.adobe.com/docs/analytics/components/metrics/custom-events.html) ciascuno, per un totale di 1000 per il gruppo di campi.

Ogni oggetto evento di livello principale contiene i singoli oggetti evento per il rispettivo intervallo. Ad esempio: `event101to200` contiene gli eventi chiave da `event101` a `event200`.

Ogni oggetto pari utilizza [[!UICONTROL Misura]](../../data-types/measure.md) tipo di dati, che fornisce un identificatore univoco e un valore quantificabile.

![Campo evento personalizzato](../../images/field-groups/analytics-full-extension/event-vars.png)

## `session` {#session}

`session` acquisisce informazioni sulla sessione che ha attivato l’evento.

![campo sessione](../../images/field-groups/analytics-full-extension/session.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `search` | [[!UICONTROL Ricerca]](../../data-types/search.md) | Acquisisce informazioni relative alla ricerca web o mobile della voce di sessione. |
| `web` | [[!UICONTROL Informazioni Web]](../../data-types/web-information.md) | Acquisisce informazioni sui clic dei collegamenti, sui dettagli della pagina web, sulle informazioni del referente e sui dettagli del browser per la voce della sessione. |
| `depth` | Intero | Profondità di sessione corrente (ad esempio il numero di pagina) per l’utente finale. |
| `num` | Intero | Numero di sessione corrente per l&#39;utente finale. |
| `timestamp` | Intero | Un timestamp Unix per la voce della sessione. |

## Passaggi successivi

Questo documento descrive la struttura e il caso d’uso per il gruppo di campi dell’estensione Analytics. Per ulteriori dettagli sul gruppo di campi stesso, consulta [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json).

Se utilizzi questo gruppo di campi per raccogliere dati di Analytics tramite Adobe Experience Platform Web SDK, consulta la guida su [configurazione di uno stream di dati](../../../datastreams/overview.md) per scoprire come mappare i dati su XDM sul lato server.
