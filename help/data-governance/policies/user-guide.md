---
keywords: Experience Platform;home;argomenti popolari;governance dei dati;guida utente per i criteri di utilizzo dei dati
solution: Experience Platform
title: Gestire i criteri di utilizzo dei dati nell’interfaccia utente
description: La governance dei dati di Adobe Experience Platform fornisce un’interfaccia utente che consente di creare e gestire i criteri di utilizzo dei dati. Questo documento fornisce una panoramica delle azioni che è possibile eseguire nell’area di lavoro Criteri nell’interfaccia utente di Experience Platform.
exl-id: 29434dc1-02c2-4267-a1f1-9f73833e76a0
source-git-commit: e539b1e165227d9a888bfe12d8205e285b3ce259
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 0%

---

# Gestire i criteri di utilizzo dei dati nell’interfaccia utente {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsagePolicies_description"
>title="Descrizione"
>abstract=""

Questo documento illustra come utilizzare **[!UICONTROL Criteri]** nell’interfaccia utente di Adobe Experience Platform per creare e gestire i criteri di utilizzo dei dati.

>[!NOTE]
>
>Per informazioni su come gestire i criteri di controllo di accesso nell’interfaccia utente, consulta [guida dell’interfaccia utente per il controllo degli accessi basato su attributi](../../access-control/abac/ui/policies.md) invece.

