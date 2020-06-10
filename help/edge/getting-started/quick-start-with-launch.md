---
title: Avvio rapido con Launch
seo-title: Avvio rapido dell’SDK Web per Adobe Experience Platform
description: Guida di avvio rapido per l’utilizzo dell’estensione SDK Web di Experience Platform per la raccolta dei dati
seo-description: Guida di avvio rapido per l’utilizzo dell’estensione SDK Web di Experience Platform per la raccolta dei dati
translation-type: tm+mt
source-git-commit: dc5ee796ca390d06fc8e08bd6c30e88a0d96dd53
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 3%

---


# Benvenuti

Questa guida illustra i diversi passaggi per configurare l’SDK Web per Adobe Experience Platform in Launch. Per poter utilizzare questa funzione, è necessario disporre di autorizzazioni ed essere nell&#39;elenco di autorizzazioni. Se vuoi entrare nella lista d&#39;attesa, ti invitiamo a contattarti il CSM.

- Accertati che sia attivato un dominio di [prime parti (CNAME)](https://docs.adobe.com/content/help/it-IT/core-services/interface/ec-cookies/cookies-first-party.html) . Se hai già un CNAME per Analytics, devi usarlo. La verifica in fase di sviluppo funzionerà senza un CNAME, ma ne avrai bisogno prima di andare in produzione
- Accedi ad Adobe Experience Platform Data Platform. Se non hai acquistato la piattaforma, ti forniremo Experience Platform Data Services Foundation da utilizzare in modo limitato con l’SDK senza costi aggiuntivi.
- Usa la versione più recente del servizio ID visitatore

## Creare un ID di configurazione

Potete creare un ID di configurazione utilizzando lo strumento [di configurazione](../fundamentals/edge-configuration.md) edge all’avvio. In questo modo sarà possibile abilitare Edge Network per inviare dati alle varie soluzioni. Per informazioni su come trovare ciascuna opzione, consultate la pagina [Edge Configuration Tool](../fundamentals/edge-configuration.md) (Strumentodi configurazione Edge).

>[!NOTE]
>
>L&#39;organizzazione deve essere inclusa nell&#39;elenco Consenti per la funzione. Contattate il CSM per inserire l&#39;elenco dei permessi.

## Preparare uno schema

Experience Platform Edge Network accetta i dati come XDM. XDM è un formato di dati che consente di definire gli schemi. Lo schema definisce il modo in cui Edge Network prevede la formattazione dei dati. Per inviare i dati è necessario definire lo schema.

- [Creare uno schema](../../xdm/tutorials/create-schema-ui.md)
- Aggiungere il mixin SDK Web di Adobe Experience Platform allo schema creato

## Installa l’SDK in Launch

Accedete a Launch e installate l&#39; `AEP Web SDK` estensione. Durante l’installazione dell’SDK, ti verrà richiesto di configurare l’estensione. Immettete l’ID di configurazione richiesto in precedenza. L’estensione completa automaticamente l’ID organizzazione.

Per ulteriori dettagli sulle diverse opzioni di configurazione, consulta [Configurazione dell’SDK](../fundamentals/configuring-the-sdk.md).

## Creazione di una base di dati sullo schema

All&#39;avvio, crea un elemento dati che fa riferimento allo schema modificando l&#39;estensione in AEP Web SDK e impostando il tipo su XDM Object. Questo caricherà lo schema e ti consentirà di mappare gli elementi dati in parti diverse dello schema.

![Elemento data in avvio](../../assets/edge_data_element.png)

## Invio di un evento

Dopo l&#39;installazione dell&#39;estensione, iniziate a inviare gli eventi aggiungendo un&#39;azione &quot;sendEvent&quot; dall&#39;estensione SDK Web AEP a una regola. Accertatevi di aggiungere all&#39;evento l&#39;elemento dati appena creato come dati XDM. È consigliabile inviare almeno un evento ogni volta che una pagina viene caricata.

Per ulteriori dettagli su come tenere traccia degli eventi, vedere [Tracciamento degli eventi](../fundamentals/tracking-events.md).

## Passaggi successivi

Una volta che i dati scorrono, è possibile effettuare le seguenti operazioni.

- [Creare lo schema](https://docs.adobe.com/content/help/en/experience-platform/xdm/schema/composition.html)
- [Informazioni sul debug](../fundamentals/debugging.md)
- Scoprite come [personalizzare l&#39;esperienza](../fundamentals/rendering-personalization-content.md)
- Scopri come inviare dati a più soluzioni
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
