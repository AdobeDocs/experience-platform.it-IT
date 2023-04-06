---
keywords: estensione inoltro eventi;mixpanel;estensione inoltro eventi mixpanel
title: Estensione di inoltro eventi API di tracciamento eventi di Mixpanel
description: Questa estensione di inoltro eventi Adobe Experience Platform invia gli eventi Adobe Experience Edge Network a Mixpanel.
source-git-commit: 8538e3a2899c3e2451519996cabeffc4b42d706c
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 1%

---

# [!DNL Mixpanel Track Events] Estensione di inoltro eventi API

[[!DNL Mixpanel]](https://www.mixpanel.com) è uno strumento di analisi del prodotto che consente di acquisire dati su come gli utenti interagiscono con un prodotto digitale. Puoi analizzare i dati dei prodotti con report semplici e interattivi che ti consentono di eseguire query e visualizzare i dati con pochi clic. [!DNL Mixpanel] progettato per rendere i team più efficienti, consentendo a tutti di analizzare i dati degli utenti in tempo reale per identificare le tendenze, comprendere il comportamento degli utenti e prendere decisioni sul prodotto.

[!DNL Mixpanel] utilizza un modello basato su eventi e incentrato sull’utente che collega ogni interazione a un singolo utente. La [!DNL Mixpanel] il modello dati è basato sui concetti di utenti, eventi e proprietà.

>[!NOTE]
>
>Fai riferimento a [!DNL Mixpanel] documentazione [gestione delle identità](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management) per comprendere come [!DNL Mixpanel] unisce gli eventi per creare cluster di identità. Si consiglia inoltre di rivedere il documento in [ID distinti](https://help.mixpanel.com/hc/en-us/articles/115004509426-Distinct-ID-Creation-JavaScript-iOS-Android-) per capire come vengono utilizzati per identificare gli utenti nei dati dell’evento.

## Casi d’uso

Usa questa estensione se desideri utilizzare i dati di Edge Network in [!DNL Mixpanel] per sfruttare le funzionalità di analisi dei prodotti.

Ad esempio, considera un’organizzazione retail con una presenza multicanale (sito web e dispositivi mobili). L’organizzazione acquisisce l’input transazionale o conversazionale come dati evento dalle proprie piattaforme e lo carica in [!DNL Mixpanel] utilizzo dell&#39;estensione di inoltro eventi.

I team di analisi possono quindi sfruttare [!DNL Mixpanel's] capacità di elaborare i set di dati e ricavare informazioni aziendali, che possono essere utilizzate per generare grafici, dashboard o altre visualizzazioni per informare le parti interessate del business.

Per ulteriori informazioni sui casi di utilizzo specifici per [!DNL Mixpanel], consulta la seguente documentazione:

* [Da nuovo a [!DNL Mixpanel]](https://help.mixpanel.com/hc/en-us/sections/360008533532-New-to-Mixpanel)
* [Che cosa è [!DNL Mixpanel]?](https://developer.mixpanel.com/docs)
* [12 must-try [!DNL Mixpanel] caratteristiche](https://mixpanel.com/blog/12-things-you-probably-didnt-know-you-could-do-with-mixpanel/)

## [!DNL Mixpanel] prerequisiti {#prerequisites-mixpanel}

È necessario disporre di un [!DNL Mixpanel] per utilizzare questa estensione. Vai a [[!DNL Mixpanel] pagina di registrazione](https://mixpanel.com/register/) per registrare e creare un account, se non ne hai già uno.

Assicurati che [[!DNL Identity Merge]](https://help.mixpanel.com/hc/en-us/articles/9648680824852-ID-Merge-Implementation-Best-Practices) è abilitata per il progetto. Passa a **[!DNL Settings]** > **[!DNL Project Setting]** > **[!DNL Identity Merge]** e attivare/disattivare l&#39;impostazione.

### Informazioni sui cluster di identità in [!DNL Mixpanel]

In [!DNL Mixpanel], un cluster di identità contiene una raccolta di `distinct_id` valori collegati a un singolo utente. [!DNL Mixpanel] gestisce il cluster di identità per ogni utente, risolvendo un singolo canale `distinct_id` da ogni cluster da utilizzare nel reporting. Puoi anche includere un identificatore personalizzato (denominato locale) `distinct_id`) per gli eventi anonimi che si verificano prima di un evento di identificazione utente.

[!DNL Mixpanel] risolve i cluster di identità tramite due metodi:

* **Identifica** : [!DNL Mixpanel] connette l&#39;identificatore scelto a un anonimo `distinct_id`. Se il tuo sito web ha [!DNL Mixpanel] SDK abilitato, Platform utilizzerà l’ `distinct_id` assegnato all&#39;utente attualmente connesso.
* **Alias**: [!DNL Mixpanel] combina due non anonimi `distinct id`è insieme se vengono soddisfatti criteri di unione aggiuntivi.

>[!NOTE]
>
>Fai riferimento a [!DNL Mixpanel] documento [gestione delle identità](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management#user-identification) per ulteriori dettagli su questi metodi.
>
>Conferma di aver abilitato la [[!DNL Mixpanel] feature di unione delle identità](#prerequisites-mixpanel) per garantire una corretta risoluzione dei cluster di identità.

### Raccogli i dettagli di configurazione richiesti {#configuration-details}

Per collegare l&#39;Experience Platform a [!DNL Mixpanel] è necessario disporre dei seguenti input:

| Tipo di chiave | Descrizione | Esempio |
| --- | --- | --- |
| Token di progetto | Token di progetto associato al [!DNL Mixpanel] conto. Fai riferimento a [!DNL Mixpanel] documentazione [ricerca del token di progetto](https://help.mixpanel.com/hc/en-us/articles/115004502806-Find-Project-Token-) a titolo indicativo. | `25470xxxxxxxxxxxxxxxxxxx1289` |

## Installa e configura il [!DNL Mixpanel] estensione {#install}

Per installare l&#39;estensione, [creare una proprietà di inoltro eventi](../../../ui/event-forwarding/overview.md#properties) oppure scegli una proprietà esistente da modificare.

Seleziona **[!UICONTROL Estensioni]** nella navigazione a sinistra. In **[!UICONTROL Catalogo]** scheda , seleziona **[!UICONTROL Installa]** sulla scheda per [!DNL Mixpanel] estensione.

![Installazione di [!DNL Mixpanel] estensione.](../../../images/extensions/server/mixpanel/install-extension.png)

## Crea un [!DNL Send Event] regola

Inizia a creare una nuova regola nella proprietà di inoltro eventi. Sotto **[!UICONTROL Azioni]**, aggiungi una nuova azione e imposta l&#39;estensione su **[!UICONTROL Pannello misto]**. Quindi, imposta il tipo di azione su **[!UICONTROL Evento Track]** per inviare eventi di Adobe Experience Edge Network a [!DNL Mixpanel].

| Ingresso | Descrizione | Obbligatorio |
| --- | --- | --- |
| [!UICONTROL Token di progetto] | Questo campo deve essere mappato al token di progetto associato al [!DNL Mixpanel] conto. | Sì |
| [!UICONTROL Tipo evento] | Nome dell&#39;evento. | Sì |
| [!UICONTROL Ora evento] | Ora dell’evento. |  |
| [!UICONTROL ID distinto del pannello multiplo] | Identificatore univoco dell&#39;utente che ha eseguito l&#39;evento. |  |
| [!UICONTROL Inserisci ID] | Identificatore univoco per l&#39;evento, utilizzato per la deduplicazione. |  |
| [!UICONTROL Proprietà evento] | Un oggetto JSON contenente proprietà personalizzate dell’evento. Scegli se fornire JSON non elaborato o utilizzare un set semplificato di input chiave-valore. |  |

>[!NOTE]
>
>Per ulteriori informazioni sui campi standard di un [!DNL Mixpanel] evento , fai riferimento al [documentazione ufficiale](https://developer.mixpanel.com/reference/import-events#event).

![Aggiungi una configurazione di azione della regola di inoltro eventi.](../../../images/extensions/server/mixpanel/track-event-action.png)

Una volta che [!UICONTROL Evento Track] viene aggiunta alla regola, puoi configurare le condizioni della regola in modo che si attivi solo per determinati eventi, oppure puoi lasciare vuota la sezione condizioni per attivare la regola per tutti gli eventi.

>[!IMPORTANT]
>
>Se il sito web utilizza la [!DNL Mixpanel] SDK, puoi continuare al passaggio successivo di [convalida dei dati in [!DNL Mixpanel]](#validate). Se non utilizzi il [!DNL Mixpanel] SDK, devi [creare una regola di tracciamento identità separata](#create-an-identity-tracking-rule) garantire che gli eventi appropriati e `distinct_id` vengono inviati a [!DNL Mixpanel] quando si verifica un evento di identificazione utente.

## Convalida dei dati all’interno di [!DNL Mixpanel] {#validate}

Se l’implementazione ha esito positivo e gli eventi vengono raccolti, visualizzerai gli eventi all’interno del [[!DNL Mixpanel] console](https://help.mixpanel.com/hc/en-us/articles/4402837164948).

Controlla se [!DNL Mixpanel] ha unito gli eventi di accesso al post con i valori e-mail e gli eventi creati durante l’utilizzo di **[!UICONTROL Invia evento]**. Se implementato correttamente, [!DNL Mixpanel] li associerà a un singolo [profilo utente](https://help.mixpanel.com/hc/en-us/articles/115004501966).

## Passaggi successivi

Questa guida spiega come inviare eventi di conversione a [!DNL Mixpanel] utilizzo dell&#39;inoltro eventi. Questa estensione di inoltro eventi sfrutta la [!DNL Mixpanel] SDK e API JavaScript. Per ulteriori informazioni su queste tecnologie sottostanti, consulta la documentazione ufficiale:

* [[!DNL Mixpanel] SDK](https://developer.mixpanel.com/docs/nodejs)
* [[!DNL Mixpanel] API JavaScript](https://developer.mixpanel.com/docs/javascript-full-api-reference#mixpanelidentify)

Per ulteriori informazioni sulle funzionalità di inoltro eventi in Experience Platform, consulta la [panoramica sull&#39;inoltro eventi](../../../ui/event-forwarding/overview.md).
