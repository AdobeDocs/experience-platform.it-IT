---
keywords: Experience Platform;home;argomenti popolari;governance dei dati;etichetta utilizzo dati;servizio criteri;guida utente etichette utilizzo dati
solution: Experience Platform
title: Gestire le etichette di utilizzo dei dati nell’interfaccia utente
description: Questa guida descrive i passaggi per lavorare con le etichette di utilizzo dei dati nell’interfaccia utente di Adobe Experience Platform.
exl-id: aa44d5cc-416a-4ef2-be14-b4f32aec162c
source-git-commit: e539b1e165227d9a888bfe12d8205e285b3ce259
workflow-type: tm+mt
source-wordcount: '1308'
ht-degree: 0%

---

# Gestire le etichette di utilizzo dei dati nell’interfaccia utente {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataGovernance_description"
>title="Descrizione"
>abstract=""

Questa guida utente descrive i passaggi per lavorare con le etichette di utilizzo dei dati in [!DNL Experience Platform] dell&#39;utente.

## Gestire le etichette a livello di set di dati

>[!IMPORTANT]
>
>L’applicazione di etichette a livello di set di dati è supportata solo per i casi di utilizzo di governance dei dati. Se si desidera creare criteri di accesso per i dati, è necessario [applica etichette allo schema](../../xdm/tutorials/labels.md) su cui si basa il set di dati. Consulta la panoramica su [controllo degli accessi basato su attributi](../../access-control/abac/overview.md) per ulteriori informazioni.

Per gestire le etichette di utilizzo dei dati a livello di set di dati, è necessario selezionare un set di dati esistente o crearne uno nuovo. Dopo aver effettuato l’accesso a Adobe Experience Platform, seleziona **[!UICONTROL Set di dati]** nella barra di navigazione a sinistra per aprire **[!UICONTROL Set di dati]** Workspace. Questa pagina elenca tutti i set di dati creati appartenenti alla tua organizzazione, insieme a dettagli utili relativi a ciascun set di dati.

![Scheda Set di dati nell’area di lavoro dati](../images/labels/datasets-tab.png)

