---
title: Avvio rapido con Launch
seo-title: ' Adobe Experience Platform Avvio rapido dell''SDK Web con Launch'
description: Guida di avvio rapido per l'utilizzo dell'estensione Experience Platform Web SDK  per la raccolta dei dati
seo-description: Guida di avvio rapido per l'utilizzo dell'estensione Experience Platform Web SDK  per la raccolta dei dati
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 3%

---


# Benvenuti

Questa guida illustra i diversi passaggi per configurare il Adobe Experience Platform  [!DNL Web SDK] in Adobe Launch. Per utilizzare questa funzione, è necessario disporre delle autorizzazioni e stare sul elenco consentiti . Se vuoi entrare nella lista d&#39;attesa, contatta il tuo CSM. Inoltre, per utilizzare questa funzione, è necessario:

- Accertati che sia attivato un dominio di [prime parti (CNAME)](https://docs.adobe.com/content/help/it-IT/core-services/interface/ec-cookies/cookies-first-party.html) . Se hai già un CNAME per Adobe  Analytics, devi usarlo. La verifica in fase di sviluppo funzionerà senza un CNAME, ma ne avrai bisogno prima di andare in produzione
- Usa la versione più recente del servizio ID visitatore

## Creare un ID di configurazione

Puoi creare un ID di configurazione utilizzando lo strumento [di configurazione](../fundamentals/edge-configuration.md) edge in Adobe Launch. In questo modo sarà possibile abilitare Edge Network per inviare dati alle varie soluzioni. Consultate la pagina [Edge Configuration Tool](../fundamentals/edge-configuration.md) (Strumentodi configurazione Edge) per informazioni dettagliate su come trovare ogni opzione.

>[!NOTE]
>
>L&#39;organizzazione deve trovarsi nel elenco consentiti  per la funzione. Contatta il tuo CSM per essere aggiunto al elenco consentiti .

## Preparare uno schema

I dati [!DNL Experience Platform Edge Network] vengono utilizzati come XDM. XDM è un formato di dati che consente di definire gli schemi. Lo schema definisce il modo in cui [!DNL Edge Network] si prevede la formattazione dei dati. Per inviare i dati è necessario definire lo schema. Assicuratevi di completare quanto segue:

1. [Creare uno schema](../../xdm/tutorials/create-schema-ui.md)
2. Aggiungete il [!DNL Web SDK ExperienceEvent] Mixin AEP allo schema creato.
3. Creare un dataset dallo schema creato.

Il seguente video è pensato per aiutarti a creare uno schema, un set di dati e un connettore di origine per lo streaming dei [!DNL Web SDK] dati.

>[!VIDEO](https://video.tv.adobe.com/v/35395?quality=12&learn=on)

## Installare l’SDK in Adobe Launch

Accedete ad Adobe Launch e installate l&#39; `AEP Web SDK` estensione. Durante l’installazione dell’SDK, ti verrà richiesto di configurare l’estensione. Immettete l’ID di configurazione richiesto in precedenza. L’estensione completa automaticamente l’ID organizzazione.

Per ulteriori dettagli sulle diverse opzioni di configurazione, consulta [Configurazione dell’SDK](../fundamentals/configuring-the-sdk.md).

## Creazione di una base di dati sullo schema

In Adobe Launch, creare un elemento dati che fa riferimento allo schema modificando l&#39;estensione in AEP [!DNL Web SDK] e impostando il tipo su Oggetto XDM. Questo caricherà lo schema e ti consentirà di mappare gli elementi dati in parti diverse dello schema.

![Elemento data in avvio](../../assets/edge_data_element.png)

## Invio di un evento

Una volta installata l’estensione, avviate l’invio di eventi aggiungendo un’azione &quot;sendEvent&quot; dall’ [!DNL Web SDK] estensione AEP a una regola. Accertatevi di aggiungere all&#39;evento l&#39;elemento dati appena creato come dati XDM. È consigliabile inviare almeno un evento ogni volta che una pagina viene caricata.

Per ulteriori dettagli su come tenere traccia degli eventi, vedere [Tracciamento degli eventi](../fundamentals/tracking-events.md).

## Passaggi successivi

Una volta che i dati scorrono, potete effettuare le seguenti operazioni:

- [Creare lo schema](https://docs.adobe.com/content/help/en/experience-platform/xdm/schema/composition.html)
- [Informazioni sul debug](../fundamentals/debugging.md)
- Scoprite come [personalizzare l&#39;esperienza](../fundamentals/rendering-personalization-content.md)
- Scopri come inviare dati a più soluzioni
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
