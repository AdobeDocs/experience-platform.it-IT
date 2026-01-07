---
keywords: Experience Platform;home;argomenti popolari;controllo degli accessi;controllo degli accessi basato su attributi;ABAC;;home;popular topic;access control;attribute-based access control;ABAC
title: Gestire i criteri di controllo di accesso
description: Gestisci i criteri di controllo dell’accesso tramite l’interfaccia Autorizzazioni in Adobe Experience Cloud.
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: 2a26c8786adc412dc643c8a0c94b966e439e034b
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 8%

---

# Gestire i criteri di controllo dell’accesso

I criteri di controllo degli accessi sono istruzioni che riuniscono attributi per stabilire azioni consentite e inammissibili. Adobe fornisce un criterio predefinito che può essere attivato immediatamente o quando l&#39;organizzazione è pronta per iniziare a controllare l&#39;accesso a oggetti specifici in base a [etichette](./labels.md){target="_blank"}. Il criterio predefinito **[!UICONTROL Default-Label-Based-Access-Control-Policy]** sfrutta le etichette applicate alle risorse per negare l&#39;accesso, a meno che gli utenti non abbiano un ruolo con un&#39;etichetta corrispondente.

>[!IMPORTANT]
>
>I criteri di controllo degli accessi non devono essere confusi con i criteri di utilizzo dei dati, che controllano il modo in cui i dati vengono utilizzati in Adobe Experience Platform. Per ulteriori informazioni, consulta la guida sulla creazione di [criteri di utilizzo dei dati](../../../data-governance/policies/create.md){target="_blank"}.

## Configurare le sandbox per un criterio {#configure-policy}

I criteri vengono applicati a livello di sandbox per controllare quali sandbox applicano il controllo degli accessi basato su etichette. Per impostazione predefinita, la funzione **[!UICONTROL Auto-include]** è attivata, il che significa che tutte le sandbox attuali e future vengono aggiunte automaticamente al criterio. Quando **[!UICONTROL Auto-include]** è disattivato, solo le sandbox aggiunte manualmente saranno soggette alle regole di controllo di accesso del criterio.

>[!NOTE]
>
>Il criterio **[!UICONTROL Default-Label-Based-Access-Control-Policy]** è attualmente l&#39;unico disponibile per la configurazione.

