---
keywords: Experience Platform;home;argomenti popolari;governance dei dati;etichetta utilizzo dati;servizio criteri;guida utente etichette utilizzo dati
solution: Experience Platform
title: Gestire le etichette di utilizzo dei dati nell’interfaccia utente
description: Questa guida descrive i passaggi per lavorare con le etichette di utilizzo dei dati nell’interfaccia utente di Adobe Experience Platform.
exl-id: aa44d5cc-416a-4ef2-be14-b4f32aec162c
source-git-commit: c1722c59c437215ce578a1a44cf0cad3b03ceca9
workflow-type: tm+mt
source-wordcount: '1549'
ht-degree: 17%

---

# Gestire le etichette di utilizzo dei dati nell’interfaccia utente {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataGovernance_description"
>title="Gestire l’utilizzo dei dati in Platform"
>abstract="<h2>Descrizione</h2><p>Il framework della governance dei dati in Experience Platform consente di etichettare gli attributi e i set di dati in base alle restrizioni di utilizzo dei dati e di impostare criteri che identifichino e rispettino tali restrizioni per azioni di marketing specifiche.</p>"

Questa guida utente descrive i passaggi per l&#39;utilizzo delle etichette di utilizzo dei dati nell&#39;interfaccia utente [!DNL Experience Platform].

## Gestisci etichette {#manage-labels}

Per applicare le etichette ai dati, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Gestisci etichette di utilizzo]** per l&#39;utilizzo nella sandbox di produzione predefinita denominata &quot;prod&quot;. Per creare un’etichetta personalizzata, devi anche disporre di diritti di amministrazione sul profilo del prodotto. Ogni organizzazione dispone di un solo elenco di etichette applicabili. **impossibile** eliminare le etichette. È invece possibile rimuoverli dai set di dati o dai campi a cui sono applicati.

Per ulteriori informazioni su come assegnare un&#39;autorizzazione, vedere la guida su come [configurare le autorizzazioni](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html) o la [panoramica sul controllo degli accessi](../../access-control/home.md). Se non hai accesso all’Admin Console per la tua organizzazione, contatta l’amministratore della tua organizzazione.

## Gestire le etichette a livello di schema

Puoi aggiungere etichette direttamente a uno schema o a campi all’interno di tale schema. Tutti i campi applicati a livello di schema verranno propagati a tutti i set di dati basati su tale schema.

