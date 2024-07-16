---
solution: Experience Platform
title: Passa a Playbook casi d’uso
description: Scopri come navigare in una galleria di playbook e iniziare con una sandbox ispirativa.
role: User
exl-id: 1f5dae75-1136-4be3-9132-01d36a4066ca
source-git-commit: 54b3d2ef22f7afb47fa8c9430c5c1645c94c837d
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 2%

---

# Passa a Playbook casi d’uso

I playbook dei casi d&#39;uso sono disponibili senza costi aggiuntivi per tutti i clienti Adobe Experience Platform. Per accedere a una raccolta completa di playbook di casi d&#39;uso nell&#39;interfaccia utente di Experience Platform, seleziona **[!UICONTROL Playbook]** dal menu di navigazione a sinistra.

![Raccolta playbook casi d&#39;uso.](/help/use-case-playbooks/assets/playbooks/discover/playbooks-gallery.png)

![Accesso diretto ai playbook di casi d&#39;uso nella barra di navigazione a sinistra.](/help/use-case-playbooks/assets/playbooks/discover/left-nav-playbooks.png)

Seleziona un playbook per passare alla pagina dei dettagli, quindi seleziona **[!UICONTROL Vai a una sandbox ispiratrice]**. Viene visualizzata una finestra modale di conferma. Seleziona **Conferma** per passare alla sandbox ispiratrice in cui puoi esplorare e sperimentare i diversi casi d&#39;uso.

Se non disponi dell’autorizzazione per creare sandbox, contatta il tuo amministratore per assistenza nella creazione di una sandbox ispiratrice.

>[!TIP]
>
>Una sandbox che ispira è una sandbox di sviluppo all’interno di Adobe Experience Platform in cui puoi creare, testare e sperimentare diversi casi d’uso prima di implementarli in un ambiente di produzione live.

![Vai alla sandbox di ispirazione.](/help/use-case-playbooks/assets/playbooks/discover/inspirational-sandbox.png)

Se non hai già configurato alcuna sandbox ispiratrice, seleziona **[!UICONTROL Crea una sandbox ispiratrice]**. Viene visualizzata una finestra modale. Immetti **Nome** e **Titolo** nelle caselle obbligatorie e seleziona **Crea**. Dopo aver creato la sandbox di ispirazione, assicurati di [definire le autorizzazioni](/help/access-control/home.md) prima di tornare alla pagina dei dettagli dei playbook del caso d&#39;uso per creare un&#39;istanza.

![Crea una sandbox ispiratrice.](/help/use-case-playbooks/assets/playbooks/discover/create-inspirational-sandbox.png)

![Inserisci nome e titolo per creare una sandbox che ispiri.](/help/use-case-playbooks/assets/playbooks/discover/create-inspirational-sandbox-modal.png)

Se selezioni un playbook di casi d’uso dall’esterno di una sandbox illuminante, non potrai creare un’istanza. Nella pagina dei dettagli, seleziona **Vai a sandbox ispirativa** per passare a una sandbox ispirativa esistente, quindi seleziona **[!UICONTROL Crea istanza]**.

Se non disponi dell’autorizzazione per creare sandbox, contatta il tuo amministratore per assistenza nella creazione di una sandbox ispiratrice.

![Nessuna autorizzazione per la creazione di sandbox.](/help/use-case-playbooks/assets/playbooks/discover/no-permissions-to-create-sandbox.png)

Se hai raggiunto il limite del numero di sandbox allocate, viene visualizzato un messaggio che ti chiede di contattare l’amministratore dell’organizzazione per aumentare il limite o disattivare o rimuovere alcune sandbox attive. Una volta regolato il limite di sandbox o ridotto il numero di sandbox attive, puoi procedere alla creazione della sandbox ispiratrice.

![Limite sandbox raggiunto.](/help/use-case-playbooks/assets/playbooks/discover/sandbox-limit-reached.png)

Tieni presente che quando crei una sandbox che ispira, le superfici di canale per le notifiche e-mail, push e SMS non vengono impostate automaticamente. Contatta l’amministratore IT per configurarli manualmente, altrimenti la creazione dell’istanza potrebbe non riuscire.

![Configurare i predefiniti per il canale.](/help/use-case-playbooks/assets/playbooks/discover/configure-channel-presets.png)

## Configurare le superfici di sandbox e di canale in Journey Optimizer {#configure-channel-surfaces}

Se la tua organizzazione dispone della licenza per [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=it) e desideri utilizzare i playbook progettati per Journey Optimizer, devi configurare i predefiniti di canale nella sandbox, che definiscono i parametri tecnici richiesti per i messaggi. [Scopri come impostare le superfici di canale in Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/channel-surfaces.html?lang=it).

Per creare istanze di playbook in Journey Optimizer, devi configurare le superfici di canale per le notifiche e-mail, push e SMS.

### Superficie del canale e-mail

Passare a `Channels` nell&#39;interfaccia di Journey Optimizer. Se non sono già configurati, configura sottodomini e pool IP separati per le e-mail di marketing e la messaggistica transazionale. Si tratta di best practice per garantire che i messaggi transazionali, come le e-mail di conferma dell’ordine, arrivino ai clienti. Immetti nomi, indirizzi e-mail e impostazioni aggiuntive. Seleziona **Invia** in alto a destra della pagina per creare la superficie del canale di marketing. Leggi la documentazione su [come impostare le superfici dei canali di posta elettronica](https://experienceleague.adobe.com/docs/journey-optimizer/using/email/configure-email/email-settings.html).

### Superficie del canale SMS

Per creare una superficie di canale SMS, crea innanzitutto una credenziale API SMS e seleziona il fornitore preferito (ad esempio, Sinch). Denomina la superficie del canale SMS (ad esempio, SMS Marketing), seleziona la configurazione e immetti un numero mittente. Seleziona **Invia** in alto a destra della pagina per salvare la superficie del canale SMS. Leggi la documentazione su [come configurare le superfici di canale SMS](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=it#message-preset-sms).

Configura anche i canali per i playbook che contengono messaggi transazionali come le conferme degli ordini.

### Superficie di canale push

Verifica che le superfici dell’app siano configurate dall’interfaccia Experience Platform o Data Collections. Questo è l’aspetto delle superfici dell’app nell’ambiente Raccolte dati.

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, dovresti sapere come impostare una sandbox ispiratrice e conoscere diversi modi per accedere ai playbook dei casi d’uso in Platform. Come passo successivo, leggi come [scegliere](/help/use-case-playbooks/playbooks/choose.md) il playbook corretto.