>[!IMPORTANT]
>
>Tutti i criteri di utilizzo dei dati (inclusi i criteri principali forniti da Adobe) sono disabilitati per impostazione predefinita. Affinché un singolo criterio possa essere preso in considerazione per l’applicazione, è necessario abilitarlo manualmente. Consulta la sezione su [abilitazione delle policy](#enable) per i passaggi su come eseguire questa operazione nell’interfaccia utente.

## Prerequisiti

Questa guida richiede una buona conoscenza di quanto segue [!DNL Experience Platform] concetti:

* [Governance dei dati](../home.md)
* [Criteri di utilizzo dei dati](./overview.md)

## Visualizza criteri esistenti {#view-policies}

In [!DNL Experience Platform] UI, seleziona **[!UICONTROL Criteri]** per aprire **[!UICONTROL Criteri]** Workspace. In **[!UICONTROL Sfoglia]** , puoi visualizzare un elenco dei criteri disponibili, comprese le etichette associate, le azioni di marketing e lo stato.

![](../images/policies/browse-policies.png)

Se hai accesso ai criteri di consenso, seleziona la **[!UICONTROL Criteri di consenso]** per visualizzarli in [!UICONTROL Sfoglia] scheda.

![](../images/policies/consent-policy-toggle.png)

Selezionare un criterio elencato per visualizzarne la descrizione e il tipo. Se è selezionato un criterio personalizzato, vengono visualizzati controlli aggiuntivi per la modifica, l’eliminazione o [abilita/disabilita il criterio](#enable).

![](../images/policies/policy-details.png)

## Creare un criterio personalizzato {#create-policy}

Per creare un nuovo criterio di utilizzo dati personalizzato, seleziona **[!UICONTROL Crea criterio]** nell&#39;angolo in alto a destra del **[!UICONTROL Sfoglia]** scheda in **[!UICONTROL Criteri]** Workspace.

![](../images/policies/create-policy-button.png)

A seconda che tu faccia parte della versione beta dei criteri di consenso, si verifica una delle seguenti situazioni:

* Se non fai parte della versione beta, vieni immediatamente portato al flusso di lavoro per [creazione di un criterio di governance dei dati](#create-governance-policy).
* Se fai parte della versione beta, una finestra di dialogo fornisce un’opzione aggiuntiva per [creare un criterio di consenso](#consent-policy).
   ![](../images/policies/choose-policy-type.png)

### Creare un criterio di governance dei dati {#create-governance-policy}

Il **[!UICONTROL Crea criterio]** viene visualizzato workflow. Per iniziare, specifica un nome e una descrizione per il nuovo criterio.

![](../images/policies/create-policy-description.png)

Quindi, seleziona le etichette di utilizzo dei dati su cui basare il criterio. Quando selezioni più etichette, puoi scegliere se i dati devono contenere tutte le etichette o solo una di esse affinché il criterio venga applicato. Seleziona **[!UICONTROL Successivo]** al termine.

![](../images/policies/add-labels.png)

Il **[!UICONTROL Seleziona azioni di marketing]** viene visualizzato il passaggio. Scegli le azioni di marketing appropriate dall’elenco fornito, quindi seleziona **[!UICONTROL Successivo]** per continuare.

>[!NOTE]
>
>Quando si selezionano più azioni di marketing, il criterio le interpreta come una regola &quot;OR&quot;. In altre parole, la politica si applica se **qualsiasi** delle azioni di marketing selezionate vengono eseguite.

![](../images/policies/add-marketing-actions.png)

Il **[!UICONTROL Revisione]** viene visualizzato un passaggio che consente di rivedere i dettagli del nuovo criterio prima di crearlo. Una volta che sei soddisfatto, seleziona **[!UICONTROL Fine]** per creare il criterio.

![](../images/policies/policy-review.png)

Il **[!UICONTROL Sfoglia]** viene visualizzata di nuovo la scheda, che ora elenca il criterio appena creato nello stato &quot;Bozza&quot;. Per abilitare il criterio, vedere la sezione successiva.

![](../images/policies/created-policy.png)

### Creare un criterio di consenso {#consent-policy}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsagePolicies_instructions"
>title="Istruzioni"
>abstract=""

>[!IMPORTANT]
>
>I criteri di consenso sono disponibili solo per le organizzazioni che hanno acquistato **Schermo sanitario Adobe** o **Adobe Privacy &amp; Security Shield**.

Se hai scelto di creare un criterio di consenso, viene visualizzata una nuova schermata che ti consente di configurare il nuovo criterio.

![](../images/policies/consent-policy-dialog.png)

Per utilizzare i criteri di consenso, devi disporre di attributi di consenso presenti nei dati del profilo. Consulta la guida su [elaborazione del consenso in Experience Platform](../../landing/governance-privacy-security/consent/adobe/overview.md) per i passaggi dettagliati su come includere gli attributi richiesti nello schema di unione.

I criteri di consenso sono composti da due componenti logici:

* **[!UICONTROL Se]**: la condizione che attiverà il controllo dei criteri. Ciò può essere basato sull’esecuzione di una determinata azione di marketing, sulla presenza di determinate etichette di utilizzo dei dati o su una combinazione delle due.
* **[!UICONTROL Then]**: attributi di consenso che devono essere presenti affinché un profilo sia incluso nell’azione che ha attivato il criterio.

#### Configurare le condizioni {#consent-conditions}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_consentif"
>title="Condizione If"
>abstract="Inizia definendo le condizioni che attiveranno il controllo dei criteri. Le condizioni possono includere l’esecuzione di determinate azioni di marketing, la presenza di determinate etichette di governance dei dati o una combinazione di entrambe."

Sotto **[!UICONTROL Se]** , seleziona le azioni di marketing e/o le etichette di utilizzo dei dati che devono attivare questo criterio. Seleziona **[!UICONTROL Visualizza tutto]** e **[!UICONTROL Seleziona etichette]** per visualizzare rispettivamente l’elenco completo delle azioni di marketing e delle etichette disponibili.

Dopo aver aggiunto almeno una condizione, puoi selezionare **[!UICONTROL Aggiungi condizione]** per continuare ad aggiungere ulteriori condizioni, se necessario, scegli il tipo di condizione appropriato dal menu a discesa.

![](../images/policies/add-condition.png)

Se selezioni più di una condizione, puoi utilizzare l’icona che appare tra di esse per cambiare la relazione condizionale tra &quot;AND&quot; e &quot;OR&quot;.

![](../images/policies/and-or-selection.png)

#### Seleziona attributi di consenso {#consent-attributes}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_consentthen"
>title="Condizione Then"
>abstract="Una volta definita la condizione &quot;If&quot;, utilizza la sezione &quot;Then&quot; per selezionare almeno un attributo di consenso dallo schema di unione. Questo è l’attributo che deve essere presente affinché i profili possano essere inclusi nell’azione disciplinata da questo criterio."

Sotto **[!UICONTROL Then]** , seleziona almeno un attributo di consenso dallo schema di unione. Questo è l’attributo che deve essere presente affinché i profili possano essere inclusi nell’azione disciplinata da questo criterio. Puoi scegliere una delle opzioni fornite dall’elenco, oppure seleziona **[!UICONTROL Visualizza tutto]** per scegliere l’attributo direttamente dallo schema di unione.

Quando selezioni l’attributo di consenso, scegli i valori per l’attributo che desideri che venga verificato da questo criterio.

![](../images/policies/select-schema-field.png)

Dopo aver selezionato almeno un attributo di consenso, il **[!UICONTROL Proprietà dei criteri]** il pannello viene aggiornato per mostrare la stima del numero di profili consentiti in base a questo criterio, inclusa la percentuale dell’archivio profili totale. Questa stima viene aggiornata automaticamente quando si regola la configurazione dei criteri.

![](../images/policies/audience-preview.png)

Per aggiungere altri attributi di consenso al criterio, seleziona **[!UICONTROL Aggiungi risultato]**.

![](../images/policies/add-result.png)

Puoi continuare ad aggiungere e modificare le condizioni e gli attributi di consenso al criterio in base alle esigenze. Quando la configurazione è soddisfacente, fornisci un nome e una descrizione facoltativa per il criterio prima di selezionare **[!UICONTROL Salva]**.

![](../images/policies/name-and-save.png)

Il criterio di consenso viene ora creato e il suo stato è impostato su [!UICONTROL Disabilitato] per impostazione predefinita. Per abilitare subito il criterio, seleziona la **[!UICONTROL Stato]** attiva la barra a destra.

![](../images/policies/enable-consent-policy.png)

#### Verificare l’applicazione dei criteri

Dopo aver creato e abilitato un criterio di consenso, puoi visualizzare in anteprima come questo influisce sui tipi di pubblico consentiti quando attivi i segmenti nelle destinazioni. Consulta la sezione su [valutazione dei criteri di consenso](../enforcement/auto-enforcement.md#consent-policy-evaluation) per ulteriori informazioni.

## Abilitare o disabilitare un criterio {#enable}

Tutti i criteri di utilizzo dei dati (inclusi i criteri principali forniti da Adobe) sono disabilitati per impostazione predefinita. Affinché un singolo criterio possa essere preso in considerazione per l’applicazione, devi abilitarlo manualmente tramite l’API o l’interfaccia utente.

È possibile abilitare o disabilitare i criteri da **[!UICONTROL Sfoglia]** scheda in **[!UICONTROL Criteri]** Workspace. Seleziona un criterio personalizzato dall’elenco per visualizzarne i dettagli a destra. Sotto **[!UICONTROL Stato]**, seleziona il pulsante di attivazione/disattivazione per abilitare o disabilitare il criterio.

![](../images/policies/enable-policy.png)

## Visualizzare le azioni di marketing {#view-marketing-actions}

In **[!UICONTROL Criteri]** Workspace, seleziona la **[!UICONTROL Azioni di marketing]** per visualizzare un elenco delle azioni di marketing disponibili definite da Adobe e dalla tua organizzazione.

![](../images/policies/marketing-actions.png)

## Creare un’azione di marketing {#create-marketing-action}

Per creare una nuova azione di marketing personalizzata, seleziona **[!UICONTROL Crea azione di marketing]** nell&#39;angolo in alto a destra del **[!UICONTROL Azioni di marketing]** scheda in **[!UICONTROL Criteri]** Workspace.

![](../images/policies/create-marketing-action.png)

Il **[!UICONTROL Crea azione di marketing]** viene visualizzata. Immetti un nome e una descrizione per l’azione di marketing, quindi seleziona **[!UICONTROL Crea]**.

![](../images/policies/create-marketing-action-details.png)

L’azione appena creata viene visualizzata nella **[!UICONTROL Azioni di marketing]** scheda. Ora puoi utilizzare l’azione di marketing quando [creazione di nuovi criteri di utilizzo dati](#create-policy).

![](../images/policies/created-marketing-action.png)

## Modificare o eliminare un’azione di marketing {#edit-delete-marketing-action}

>[!NOTE]
>
>È possibile modificare solo le azioni di marketing personalizzate definite dall’organizzazione. Le azioni di marketing definite dall’Adobe non possono essere modificate o eliminate.

In **[!UICONTROL Criteri]** Workspace, seleziona la **[!UICONTROL Azioni di marketing]** per visualizzare un elenco delle azioni di marketing disponibili definite da Adobe e dalla tua organizzazione. Seleziona un’azione di marketing personalizzata dall’elenco, quindi utilizza i campi forniti nella sezione di destra per modificarne i dettagli.

![](../images/policies/edit-marketing-action.png)

Se l’azione di marketing non è utilizzata da alcun criterio di utilizzo esistente, puoi eliminarla selezionando **[!UICONTROL Elimina azione di marketing]**.

>[!NOTE]
>
>Se si tenta di eliminare un’azione di marketing utilizzata da un criterio esistente, viene visualizzato un messaggio di errore a indicare che il tentativo di eliminazione non è riuscito.

![](../images/policies/delete-marketing-action.png)

## Passaggi successivi

Questo documento fornisce una panoramica su come gestire i criteri di utilizzo dei dati in [!DNL Experience Platform] UI. Per i passaggi su come gestire i criteri utilizzando [!DNL Policy Service API], vedere [guida per sviluppatori](../api/getting-started.md). Per informazioni su come applicare i criteri di utilizzo dei dati, vedi [panoramica sull’applicazione dei criteri](../enforcement/overview.md).

Il video seguente illustra come utilizzare i criteri di utilizzo in [!DNL Experience Platform] Interfaccia utente:

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)