>[!NOTE]
>
>Se i criteri di utilizzo dei dati sono stati creati prima dell’assegnazione dell’etichetta al campo, è possibile che venga visualizzata una finestra di dialogo per la violazione dei criteri di governance quando si applicano le etichette al nuovo schema. Questa finestra di dialogo indica che l’applicazione di questa etichetta violerà un criterio di utilizzo esistente. Utilizza il diagramma di derivazione dati per capire quali altre modifiche di configurazione devono essere apportate prima di poter aggiungere l’etichetta al campo schema.
>
>![La violazione dei criteri di governance dei dati ha rilevato una finestra di dialogo con il riepilogo delle violazioni e il diagramma di derivazione dei dati evidenziati.](../images/labels/policy-violation-dialog.png)
>
>Per ulteriori informazioni sulle violazioni parziali dei criteri, consulta la [documentazione sulle violazioni dei criteri di utilizzo dei dati](../enforcement/auto-enforcement.md#data-usage-violation).

Per gestire le etichette di utilizzo dei dati a livello di schema, è necessario selezionare uno schema esistente o crearne uno nuovo. Dopo aver effettuato l&#39;accesso a Adobe Experience Platform, seleziona **[!UICONTROL Schemi]** nel menu di navigazione a sinistra per aprire l&#39;area di lavoro **[!UICONTROL Schemi]**. Questa pagina elenca tutti gli schemi creati appartenenti alla tua organizzazione, insieme a dettagli utili relativi a ciascuno schema.

![Interfaccia utente di Adobe Experience Platform con la scheda Schema evidenziata.](../images/labels/schema-tab.png)

La sezione successiva descrive i passaggi necessari per creare un nuovo schema a cui applicare le etichette. Se desideri modificare le etichette per uno schema esistente, seleziona lo schema dall&#39;elenco e passa a [aggiunta di etichette di utilizzo dati allo schema](#add-labels).

### Crea un nuovo schema

Per creare un nuovo schema, seleziona **[!UICONTROL Crea schema]** nell&#39;angolo superiore destro dell&#39;area di lavoro **[!UICONTROL Schemi]**. Per istruzioni complete, consulta la guida su [come creare uno schema utilizzando l&#39;Editor di schema](../../xdm/tutorials/create-schema-ui.md#create). In alternativa, è possibile [creare uno schema utilizzando lo Schema Registry API](../../xdm/tutorials/create-schema-api.md), se necessario.

### Aggiungere etichette di utilizzo dati a uno schema {#add-labels-to-schema}

Dopo aver creato un nuovo schema o aver selezionato uno schema esistente dall&#39;elenco nella scheda [!UICONTROL Sfoglia] dell&#39;area di lavoro [!UICONTROL Schemi], selezionare un campo dallo schema nell&#39;Editor schema. Nella barra laterale [!UICONTROL Proprietà campo], seleziona **[!UICONTROL Applica etichette di accesso e governance dei dati]**.

![La scheda Struttura dell&#39;area di lavoro Schemi visualizza la visualizzazione dello schema con le etichette Applica accesso e Governance dei dati evidenziate.](../images/labels/schema-label-governance.png)

Viene visualizzata una finestra di dialogo che consente di applicare e gestire le etichette di utilizzo dei dati a livello di schema e di campo. Consulta il tutorial XDM per istruzioni complete su [come aggiungere o modificare le etichette di utilizzo dei dati per gli schemi XDM](../../xdm/tutorials/labels.md#select-schema-field).

### Aggiungere etichette di utilizzo dei dati a un set di dati specifico {#add-labels-to-dataset}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataGovernance_instructions"
>title="Istruzioni"
>abstract="<ol><li>Seleziona <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/user-guide.html?lang=it">Set di dati</a> nella barra di navigazione a sinistra, quindi seleziona il set di dati a cui desideri imporre limitazioni.</li><li>Dalla visualizzazione dei dettagli del set di dati, seleziona la scheda <b>Governance dei dati</b>.</li><li>Seleziona i campi del set di dati che desideri limitare, quindi seleziona <b>Modifica etichette di governance</b> per etichettare i dati in base a restrizioni di utilizzo.</li><li>Dopo aver etichettato i dati, seleziona <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html?lang=it">Criteri</a> nella barra di navigazione a sinistra, quindi seleziona <b>Crea criterio</b>.</li><li>Scegli di creare un <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html?lang=it#create-governance-policy">Criterio di governance dei dati</a>, quindi seleziona le etichette di utilizzo dei dati applicabili al criterio.</li><li>Seleziona le azioni di marketing che il criterio dovrà rifiuterà per i dati contenenti tali etichette. Dopo aver creato il criterio, selezionalo dall’elenco e abilitalo utilizzando l’interruttore nella barra a destra.</li><li>Per ogni criterio abilitato, Platform impedisce che i dati contenenti le etichette specificate possano essere utilizzati nelle azioni di marketing definite. Questo viene eseguito automaticamente quando si tenta di attivare i dati con la relativa etichetta in una destinazione a cui sono associate le specifiche azioni di marketing (casi d’uso).</li></ol>"

>[!IMPORTANT]
>
>Le etichette non possono più essere applicate ai campi a livello di set di dati. Questo flusso di lavoro è stato dichiarato obsoleto a favore dell’applicazione di etichette a livello di schema. Eventuali etichette applicate in precedenza a livello di oggetto del set di dati continueranno a essere supportate tramite l’interfaccia utente di Platform fino al 31 maggio 2024. Per garantire che le etichette siano coerenti in tutti gli schemi, tutte le etichette precedentemente associate ai campi a livello di set di dati devono essere migrate a livello di schema da te nel corso dell’anno successivo. Consulta la documentazione per le istruzioni su [come migrare le etichette applicate in precedenza dal set di dati al livello dello schema](../e2e.md#migrate-labels).

Le etichette possono essere applicate all&#39;intero set di dati dalla scheda **[!UICONTROL Governance dei dati]** dell&#39;area di lavoro **[!UICONTROL Set di dati]**. L’area di lavoro ti consente di gestire le etichette di utilizzo dei dati a livello di set di dati.

![Scheda [!UICONTROL Governance dei dati] dell&#39;area di lavoro [!UICONTROL Set di dati] con governance dei dati evidenziata.](../images/labels/dataset-governance.png)

Per modificare le etichette di utilizzo dei dati a livello di set di dati, iniziare selezionando l&#39;icona della matita (![Un&#39;icona della matita.](/help/images/icons/edit.png)) nella riga del nome del set di dati.

![Scheda [!UICONTROL Governance dei dati] dell&#39;area di lavoro [!UICONTROL Set di dati] con l&#39;icona Modifica matita evidenziata.](../images/labels/dataset-level-edit.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Modifica etichette di governance]**. Nella finestra di dialogo, seleziona le caselle accanto alle etichette da applicare al set di dati. Ricorda che queste etichette verranno ereditate da tutti i campi all’interno del set di dati. L&#39;intestazione **[!UICONTROL Etichette applicate]** viene aggiornata quando si seleziona ogni casella, mostrando le etichette scelte. Dopo aver selezionato le etichette desiderate, seleziona **[!UICONTROL Salva modifiche]**.

![La finestra di dialogo Modifica etichette di governance con le caselle di controllo delle etichette e Salva modifiche evidenziate.](../images/labels/apply-labels-dataset.png)

L&#39;area di lavoro **[!UICONTROL Governance dei dati]** viene nuovamente visualizzata, con le etichette applicate a livello di set di dati nella riga iniziale della tabella. Puoi anche vedere le etichette, indicate da singole schede, che vengono ereditate fino a ciascuno dei campi all’interno del set di dati.

![Scheda [!UICONTROL Governance dei dati] dell&#39;area di lavoro [!UICONTROL Set di dati] con etichette a livello di set di dati applicate ed etichette dei campi del set di dati ereditate evidenziate.](../images/labels/applied-dataset-labels.png)

### Rimuovere le etichette da un set di dati {#remove-labels-from-a-dataset}

Le etichette aggiunte a livello di set di dati presentano una &quot;x&quot; accanto alla scheda. Questo consente di rimuovere le etichette dall’intero set di dati. Le etichette ereditate accanto a ciascun campo non hanno una &quot;x&quot; accanto e appaiono &quot;disattivate&quot;. Queste **etichette ereditate sono di sola lettura**, ovvero non possono essere rimosse o modificate a livello di campo.

<!-- ## View labels at the dataset field level {#view-labels-at-dataset-field-level} -->

<!-- To view labels inherited by the dataset from the schema level, select **[!UICONTROL Datasets]** to navigate to the datasets workspace and select the relevant dataset from the list. 

![The Browse tab of the Datasets workspace with Datasets highlighted in the left sidebar.](../images/labels/dataset-navigation.png)

Next, select the **[!UICONTROL Data Governance]** tab to show the labels that have been applied to the dataset. You can also see that the labels are inherited down to each of the fields within the dataset.

![Dataset Labels inherited by fields](../images/labels/dataset-labels-applied.png)

The inherited labels beside each field do not have an "x" next to them and appear "greyed out" with no ability to remove or edit. This is because **inherited fields are read-only**, meaning they cannot be removed at the field level. -->

<!--Beleive can cut above here  -->

L&#39;opzione **[!UICONTROL Mostra etichette ereditate]** è attivata per impostazione predefinita e consente di visualizzare tutte le etichette ereditate dallo schema nei relativi campi. Se si disattiva l’opzione, vengono nascoste tutte le etichette ereditate all’interno del set di dati.

![Scheda Governance dei dati dell&#39;area di lavoro Set di dati con l&#39;opzione Mostra etichette ereditate evidenziata.](../images/labels/inherited-labels.png)

<!-- Labels applied to the dataset appear in read-only form within the **[!UICONTROL Data Governance]** view for that dataset. 

![The Data Governance tab of the Datasets workspace with labels highlighted.](../images/labels/read-only-governance-labels.png) -->

>[!NOTE]
>
>Le etichette applicate prima che la funzione di etichettatura del set di dati diventasse obsoleta possono essere rimosse dal set di dati individuando il set di dati pertinente e selezionando l’icona Annulla sull’etichetta.
>![Scheda Governance dei dati dell&#39;area di lavoro Set di dati con un&#39;etichetta eliminabile evidenziata.](../images/labels/remove-governance-labels.png)
>Consulta la documentazione per le istruzioni su [come migrare le etichette applicate in precedenza dal set di dati al livello dello schema](../e2e.md#migrate-labels).

## Gestire le etichette personalizzate {#manage-custom-labels}

>[!CONTEXTUALHELP]
>id="platform_governance_createlabels"
>title="Create labels (Creare etichette)"
>abstract="Le etichette consentono di classificare set di dati e campi in base ai criteri di utilizzo applicati a tali dati. Platform fornisce un set standard di etichette da utilizzare, ma puoi anche creare etichette personalizzate specifiche per la tua organizzazione."

Puoi creare etichette di utilizzo personalizzate all&#39;interno dell&#39;area di lavoro **[!UICONTROL Criteri]** nell&#39;interfaccia utente [!DNL Experience Platform]. Seleziona **[!UICONTROL Criteri]** nell&#39;area di navigazione a sinistra, quindi seleziona **[!UICONTROL Etichette]** per visualizzare un elenco di etichette esistenti. Da qui, seleziona **[!UICONTROL Crea etichetta]**.

![Area di lavoro Criteri con criteri di creazione evidenziati.](../images/labels/create-label-btn.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Crea etichetta]**. Da qui, fornisci le seguenti informazioni per la nuova etichetta:

* **[!UICONTROL Nome]**: un identificatore univoco per l&#39;etichetta. Questo valore viene utilizzato a scopo di ricerca e deve quindi essere breve e conciso.
* **[!UICONTROL Nome descrittivo]**: un nome visualizzato descrittivo per l&#39;etichetta.
* **[!UICONTROL Descrizione]**: (facoltativo) una descrizione per l&#39;etichetta per fornire ulteriore contesto.

Al termine, selezionare **[!UICONTROL Crea]**.

![Area di lavoro Criteri Finestra di dialogo Crea etichetta con Crea evidenziato.](../images/labels/create-label-dialog.png)

La finestra di dialogo si chiude e l&#39;etichetta personalizzata appena creata viene visualizzata nell&#39;elenco nella scheda **[!UICONTROL Etichette]**.

![Scheda Etichette dell&#39;area di lavoro Criteri con la nuova etichetta personalizzata evidenziata.](../images/labels/label-created.png)

È ora possibile selezionare l&#39;etichetta in **[!UICONTROL Etichette personalizzate]** durante la modifica delle etichette di utilizzo per set di dati e campi o durante la creazione di criteri di utilizzo dei dati.

![Finestra di dialogo Applica etichette di accesso e governance dei dati con le etichette personalizzate evidenziate.](../images/labels/add-custom-label.png)

## Passaggi successivi

Dopo aver aggiunto le etichette di utilizzo dei dati a livello di set di dati e campo, puoi iniziare a acquisire dati in [!DNL Experience Platform]. Per ulteriori informazioni, consulta la [documentazione sull&#39;acquisizione dei dati](../../ingestion/home.md).

Ora puoi anche definire i criteri di utilizzo dei dati in base alle etichette applicate. Per ulteriori informazioni, vedere la [panoramica dei criteri di utilizzo dei dati](../policies/overview.md).

<!-- The workflow of this video is now outdated. This can be enabled once the video has been updated

## Additional resources

The following video is intended to support your understanding of Data Governance, and outlines how to apply labels to a dataset and individual fields.

>[!VIDEO](https://video.tv.adobe.com/v/29709?quality=12&enable10seconds=on&speedcontrol=on) -->