La sezione successiva descrive i passaggi necessari per creare un nuovo set di dati a cui applicare le etichette. Se desideri modificare le etichette per un set di dati esistente, seleziona il set di dati dall’elenco e passa a [aggiunta di etichette di utilizzo dati al set di dati](#add-labels).

### Creare un nuovo set di dati

>[!NOTE]
>
>In questo esempio, un set di dati viene creato utilizzando un [!DNL Experience Data Model] (XDM). Per ulteriori informazioni sugli schemi XDM, vedi [Panoramica del sistema XDM](../../xdm/home.md) e [nozioni di base sulla composizione dello schema](../../xdm/schema/composition.md).

Per creare un nuovo set di dati, seleziona **[!UICONTROL Crea set di dati]** nell&#39;angolo in alto a destra del **[!UICONTROL Set di dati]** Workspace.

![](../images/labels/create-dataset.png)

Il **[!UICONTROL Crea set di dati]** viene visualizzata la schermata. Da qui, seleziona **[!UICONTROL Crea set di dati dallo schema]**.

![Crea set di dati dallo schema](../images/labels/create-from-dataset.png)

Il **[!UICONTROL Seleziona schema]** viene visualizzata una schermata che elenca tutti gli schemi disponibili che è possibile utilizzare per creare un set di dati. Seleziona il pulsante di opzione accanto a uno schema per selezionarlo. Il **[!UICONTROL Schemi]** sul lato destro mostra ulteriori dettagli sullo schema selezionato. Dopo aver selezionato uno schema, seleziona **[!UICONTROL Successivo]**.

![Seleziona schema set di dati](../images/labels/select-schema.png)

Il **[!UICONTROL Configurare il set di dati]** viene visualizzata la schermata. Specifica un nome (obbligatorio) e una descrizione (facoltativa ma consigliata) per il nuovo set di dati, quindi seleziona **[!UICONTROL Fine]**.

![Configurare il set di dati con nome e descrizione](../images/labels/configure-dataset.png)

Il **[!UICONTROL Attività set di dati]** viene visualizzata una pagina contenente informazioni sul set di dati appena creato. In questo esempio, il set di dati è denominato &quot;Membri fedeltà&quot;, pertanto la navigazione superiore mostra **Set di dati > Membri fedeltà**.

![Pagina Attività set di dati](../images/labels/dataset-created.png)

### Aggiungere etichette di utilizzo dati al set di dati {#add-labels}

Dopo aver creato un nuovo set di dati o selezionato un set di dati esistente dall’elenco in **[!UICONTROL Set di dati]** workspace, seleziona **[!UICONTROL Governance dei dati]** per aprire **[!UICONTROL Governance dei dati]** Workspace. L’area di lavoro ti consente di gestire le etichette di utilizzo dei dati a livello di set di dati e di campo.

![Scheda Governance dei dati del set di dati](../images/labels/dataset-governance.png)

Per modificare le etichette di utilizzo dei dati a livello di set di dati, inizia selezionando l’icona a forma di matita accanto al nome del set di dati.

![Modificare le etichette a livello di set di dati](../images/labels/dataset-level-edit.png)

Il **[!UICONTROL Modifica etichette di governance]** viene visualizzata una finestra di dialogo. Nella finestra di dialogo, seleziona le caselle accanto alle etichette da applicare al set di dati. Ricorda che queste etichette verranno ereditate da tutti i campi all’interno del set di dati. Il **[!UICONTROL Etichette applicate]** l’intestazione viene aggiornata quando selezioni ogni casella, mostrando le etichette scelte. Dopo aver selezionato le etichette desiderate, seleziona **[!UICONTROL Salva modifiche]**.

![Applicare le etichette di governance a livello di set di dati](../images/labels/apply-labels-dataset.png)

Il **[!UICONTROL Governance dei dati]** viene nuovamente visualizzato l’area di lavoro, con le etichette applicate a livello di set di dati. Puoi anche vedere che le etichette vengono ereditate fino a ciascuno dei campi all’interno del set di dati.

![Etichette del set di dati ereditate dai campi](../images/labels/dataset-labels-applied.png)

Accanto alle etichette a livello di set di dati viene visualizzata una &quot;x&quot; che consente di rimuovere le etichette. Le etichette ereditate accanto a ciascun campo non hanno una &quot;x&quot; accanto e appaiono &quot;disattivate&quot; senza possibilità di rimozione o modifica. Questo perché **i campi ereditati sono di sola lettura**, il che significa che non possono essere rimossi a livello di campo.

Il **[!UICONTROL Mostra etichette ereditate]** l’opzione è attivata per impostazione predefinita, consente di visualizzare tutte le etichette ereditate dal set di dati ai relativi campi. Se si disattiva l’opzione, vengono nascoste tutte le etichette ereditate all’interno del set di dati.

![Nascondi etichette ereditate](../images/labels/inherited-labels.png)

## Gestire le etichette a livello di campo del set di dati {#manage-labels-at-dataset-field-level}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataGovernance_instructions"
>title="Istruzioni"
>abstract=""

>[!IMPORTANT]
>
>L’applicazione di etichette a livello di campo del set di dati è supportata solo per i casi di utilizzo di governance dei dati. Se si desidera creare criteri di accesso per i dati, è necessario [applica etichette allo schema](../../xdm/tutorials/labels.md) su cui si basa il set di dati. Consulta la panoramica su [controllo degli accessi basato su attributi](../../access-control/abac/overview.md) per ulteriori informazioni.

Continuazione del flusso di lavoro per [aggiunta e modifica di etichette di utilizzo dei dati a livello di set di dati](#add-labels), è inoltre possibile gestire le etichette a livello di campo all&#39;interno del **[!UICONTROL Governance dei dati]** dell’area di lavoro per quel set di dati.

Per applicare le etichette di utilizzo dei dati a un singolo campo, seleziona la casella di controllo accanto al nome del campo, quindi seleziona **[!UICONTROL Modifica etichette di governance]**.

![Modifica etichette campi](../images/labels/field-label-edit.png)

Il **[!UICONTROL Modifica etichette di governance]** viene visualizzata. La finestra di dialogo visualizza le intestazioni che mostrano i campi selezionati, le etichette applicate e le etichette ereditate. Le etichette ereditate (C2 e C5) sono disattivate nella finestra di dialogo. Sono etichette di sola lettura ereditate dal livello del set di dati e sono quindi modificabili solo a livello di set di dati.

![Modificare le etichette di governance per un singolo campo](../images/labels/field-label-inheritance.png)

Seleziona le etichette a livello di campo selezionando la casella di controllo accanto a ogni etichetta che desideri utilizzare. Quando si selezionano le etichette, **[!UICONTROL Etichette applicate]** l’intestazione viene aggiornata per mostrare le etichette applicate ai campi mostrati nella **[!UICONTROL Campi selezionati]** intestazione. Dopo aver selezionato le etichette a livello di campo, seleziona **[!UICONTROL Salva modifiche]**.

![Applica etichette a livello di campo](../images/labels/apply-labels-field.png)

Il **[!UICONTROL Governance dei dati]** workspace, che ora visualizza le etichette a livello di campo selezionate nella riga accanto al nome del campo. L’etichetta a livello di campo è affiancata da una &quot;x&quot;, che consente di rimuoverla.

![Campo che mostra le etichette a livello di campo](../images/labels/field-labels-applied.png)

È possibile ripetere questi passaggi per continuare ad aggiungere e modificare etichette a livello di campo per campi aggiuntivi, inclusa la selezione di più campi per applicare etichette a livello di campo contemporaneamente.

![Selezionare più campi per applicare le etichette a livello di campo contemporaneamente.](../images/labels/multiple-fields.png)

È importante ricordare che l’ereditarietà si sposta solo dal livello superiore verso il basso (campi di → di set di dati), il che significa che le etichette applicate a livello di campo non vengono propagate ad altri campi o set di dati.

## Gestire le etichette a livello di schema

Puoi aggiungere etichette direttamente a uno schema o a campi all’interno di tale schema. Tutti i campi applicati a livello di schema verranno propagati a tutti i set di dati basati su tale schema.

Guarda il tutorial su [gestione delle etichette a livello di schema](../../xdm/tutorials/labels.md) per ulteriori informazioni.

## Gestire le etichette personalizzate {#manage-custom-labels}

>[!CONTEXTUALHELP]
>id="platform_governance_createlabels"
>title="Create labels (Creare etichette)"
>abstract="Le etichette consentono di categorizzare set di dati e campi in base ai criteri di utilizzo applicabili a tali dati. Platform fornisce un set standard di etichette da utilizzare, ma puoi anche creare etichette personalizzate specifiche per la tua organizzazione."

Puoi creare etichette di utilizzo personalizzate all&#39;interno del **[!UICONTROL Criteri]** area di lavoro in [!DNL Experience Platform] UI. Seleziona **[!UICONTROL Criteri]** nel menu di navigazione a sinistra, quindi seleziona **[!UICONTROL Etichette]** per visualizzare un elenco di etichette esistenti. Da qui, seleziona **[!UICONTROL Crea etichetta]**.

![](../images/labels/create-label-btn.png)

Il **[!UICONTROL Crea etichetta]** viene visualizzata. Da qui, fornisci le seguenti informazioni per la nuova etichetta:

* **[!UICONTROL Identificatore]**: identificatore univoco dell’etichetta. Questo valore viene utilizzato a scopo di ricerca e deve quindi essere breve e conciso.
* **[!UICONTROL Nome]**: nome visualizzato descrittivo per l’etichetta.
* **[!UICONTROL Descrizione]**: (facoltativo) descrizione dell’etichetta per fornire ulteriore contesto.

Al termine, seleziona **[!UICONTROL Crea]**.

![](../images/labels/create-label.png)

La finestra di dialogo si chiude e l’etichetta personalizzata appena creata viene visualizzata nell’elenco sotto **[!UICONTROL Etichette]** scheda.

![](../images/labels/label-created.png)

L’etichetta ora può essere selezionata in **[!UICONTROL Etichette personalizzate]** durante la modifica delle etichette di utilizzo per set di dati e campi o durante la creazione di criteri di utilizzo dei dati.

<img src="../images/labels/add-custom-label.png" width="600" /><br>

## Passaggi successivi

Ora che hai aggiunto le etichette di utilizzo dei dati a livello di set di dati e di campo, puoi iniziare ad acquisire i dati in [!DNL Experience Platform]. Per ulteriori informazioni, consulta la sezione [documentazione sull’acquisizione dei dati](../../ingestion/home.md).

Ora puoi anche definire i criteri di utilizzo dei dati in base alle etichette applicate. Per ulteriori informazioni, vedere [panoramica dei criteri di utilizzo dei dati](../policies/overview.md).

## Risorse aggiuntive

Il video seguente ha lo scopo di aiutarti a comprendere la governance dei dati e illustra come applicare le etichette a un set di dati e ai singoli campi.

>[!VIDEO](https://video.tv.adobe.com/v/29709?quality=12&enable10seconds=on&speedcontrol=on)
