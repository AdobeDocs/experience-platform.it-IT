---
title: Avvio rapido con Launch
seo-title: ' Adobe Experience Platform Avvio rapido dell''SDK Web con Launch'
description: Guida di avvio rapido per l'utilizzo dell'estensione SDK Web  Experience Platform per la raccolta dei dati
seo-description: Guida di avvio rapido per l'utilizzo dell'estensione SDK Web  Experience Platform per la raccolta dei dati
translation-type: tm+mt
source-git-commit: d958e323df2535c168edd3a35b878fcc4bb73370
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 3%

---


# Benvenuti

Questa guida illustra i diversi modi in cui impostare l’SDK Web  Adobe Experience Platform in Launch. Per utilizzare questa funzione è necessario essere inseriti nella white list. Se vuoi entrare nella lista d&#39;attesa, contatta il tuo CSM.

- Accertati che sia attivato un dominio di [prime parti (CNAME)](https://docs.adobe.com/content/help/it-IT/core-services/interface/ec-cookies/cookies-first-party.html) . Se hai già un CNAME per  Analytics, devi usarlo. Il test in fase di sviluppo funziona senza un CNAME, ma ne hai bisogno prima di andare in produzione.
- Avere diritto a  Adobe Experience Platform. Se non hai acquistato Platform,  Adobe ti fornirà  Data Services Foundation da utilizzare in modo limitato con l&#39;SDK senza costi aggiuntivi.
- Utilizzate la versione più recente del servizio ID visitatori.

## Preparare uno schema

Il  Experience Platform Edge Network accetta i dati come XDM. XDM è un formato di dati che consente di definire gli schemi. Lo schema definisce il modo in cui Edge Network prevede la formattazione dei dati. Per inviare i dati, è necessario definire lo schema.

1. [Creare uno schema](../../xdm/tutorials/create-schema-ui.md)
2. Aggiungete il [!DNL Web SDK ExperienceEvent] Mixin AEP allo schema creato.
3. Creare un dataset dallo schema creato.

Il seguente video è pensato per aiutarti a creare uno schema, un set di dati e un connettore di origine per lo streaming dei [!DNL Web SDK] dati.

Accedete a Launch e installate l&#39; `AEP Web SDK` estensione. Quando installi l’SDK, ti viene richiesto di configurare l’estensione. Immettete l’ID di configurazione richiesto in precedenza. L’estensione completa automaticamente l’ID organizzazione.


Per ulteriori dettagli sulle diverse opzioni di configurazione, consulta [Configurazione dell’SDK](../fundamentals/configuring-the-sdk.md).

## Creare un ID di configurazione

Puoi creare un ID di configurazione utilizzando lo strumento [di configurazione](../fundamentals/edge-configuration.md) edge in Launch. Questo consente di abilitare Edge Network per l&#39;invio di dati alle varie soluzioni. Per informazioni su come trovare ciascuna opzione, consultate la pagina [Edge Configuration Tool](../fundamentals/edge-configuration.md) (Strumentodi configurazione Edge).

>[!NOTE]
>
>Per questa funzione è necessario autorizzare l&#39;organizzazione. Contatta il tuo CSM per essere inserito nella lista per eventuali whitelist.

## Creazione di un elemento dati basato sullo schema

In Launch, creare un elemento dati che fa riferimento allo schema modificando l&#39;estensione in AEP Web SDK e impostando il tipo su `XDM Object`. Questo carica lo schema e consente di mappare gli elementi dati in parti diverse dello schema.

![Elemento data in avvio](../../assets/edge_data_element.png)

## Invio di un evento

Dopo l&#39;installazione dell&#39;estensione, iniziate a inviare gli eventi aggiungendo un&#39; `sendEvent` azione dall&#39;estensione AEP Web SDK a una regola. Aggiungete all&#39;evento l&#39;elemento dati appena creato come dati XDM.  Adobe consiglia di inviare almeno un evento ogni volta che una pagina viene caricata.

Per ulteriori dettagli su come tenere traccia degli eventi, vedere [Tracciamento degli eventi](../fundamentals/tracking-events.md).

## Passaggi successivi

Dopo avere eseguito lo scorrimento dei dati, è possibile effettuare le seguenti operazioni.

- [Creare lo schema](https://docs.adobe.com/content/help/en/experience-platform/xdm/schema/composition.html)
- [Informazioni sul debug](../fundamentals/debugging.md)
- Scoprite come [personalizzare l&#39;esperienza](../fundamentals/rendering-personalization-content.md)
- Scopri come inviare dati a più soluzioni
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