Per iniziare a configurare le sandbox di un criterio, passa a **[!UICONTROL Permissions]** in [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"}. Seleziona **[!UICONTROL Policies]** dal pannello a sinistra, quindi seleziona **[!UICONTROL Default-Label-Based-Access-Control-Policy]** dall&#39;elenco.

![L&#39;area di lavoro dei criteri visualizza un elenco dei criteri esistenti.](../../images/ui/policies/policies-home.png){zoomable="yes"}

Viene visualizzata l’area di lavoro dei dettagli del criterio. Selezionare la scheda **[!UICONTROL Sandboxes]** per visualizzare l&#39;elenco delle sandbox associate al criterio e accedere alle opzioni di configurazione sandbox.

![L&#39;area di lavoro sandbox del criterio mostra un elenco di sandbox associate.](../../images/ui/policies/policy-sandbox.png){zoomable="yes"}

### Gestisci inclusione automatica {#manage-auto-include}

>[!IMPORTANT]
>
>Per impostazione predefinita, **[!UICONTROL Auto-include]** è attivato, il che significa che tutte le sandbox attuali e future vengono aggiunte automaticamente al criterio.

Per controllare quali sandbox sono incluse in un criterio, puoi attivare o disattivare la funzione **[!UICONTROL Auto-include]**. Quando disattivi **[!UICONTROL Auto-include]**, le sandbox future non verranno aggiunte automaticamente al criterio. Tuttavia, la disattivazione della funzionalità **non rimuoverà** le sandbox già incluse nel criterio.

![Scheda sandbox del criterio con l&#39;opzione di inclusione automatica evidenziata e disattivata.](../../images/ui/policies/policy-auto-include.png){zoomable="yes"}

Per riattivare **[!UICONTROL Auto-include]**, utilizzare l&#39;interruttore per riattivarlo. Viene visualizzata la finestra di dialogo **[!UICONTROL Enable Auto-include]** in cui viene richiesto di confermare la selezione. Selezionare **[!UICONTROL Enable]** per completare l&#39;impostazione di configurazione.

>[!NOTE]
>
>Quando riattivi **[!UICONTROL Auto-include]**, tutte le sandbox precedentemente rimosse dal criterio verranno aggiunte di nuovo.

![La finestra di dialogo Abilita inclusione automatica con l&#39;opzione Abilita evidenziata.](../../images/ui/policies/policy-enable-auto-include.png){zoomable="yes"}

### Gestire manualmente le sandbox {#manually-manage-sandboxes}

Quando **[!UICONTROL Auto-include]**&#x200B;è disattivato, è possibile aggiungere o rimuovere manualmente sandbox specifiche dal criterio. Questo offre un controllo preciso sulle sandbox che applicano le regole di controllo dell’accesso del criterio.

>[!NOTE]
>
>Per aggiungere o rimuovere manualmente le sandbox, l&#39;interruttore **[!UICONTROL Auto-include]** **deve** essere disattivato.

**Per aggiungere sandbox:**

Seleziona **[!UICONTROL Add Sandboxes]** dall&#39;area di lavoro sandbox del criterio.

![Area di lavoro del criterio con l&#39;opzione Aggiungi sandbox evidenziata.](../../images/ui/policies/policy-add-sandboxes.png){zoomable="yes"}

Viene visualizzata la finestra di dialogo **[!UICONTROL Add Sandboxes]**, in cui viene visualizzata la raccolta di sandbox disponibili. Selezionare le sandbox da aggiungere al criterio, quindi selezionare **[!UICONTROL Save]**.

![Finestra di dialogo Aggiungi sandbox con sandbox selezionata ed opzione Salva evidenziata.](../../images/ui/policies/policy-add-sandboxes-select.png){zoomable="yes"}

>[!NOTE]
>
>Se nel criterio sono già incluse tutte le sandbox disponibili, nella finestra di dialogo viene visualizzato il messaggio &quot;Non hai nulla nella libreria&quot;.

**Per rimuovere le sandbox:**

Individua la sandbox da rimuovere dall&#39;elenco e seleziona l&#39;icona **X** accanto al nome.

![Elenco di sandbox del criterio con una &quot;x&quot; evidenziata per rimuovere una sandbox.](../../images/ui/policies/policy-remove-sandbox.png){zoomable="yes"}

Viene visualizzata una finestra di dialogo di conferma. Seleziona **[!UICONTROL Confirm]** per completare la rimozione della sandbox dal criterio.

![Finestra di dialogo di conferma di una sandbox con l&#39;opzione Conferma evidenziata.](../../images/ui/policies/policy-remove-sandbox-confirmation.png){zoomable="yes"}

## Attivare un criterio {#activate-policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="Cosa sono i criteri?"
>abstract="I criteri sono dichiarazioni che riuniscono alcuni attributi al fine di definire azioni ammissibili e non ammissibili. A ogni organizzazione viene fornito un criterio predefinito che è necessario attivare per iniziare a controllare l’accesso a oggetti specifici in base alle etichette. Le etichette applicate alle risorse negano l’accesso a meno che gli utenti non siano assegnati a un ruolo con un’etichetta corrispondente. Non è possibile modificare o eliminare i criteri, ma è possibile attivarli o disattivarli."
>additional-url="https://experienceleague.adobe.com/it/docs/experience-platform/access-control/abac/permissions-ui/labels" text="Gestire le etichette"

Per attivare un criterio esistente, selezionarlo dalla scheda **[!UICONTROL Policies]** in **[!UICONTROL Permissions]**. Lo stato di attivazione del criterio è visibile nella sezione **[!UICONTROL Status]**.

![Area di lavoro criteri con lo stato di un criterio evidenziato.](../../images/ui/policies/policy-status.png){zoomable="yes"}

Verrà visualizzata l’area di lavoro dei dettagli del criterio. Seleziona **[!UICONTROL Activate]**.

![Area di lavoro dettagli del criterio con l&#39;opzione Attiva evidenziata.](../../images/ui/policies/policy-activate.png){zoomable="yes"}

Viene visualizzata la finestra di dialogo **[!UICONTROL Activate Policy]**. Selezionare **[!UICONTROL Confirm]** per completare l&#39;attivazione del criterio.

![La finestra di dialogo Attiva criterio con l&#39;opzione Conferma evidenziata.](../../images/ui/policies/policy-activate-confirm.png){zoomable="yes"}

## Passaggi successivi

Attivando un criterio, puoi passare al passaggio successivo per [gestire le autorizzazioni per un ruolo](permissions.md).
