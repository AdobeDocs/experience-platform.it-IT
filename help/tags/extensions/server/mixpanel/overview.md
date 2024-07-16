---
keywords: estensione inoltro eventi;mixpanel;estensione inoltro eventi mixpanel
title: Estensione inoltro eventi API Mixpanel Track Events
description: Questa estensione di inoltro degli eventi Adobe Experience Platform invia eventi di Edge Network a Mixpanel.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 21e2e0fa-4949-4be4-859f-d449d21d8f41
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 1%

---

# Estensione di inoltro eventi API [!DNL Mixpanel Track Events]

[[!DNL Mixpanel]](https://www.mixpanel.com) è uno strumento di analisi del prodotto che consente di acquisire dati sul modo in cui gli utenti interagiscono con un prodotto digitale. Puoi analizzare i dati dei prodotti con rapporti semplici e interattivi che ti consentono di eseguire query e visualizzare i dati con pochi clic. [!DNL Mixpanel] progettato per rendere più efficienti i team, consentendo a tutti di analizzare i dati degli utenti in tempo reale per identificare le tendenze, comprendere il comportamento degli utenti e prendere decisioni sul prodotto.

[!DNL Mixpanel] utilizza un modello basato su eventi e incentrato sull&#39;utente che collega ogni interazione a un singolo utente. Il modello dati [!DNL Mixpanel] è basato sui concetti di utenti, eventi e proprietà.

>[!NOTE]
>
>Per informazioni su come [!DNL Mixpanel] unisce gli eventi per creare cluster di identità, consulta la documentazione di [!DNL Mixpanel] in [gestione identità](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management). È inoltre consigliabile esaminare il documento in [ID distinti](https://help.mixpanel.com/hc/en-us/articles/115004509426-Distinct-ID-Creation-JavaScript-iOS-Android-) per capire come vengono utilizzati per identificare gli utenti nei dati evento.

## Casi d’uso

Questa estensione deve essere utilizzata se si desidera utilizzare i dati dell&#39;Edge Network in [!DNL Mixpanel] per sfruttare le funzionalità di analisi del prodotto.

Ad esempio, considera un’organizzazione di vendita al dettaglio con una presenza multicanale (sito web e dispositivi mobili). L&#39;organizzazione acquisisce input transazionali o conversazionali come dati evento dalle proprie piattaforme e li carica in [!DNL Mixpanel] utilizzando l&#39;estensione di inoltro degli eventi.

I team di Analytics possono quindi sfruttare le funzionalità di [!DNL Mixpanel's] per elaborare i set di dati e ottenere informazioni aziendali, che possono essere utilizzate per generare grafici, dashboard o altre visualizzazioni per informare le parti interessate.

Per ulteriori informazioni sui casi d&#39;uso specifici di [!DNL Mixpanel], consulta la seguente documentazione:

* [Nuovo a [!DNL Mixpanel]](https://docs.mixpanel.com/docs)
* [Che cosa è [!DNL Mixpanel]?](https://developer.mixpanel.com/docs)
* [12 must-try [!DNL Mixpanel] funzionalità](https://mixpanel.com/blog/12-things-you-probably-didnt-know-you-could-do-with-mixpanel/)

## [!DNL Mixpanel] prerequisiti {#prerequisites-mixpanel}

Per utilizzare questa estensione, è necessario disporre di un account [!DNL Mixpanel] valido. Vai alla [[!DNL Mixpanel] pagina di registrazione](https://mixpanel.com/register/) per registrarti e creare un account, se non ne hai già uno.

Verificare che l&#39;impostazione [[!DNL Identity Merge]](https://help.mixpanel.com/hc/en-us/articles/9648680824852-ID-Merge-Implementation-Best-Practices) sia abilitata per il progetto. Passa a **[!DNL Settings]** > **[!DNL Project Setting]** > **[!DNL Identity Merge]** e attiva/disattiva l&#39;impostazione.

### Informazioni sui cluster di identità in [!DNL Mixpanel]

In [!DNL Mixpanel] un cluster di identità contiene una raccolta di `distinct_id` valori che si connettono a un singolo utente. [!DNL Mixpanel] gestisce il cluster di identità per ogni utente, risolvendo un singolo `distinct_id` canonico da ogni cluster da utilizzare nel reporting. È inoltre possibile includere un proprio identificatore (denominato `distinct_id` locale) per gli eventi anonimi che si verificano prima di un evento di identificazione utente.

[!DNL Mixpanel] risolve i cluster di identità tramite due metodi:

* **Identifica**: [!DNL Mixpanel] collega l&#39;identificatore scelto a un `distinct_id` anonimo. Se l&#39;SDK [!DNL Mixpanel] del tuo sito Web è abilitato, Platform utilizzerà `distinct_id` assegnato all&#39;utente attualmente connesso.
* **Alias**: [!DNL Mixpanel] combina due `distinct id` non anonimi se vengono soddisfatti criteri di unione aggiuntivi.

>[!NOTE]
>
>Per ulteriori informazioni su questi metodi, consultare il documento [!DNL Mixpanel] in [gestione identità](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management#user-identification).
>
>Conferma di aver abilitato la [[!DNL Mixpanel] funzione di unione identità](#prerequisites-mixpanel) per garantire che i cluster di identità vengano risolti in modo appropriato.

### Raccogliere i dettagli di configurazione richiesti {#configuration-details}

Per connettere Experience Platform a [!DNL Mixpanel] è necessario disporre dei seguenti input:

| Tipo di chiave | Descrizione | Esempio |
| --- | --- | --- |
| Token progetto | Il token di progetto associato al tuo account [!DNL Mixpanel]. Consulta la documentazione di [!DNL Mixpanel] in [come trovare il token di progetto](https://help.mixpanel.com/hc/en-us/articles/115004502806-Find-Project-Token-). | `25470xxxxxxxxxxxxxxxxxxx1289` |

## Installa e configura l&#39;estensione [!DNL Mixpanel] {#install}

Per installare l&#39;estensione, [crea una proprietà di inoltro eventi](../../../ui/event-forwarding/overview.md#properties) o scegli una proprietà esistente da modificare.

Seleziona **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra. Nella scheda **[!UICONTROL Catalogo]**, seleziona **[!UICONTROL Installa]** sulla scheda per l&#39;estensione [!DNL Mixpanel].

![Installazione dell&#39;estensione [!DNL Mixpanel].](../../../images/extensions/server/mixpanel/install-extension.png)

## Crea una regola [!DNL Send Event]

Inizia a creare una nuova regola nella proprietà di inoltro degli eventi. In **[!UICONTROL Azioni]**, aggiungi una nuova azione e imposta l&#39;estensione su **[!UICONTROL Mixpanel]**. Impostare quindi il tipo di azione su **[!UICONTROL Traccia evento]** per inviare eventi di Edge Network a [!DNL Mixpanel].

| Input | Descrizione | Obbligatorio |
| --- | --- | --- |
| [!UICONTROL Token progetto] | Questo campo deve essere mappato al token del progetto associato al tuo account [!DNL Mixpanel]. | Sì |
| [!UICONTROL Tipo evento] | Il nome dell’evento. | Sì |
| [!UICONTROL Ora evento] | Ora dell’evento. | |
| [!UICONTROL ID distinto Mixpanel] | L’identificatore univoco dell’utente che ha eseguito l’evento. | |
| [!UICONTROL Inserisci ID] | Un identificatore univoco dell’evento, utilizzato per la deduplicazione. | |
| [!UICONTROL Proprietà evento] | Oggetto JSON contenente le proprietà personalizzate dell’evento. Scegli se fornire JSON non elaborato o utilizzare un set semplificato di input chiave-valore. | |

>[!NOTE]
>
>Per ulteriori informazioni sui campi standard per un evento [!DNL Mixpanel], consulta la [documentazione ufficiale](https://developer.mixpanel.com/reference/import-events#event).

![Aggiungi una configurazione dell&#39;azione della regola di inoltro eventi.](../../../images/extensions/server/mixpanel/track-event-action.png)

Una volta aggiunta l&#39;azione [!UICONTROL Traccia evento] alla regola, è possibile configurare le condizioni della regola in modo che venga attivata solo per determinati eventi, oppure è possibile lasciare vuota la sezione delle condizioni per attivare la regola per tutti gli eventi.

>[!IMPORTANT]
>
>Se il tuo sito Web utilizza l&#39;SDK [!DNL Mixpanel], puoi passare al passaggio successivo di [convalida dei dati entro [!DNL Mixpanel]](#validate). Se non utilizzi l&#39;SDK [!DNL Mixpanel], devi [creare una regola di tracciamento identità separata](#create-an-identity-tracking-rule) per garantire che gli eventi appropriati e i valori `distinct_id` vengano inviati a [!DNL Mixpanel] quando si verifica un evento di identificazione utente.

## Convalida dati in [!DNL Mixpanel] {#validate}

Se l&#39;implementazione ha esito positivo e gli eventi vengono raccolti, gli eventi verranno visualizzati nella [[!DNL Mixpanel] console](https://help.mixpanel.com/hc/en-us/articles/4402837164948).

Verifica se [!DNL Mixpanel] ha unito gli eventi di post-accesso compilati con valori e-mail e gli eventi creati quando si utilizza **[!UICONTROL Invia evento]**. Se implementato correttamente, [!DNL Mixpanel] li assocerà a un singolo [profilo utente](https://help.mixpanel.com/hc/en-us/articles/115004501966).

## Passaggi successivi

Questa guida illustra come inviare eventi di conversione a [!DNL Mixpanel] tramite l&#39;inoltro di eventi. Questa estensione per l&#39;inoltro degli eventi sfrutta l&#39;SDK [!DNL Mixpanel] e l&#39;API JavaScript. Per ulteriori informazioni su queste tecnologie di base, consulta la documentazione ufficiale:

* [[!DNL Mixpanel] SDK](https://developer.mixpanel.com/docs/nodejs)
* [[!DNL Mixpanel] API JavaScript](https://developer.mixpanel.com/docs/javascript-full-api-reference#mixpanelidentify)

Per ulteriori informazioni sulle funzionalità di inoltro degli eventi in Experience Platform, consulta la [panoramica sull&#39;inoltro degli eventi](../../../ui/event-forwarding/overview.md).
