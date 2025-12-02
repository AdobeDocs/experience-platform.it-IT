---
solution: Experience Platform
title: Introduzione ai playbook con casi d’uso
description: Scopri come iniziare a utilizzare la funzionalità Playbook di casi d’uso.
role: Admin
exl-id: 1c39792e-49fe-4c5f-9796-fa29f60b7461
source-git-commit: d6b62b9539a04be2d2adc7aa66436a294e08303a
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 8%

---


# Introduzione

Scopri come impostare l’account per Use Case Playbook, progettato per Real-Time Customer Data Platform e Adobe Journey Optimizer se non è configurato automaticamente. I tre passaggi principali di configurazione sono:

* Creare una sandbox
* Configurare le autorizzazioni utente
* Configurare le superfici di canale Journey Optimizer per le notifiche e-mail, push e SMS (se si intende utilizzare i playbook Journey Optimizer)

Per accedere a una raccolta completa di playbook di casi d&#39;uso nell&#39;interfaccia utente di Experience Platform, seleziona **[!UICONTROL Playbooks]** dal menu di navigazione a sinistra. Leggi la documentazione su come [esplorare i playbook dei casi d&#39;uso](../playbooks/navigate.md) e iniziare a utilizzare una [sandbox ispiratrice](../playbooks/navigate.md).

## Configurare i playbook di casi d’uso - Procedura dettagliata con video {#video}

Guarda questo video per scoprire i passaggi necessari per creare la sandbox, configurare le autorizzazioni e configurare le superfici di canale per le notifiche e-mail, push e SMS in Journey Optimizer.

