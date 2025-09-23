---
title: Panoramica dell’estensione Snap Pixel
description: Scopri come utilizzare l’estensione tag Snap Pixel per acquisire interazioni utente di valore in Adobe Experience Platform.
last-substantial-update: 2025-09-17T00:00:00Z
source-git-commit: d846bd5dee5ce0ee8836dc25e20d9fd070714114
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---

# Panoramica dell&#39;estensione [!DNL Snap Pixel]

[[!DNL Snap Pixel]](https://businesshelp.snapchat.com/s/article/snap-pixel-about) è uno strumento di analisi basato su JavaScript che consente di acquisire interazioni utente preziose sul sito Web. Le azioni importanti dei visitatori, come acquisti, iscrizioni o altre conversioni, vengono inviate automaticamente al [Gestione annunci](http://ads.snapchat.com/), consentendo di misurare e ottimizzare le prestazioni di annunci, campagne, percorsi di conversione e altro ancora.

L&#39;estensione tag [!DNL Snap Pixel] consente di integrare la funzionalità [!DNL Snap Pixel] direttamente nelle librerie tag lato client. Questa documentazione illustra come installare l’estensione e implementarne le funzioni all’interno delle regole di gestione dei tag.

L&#39;estensione tag [!DNL Snap Pixel] semplifica l&#39;integrazione della funzionalità [!DNL Snap Pixel] nelle librerie tag lato client esistenti. Questa documentazione illustra come installare l&#39;estensione e configurarne le funzionalità nelle [regole](../../../ui/managing-resources/rules.md) di gestione dei tag.

## Prerequisiti {#prerequisites}

Per utilizzare l&#39;estensione, sarà necessario un account [!DNL Snap] valido con accesso a [!DNL Ads Manager]. Devi [creare un nuovo [!DNL Snap Pixel]](https://forbusiness.snapchat.com/advertising/snap-pixel#about) e copiarne l&#39;ID pixel per configurare l&#39;estensione per il tuo account. Se disponi di un [!DNL Snap Pixel] esistente, puoi semplicemente utilizzarne l&#39;ID.

È consigliabile utilizzare [!DNL Snap Pixel] insieme a [!DNL Snap Conversions API] per inviare gli stessi eventi sia dal lato client che dal lato server. Questo approccio può aiutare a recuperare gli eventi che potrebbero non essere acquisiti solo da [!DNL Snap Pixel]. Consulta l&#39;estensione API [[!DNL Snap] Conversions per l&#39;inoltro degli eventi](../../server/snap/overview.md) per i passaggi su come integrarla nelle implementazioni lato server. Tieni presente che la tua organizzazione deve avere accesso a [inoltro eventi](../../../ui/event-forwarding/overview.md) per utilizzare l&#39;estensione lato server.

## Installare l’estensione {#install}

Per installare l&#39;estensione [!DNL Snap Pixel], passa all&#39;interfaccia utente di Data Collection o all&#39;interfaccia utente di Experience Platform e seleziona **[!UICONTROL Tag]** nell&#39;area di navigazione a sinistra. Da qui, seleziona una proprietà a cui aggiungere l’estensione o creane una nuova.

Dopo aver selezionato o creato la proprietà desiderata, seleziona **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra, quindi seleziona la scheda **[!UICONTROL Catalogo]**. Cerca la scheda [!UICONTROL Snap Pixel], quindi seleziona **[!UICONTROL Installa]**.

![Pulsante [!UICONTROL Installa] selezionato per l&#39;estensione [!UICONTROL Snap Pixel] nell&#39;interfaccia utente di Data Collection.](./images/install.png)

Nella vista di configurazione visualizzata, devi fornire l’ID pixel copiato in precedenza per collegare l’estensione al tuo account. Puoi incollare l’ID direttamente nell’input, oppure selezionare un elemento dati esistente.

Al termine, selezionare **[!UICONTROL Salva]**.

![L&#39;ID [!DNL Pixel] fornito come elemento dati nella vista di configurazione dell&#39;estensione.](./images/configure.png)

L’estensione è installata e ora puoi utilizzarne le varie azioni nelle regole dei tag.

## Configurare una regola di tag {#rule}

[!DNL Snap Pixel] supporta un set di eventi standard predefiniti, ciascuno con contesti specifici e parametri accettati. Le azioni delle regole disponibili nell&#39;estensione [!DNL Snap Pixel] si allineano a questi tipi di evento, semplificando la classificazione e la configurazione degli eventi inviati a [!DNL Snap] in base al tipo.

A scopo dimostrativo, in questa sezione viene illustrato come generare una regola che invia eventi di acquisto a [!DNL Snap].

Per iniziare, crea una nuova regola di tag e definisci le condizioni in base alle esigenze. Durante la configurazione delle azioni della regola, scegli [!DNL Snap Pixel] come estensione, quindi seleziona **[!UICONTROL Invia evento di acquisto]** come tipo di azione.

Dopo aver completato la configurazione dell&#39;azione [!UICONTROL Invia evento di acquisto], seleziona **[!UICONTROL Mantieni modifiche]** per aggiungerla alla configurazione della regola.

![Tipo di azione [!UICONTROL Invia evento di acquisto] selezionato per una regola nell&#39;interfaccia utente di Data Collection.](./images/action-type.png)

Una volta completata la configurazione generale della regola, selezionare **[!UICONTROL Salva nella libreria]**.

Per applicare gli aggiornamenti, pubblica un nuovo tag [build](../../../ui/publishing/builds.md) per abilitare le modifiche alla libreria.

## Conferma che [!DNL Snap] sta ricevendo dati {#confirm}

Dopo aver distribuito la build aggiornata al sito Web, è possibile verificare che i dati vengano inviati come previsto attivando gli eventi di conversione nel browser e verificando che vengano visualizzati in [[!DNL Snap Events Manager]](https://businesshelp.snapchat.com/s/article/events-manager).

## Passaggi successivi {#next-steps}

Questa guida illustra come inviare dati a [!DNL Snap] utilizzando l&#39;estensione tag [!DNL Snap Pixel]. Se si prevede anche di inviare eventi lato server a [!DNL Snap], è possibile procedere all&#39;installazione e alla configurazione di [[!DNL Snap Conversions API event forwarding extension]](../../server/snap/overview.md).
