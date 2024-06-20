---
solution: Experience Platform
title: Introduzione ai playbook con casi d’uso
description: Scopri come iniziare a utilizzare la funzionalità Playbook di casi d’uso.
role: Admin
exl-id: 1c39792e-49fe-4c5f-9796-fa29f60b7461
source-git-commit: 54b3d2ef22f7afb47fa8c9430c5c1645c94c837d
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 15%

---


# Introduzione

Scopri come impostare l’account per Use Case Playbook, progettato per Real-time Customer Data Platform e Adobe Journey Optimizer se non è configurato automaticamente. I tre passaggi principali di configurazione sono:

* Creare una sandbox
* Configurare le autorizzazioni utente
* Configurare le superfici di canale Journey Optimizer per le notifiche e-mail, push e SMS (se si intende utilizzare i playbook Journey Optimizer)

## Configurare i playbook di casi d’uso - Procedura dettagliata con video {#video}

Guarda questo video per scoprire i passaggi necessari per creare la sandbox, configurare le autorizzazioni e configurare le superfici di canale per le notifiche e-mail, push e SMS in Journey Optimizer.

>[!VIDEO](https://video.tv.adobe.com/v/3426987?learn=on)

## Creare una sandbox di sviluppo {#create-development-sandbox}

I playbook basati su casi d’uso utilizzano un tipo speciale di sandbox di sviluppo. Per iniziare e accedere alla funzionalità [[!UICONTROL Playbook di casi d’uso]](/help/use-case-playbooks/playbooks/overview.md), [crea una nuova sandbox di sviluppo](/help/sandboxes/ui/user-guide.md#create) (accertati di non selezionare una sandbox di produzione) il cui nome (non il titolo) contiene `-ucp` o `-UCP` nel suffisso, come illustrato di seguito.

>[!IMPORTANT]
>
>Quando crei una nuova sandbox di sviluppo, accertati che il nome contenga `-ucp` o `-UCP` nel suffisso.


![Crea una sandbox di sviluppo per i playbook di casi d’uso](/help/use-case-playbooks/assets/playbooks/get-started/create-sandbox-ucp.png)

Ora dovresti vedere [!UICONTROL Playbook] nella barra a sinistra sotto [!UICONTROL Playbook di casi d’uso].

![Dopo aver creato la sandbox, utilizza i playbook dei casi d’uso nell’interfaccia utente.](/help/use-case-playbooks/assets/playbooks/get-started/ucp-sandbox-in-ui.png)

Se non vedi [!UICONTROL Playbook] nella barra a sinistra, come illustrato in precedenza, utilizza questo collegamento `https://experience.adobe.com/#/@<YOUR_ORG>/sname:<YOUR_SANDBOX_NAME>/platform/mexp/templates` per passare direttamente a tale posizione. Nel collegamento, `<YOUR_ORG>` è il nome della tua organizzazione e `<YOUR_SANDBOX_NAME>` è il nome della sandbox di sviluppo creata.

## Concedi al team le autorizzazioni di accesso richieste {#grant-access-permissions}

Per iniziare a utilizzare [!UICONTROL Playbook di casi d’uso], i membri del team marketing devono disporre delle autorizzazioni appropriate per poter visualizzare l’elenco dei playbook creati o creare essi stessi i playbook.

**Autorizzazioni richieste**

Per aggiungere le autorizzazioni richieste, nell’interfaccia utente Autorizzazioni, includi la nuova sandbox del playbook per il caso d’uso in [ruoli già configurati](/help/access-control/abac/ui/permissions.md#managing-sandboxes-for-role), inclusi quelli utilizzati per altre sandbox di sviluppo.

![Sandbox playbook per ruoli già configurati](/help/use-case-playbooks/assets/playbooks/get-started/permissions-to-existing-roles.png)

**Imposta un ruolo per i playbook:**

In alternativa, è possibile aggiungere nuovi ruoli con [le autorizzazioni richieste](/help/access-control/home.md#sandboxes-and-permissions).

[Imposta un nuovo ruolo](/help/access-control/abac/ui/permissions.md) con i permessi necessari per le mansioni essenziali del playbook. Crea un ruolo e aggiungi la nuova sandbox, come illustrato di seguito.

![Creare un ruolo e aggiungerlo alla sandbox](/help/use-case-playbooks/assets/playbooks/get-started/create-new-role.png)

**Autorizzazioni per le istanze del playbook**

Come parte dei playbook di Use Case, creerai varie risorse come schemi, tipi di pubblico, destinazioni, percorsi. Per creare questi oggetti, tu e altri utenti dovrete disporre delle autorizzazioni appropriate.

**Autorizzazioni per gli schemi**

Per creare e gestire gli schemi, utilizza le autorizzazioni di modellazione dati; **[!UICONTROL Gestire gli schemi]**, **[!UICONTROL Visualizzare gli schemi]**, **[!UICONTROL Gestire le relazioni]**, **[!UICONTROL Gestire i metadati di identità]**

**Autorizzazioni per le destinazioni**

Per creare e gestire le destinazioni, utilizza le autorizzazioni Destinazioni; **[!UICONTROL Gestisci]**, **[!UICONTROL Destinazioni]**, **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Attiva segmento senza mappatura]**, **[!UICONTROL Gestire e attivare la destinazione del set di dati]**, **[!UICONTROL Authoring delle destinazioni]**.

**Autorizzazioni per i percorsi**

Per creare e gestire i percorsi, utilizza le autorizzazioni Percorsi; **[!UICONTROL Gestisci Percorsi]**, **[!UICONTROL Visualizza Percorsi]**, **[!UICONTROL Visualizza rapporto Percorsi]**, **[!UICONTROL Gestisci Percorsi]**, **[!UICONTROL Eventi]**, **[!UICONTROL Origini dati e azioni]**, **[!UICONTROL Visualizza Percorsi]**, **[!UICONTROL Eventi]**, **[!UICONTROL Origini dati e azioni, Percorsi Publish]**.

L’immagine seguente mostra un’istantanea delle autorizzazioni consigliate agli utenti per visualizzare, creare e gestire i playbook e le risorse generate dai playbook.

![Snapshot di tutti gli elementi di autorizzazione necessari per creare tutte le istanze dei playbook](/help/use-case-playbooks/assets/playbooks/get-started/permission-snapshot.png)

**Aggiungere utenti al ruolo**

Una volta [ha creato un nuovo ruolo](/help/access-control/abac/ui/permissions.md#managing-users-for-role) come indicato sopra, aggiungiti come utente a esso. Se si crea un ruolo con accesso limitato per un altro gruppo di utenti con accesso in sola visualizzazione, includere solo gli elementi di visualizzazione necessari associati a tali autorizzazioni.

## Configurare le superfici di sandbox e di canale in Journey Optimizer {#configure-channel-surfaces}

Se la tua organizzazione dispone della licenza per [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=it)e per utilizzare i playbook progettati per Journey Optimizer, devi configurare i predefiniti di canale nella sandbox, che definiscono i parametri tecnici richiesti per i messaggi. [Scopri come impostare le superfici di canale in Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/channel-surfaces.html?lang=it).

Per creare istanze di playbook in Journey Optimizer, devi configurare le superfici di canale per le notifiche e-mail, push e SMS.

### Superficie del canale e-mail

Vai a `Channels` nell’interfaccia di Journey Optimizer. Se non sono già configurati, configura sottodomini e pool IP separati per le e-mail di marketing e la messaggistica transazionale. Si tratta di best practice per garantire che i messaggi transazionali, come le e-mail di conferma dell’ordine, arrivino ai clienti. Immetti nomi, indirizzi e-mail e impostazioni aggiuntive. Seleziona **Invia** in alto a destra per creare la superficie del canale di marketing. Leggi la documentazione su [come impostare le superfici dei canali di posta elettronica](https://experienceleague.adobe.com/docs/journey-optimizer/using/email/configure-email/email-settings.html).

### Superficie del canale SMS

Per creare una superficie di canale SMS, crea innanzitutto una credenziale API SMS e seleziona il fornitore preferito (ad esempio, Sinch). Denomina la superficie del canale SMS (ad esempio, SMS Marketing), seleziona la configurazione e immetti un numero mittente. Seleziona **Invia** in alto a destra nella pagina per salvare la superficie del canale SMS. Leggi la documentazione su [come impostare le superfici di canale SMS](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=it#message-preset-sms).

Configura anche i canali per i playbook che contengono messaggi transazionali come le conferme degli ordini.

### Superficie di canale push

Verifica che le superfici dell’app siano configurate dall’interfaccia Experienci Platform o Data Collections. Questo è l’aspetto delle superfici dell’app nell’ambiente Raccolte dati.

<!-- ![App surfaces in Data collections](/help/use-case-playbooks/assets/playbooks/get-started/.png) -->

Quindi, seleziona il canale, le piattaforme e le app che hai visualizzato nelle configurazioni della superficie dell’app. Seleziona **Invia** per creare la superficie del canale push.

Leggi la documentazione su [come impostare le superfici di canale push](https://experienceleague.adobe.com/docs/journey-optimizer/using/push/push-config/push-configuration.html).

## Passaggi successivi {#next-steps}

Dopo aver seguito tutti i passaggi descritti in questo documento, dovresti aver creato una sandbox di sviluppo con i playbook Use Case disponibili nel menu di navigazione a sinistra. Ora sai anche come concedere ai membri del gruppo le autorizzazioni necessarie per visualizzare e gestire i playbook e generare risorse. Come passaggio successivo, leggi come [scegli il playbook giusto](/help/use-case-playbooks/playbooks/choose.md) per te e poi [crea istanze da esso](/help/use-case-playbooks/playbooks/create-share-reuse.md).