>[!VIDEO](https://video.tv.adobe.com/v/3426987?learn=on)

## Creare una sandbox di sviluppo {#create-development-sandbox}

I playbook basati su casi d’uso utilizzano un tipo speciale di sandbox di sviluppo. Per iniziare e accedere alla funzionalità [[!UICONTROL Use Case Playbooks]](/help/use-case-playbooks/playbooks/overview.md), [crea una nuova sandbox di sviluppo](/help/sandboxes/ui/user-guide.md#create) (assicurati di non selezionare una sandbox di produzione) con il nome (non il titolo) che contiene `-ucp` o `-UCP` nel suffisso, come mostrato di seguito.

>[!IMPORTANT]
>
>Quando crei una nuova sandbox di sviluppo, accertati che il nome contenga `-ucp` o `-UCP` nel suffisso.


![Crea una sandbox di sviluppo per i playbook di casi d’uso](/help/use-case-playbooks/assets/playbooks/get-started/create-sandbox-ucp.png)

[!UICONTROL Playbooks] dovrebbe essere visualizzato nella barra a sinistra sotto [!UICONTROL Use Case Playbooks].

![Dopo aver creato la sandbox, utilizza i playbook dei casi d’uso nell’interfaccia utente.](/help/use-case-playbooks/assets/playbooks/get-started/ucp-sandbox-in-ui.png)

Se [!UICONTROL Playbooks] non è visualizzato nella barra a sinistra come mostrato sopra, utilizza questo collegamento `https://experience.adobe.com/#/@<YOUR_ORG>/sname:<YOUR_SANDBOX_NAME>/platform/mexp/templates` per spostarti direttamente qui. Nel collegamento, `<YOUR_ORG>` è il nome della tua organizzazione e `<YOUR_SANDBOX_NAME>` è il nome della sandbox di sviluppo creata.

## Concedi al team le autorizzazioni di accesso richieste {#grant-access-permissions}

Per iniziare a utilizzare [!UICONTROL Use Case Playbooks], i membri del team marketing devono disporre delle autorizzazioni appropriate per poter visualizzare l&#39;elenco dei playbook creati o creare essi stessi i playbook.

**Autorizzazioni richieste**

Per aggiungere le autorizzazioni richieste, nell&#39;interfaccia utente Autorizzazioni, includi la nuova sandbox del playbook del caso d&#39;uso in [ruoli già configurati](/help/access-control/abac/ui/permissions.md#managing-sandboxes-for-role), inclusi quelli utilizzati per altre sandbox di sviluppo.

![Sandbox playbook per ruoli già configurati](/help/use-case-playbooks/assets/playbooks/get-started/permissions-to-existing-roles.png)

**Imposta un ruolo per i playbook:**

In alternativa, è possibile aggiungere nuovi ruoli con [le autorizzazioni richieste](/help/access-control/home.md#sandboxes-and-permissions).

[Configura un nuovo ruolo](/help/access-control/abac/ui/permissions.md) con le autorizzazioni necessarie per le attività essenziali del playbook. Crea un ruolo e aggiungi la nuova sandbox, come illustrato di seguito.

![Crea un ruolo e aggiungilo alla sandbox](/help/use-case-playbooks/assets/playbooks/get-started/create-new-role.png)

**Autorizzazioni per le istanze del playbook**

Come parte dei playbook di Use Case, creerai varie risorse come schemi, tipi di pubblico, destinazioni, percorsi. Per creare questi oggetti, tu e altri utenti dovrete disporre delle autorizzazioni appropriate.

**Autorizzazioni per gli schemi**

Per creare e gestire gli schemi, utilizzare le autorizzazioni di modellazione dati; **[!UICONTROL Manage Schemas]**, **[!UICONTROL View Schemas]**, **[!UICONTROL Manage Relationships]**, **[!UICONTROL Manage Identity Metadata]**

**Autorizzazioni per le destinazioni**

Per creare e gestire le destinazioni, utilizzare le autorizzazioni Destinazioni; **[!UICONTROL Manage]**, **[!UICONTROL Destinations]**, **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL Activate Segment without Mapping]**, **[!UICONTROL Manage and Activate Dataset Destination]**, **[!UICONTROL Destination Authoring]**.

**Autorizzazioni per percorsi**

Per creare e gestire i percorsi, utilizzare le autorizzazioni Percorsi; **[!UICONTROL Manage Journeys]**, **[!UICONTROL View Journeys]**, **[!UICONTROL View Journeys Report]**, **[!UICONTROL Manage Journeys]**, **[!UICONTROL Events]**, **[!UICONTROL Data Sources and Actions]**, **[!UICONTROL View Journeys]**, **[!UICONTROL Events]**, **[!UICONTROL Data Sources and Actions, Publish Journeys]**.

L’immagine seguente mostra un’istantanea delle autorizzazioni consigliate agli utenti per visualizzare, creare e gestire i playbook e le risorse generate dai playbook.

![Istantanea di tutti gli elementi di autorizzazione necessari per creare tutte le istanze dei playbook](/help/use-case-playbooks/assets/playbooks/get-started/permission-snapshot.png)

**Aggiungi utenti al ruolo**

Dopo aver [creato una nuova mansione](/help/access-control/abac/ui/permissions.md#managing-users-for-role) come indicato sopra, aggiungiti come utente. Se si crea un ruolo con accesso limitato per un altro gruppo di utenti con accesso in sola visualizzazione, includere solo gli elementi di visualizzazione necessari associati a tali autorizzazioni.

## Configurare le superfici di sandbox e di canale in Journey Optimizer {#configure-channel-surfaces}

Se la tua organizzazione dispone della licenza per [Adobe Journey Optimizer](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/ajo-home) e desideri utilizzare i playbook progettati per Journey Optimizer, configura le superfici di canale nella sandbox. Le superfici di canale definiscono tutti i parametri tecnici richiesti per i messaggi, ad esempio il tipo di e-mail, l’e-mail e il nome del mittente, le app mobili, la configurazione degli SMS e altro ancora. [Scopri come impostare le superfici di canale in Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/channel-surfaces).

Per creare istanze di playbook in Journey Optimizer, devi configurare le superfici di canale per le notifiche e-mail, push e SMS.

### Superficie del canale e-mail

Passare a `Channels` nell&#39;interfaccia di Journey Optimizer. Se non sono già configurati, configura sottodomini e pool IP separati per le e-mail di marketing e la messaggistica transazionale. Si tratta di best practice per garantire che i messaggi transazionali, come le e-mail di conferma dell’ordine, arrivino ai clienti. Immetti nomi, indirizzi e-mail e impostazioni aggiuntive. Seleziona **Invia** in alto a destra della pagina per creare la superficie del canale di marketing. Leggi la documentazione su [come impostare le superfici dei canali di posta elettronica](https://experienceleague.adobe.com/docs/journey-optimizer/using/email/configure-email/email-settings.html).

### Superficie del canale SMS

Per creare una superficie di canale SMS, crea innanzitutto una credenziale API SMS e seleziona il fornitore preferito (ad esempio, Sinch). Denomina la superficie del canale SMS (ad esempio, SMS Marketing), seleziona la configurazione e immetti un numero mittente. Seleziona **Invia** in alto a destra della pagina per salvare la superficie del canale SMS. Leggi la documentazione su [come configurare le superfici di canale SMS](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=it#message-preset-sms).

Configura anche i canali per i playbook che contengono messaggi transazionali come le conferme degli ordini.

### Superficie di canale push

Conferma che le configurazioni del canale siano configurate dall’interfaccia di Experience Platform o di Data Collections. Questa è l’aspetto delle configurazioni del canale nell’ambiente Raccolta dati.

<!-- ![Channel configurations in Data collections](/help/use-case-playbooks/assets/playbooks/get-started/.png) -->

Quindi, seleziona il canale, le piattaforme e le app che hai visualizzato nelle configurazioni del canale. Seleziona **Invia** per creare la superficie del canale push.

Leggi la documentazione su [come impostare le superfici dei canali push](https://experienceleague.adobe.com/docs/journey-optimizer/using/push/push-config/push-configuration.html).

## Passaggi successivi {#next-steps}

Dopo aver seguito tutti i passaggi descritti in questo documento, dovresti aver creato una sandbox di sviluppo con i playbook Use Case disponibili nel menu di navigazione a sinistra. Ora sai anche come concedere ai membri del gruppo le autorizzazioni necessarie per visualizzare e gestire i playbook e generare risorse. Come passo successivo, leggi come [scegliere il playbook corretto](/help/use-case-playbooks/playbooks/choose.md) per te e quindi [crearne delle istanze](/help/use-case-playbooks/playbooks/create-share-reuse.md).
