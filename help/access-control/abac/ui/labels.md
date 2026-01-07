---
keywords: Experience Platform;home;argomenti popolari;controllo degli accessi;controllo degli accessi basato su attributi
title: Etichette di gestione del controllo dell'accesso basate su attributi
description: Gestisci le etichette tramite l’interfaccia Autorizzazioni in Adobe Experience Cloud.
exl-id: c790f09c-fda6-48bf-95db-3f5053cd882e
source-git-commit: 855f0a1384f658d39aa9d4fbb6bcb032933e59db
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 11%

---

# Gestire le etichette

È possibile utilizzare le etichette per categorizzare i set di dati e i campi in base all’utilizzo dei dati e ai criteri di controllo dell’accesso basati su attributi. Le etichette possono essere applicate in qualsiasi momento, offrendo flessibilità nella scelta di come gestire i dati. Le best practice incoraggiano i dati di etichettatura non appena vengono acquisiti in Adobe Experience Platform o non appena i dati diventano disponibili per l’uso. Leggi questo documento per scoprire come gestire le etichette nell’interfaccia utente Autorizzazioni.

Per un elenco completo delle etichette e dei criteri di governance corrispondenti, leggere la guida su [etichette di utilizzo dei dati di base](../../../data-governance/labels/reference.md){target="_blank"}.

>[!NOTE]
>
>Per creare o visualizzare [attributi calcolati](../../../profile/computed-attributes/overview.md){target="_blank"} con campi contenenti una determinata etichetta, è necessario avere accesso a tale etichetta.

## Esplora etichette {#explore-labels}

Per visualizzare tutte le etichette disponibili, passa a **[!UICONTROL Permissions]** in [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"}. Seleziona **[!UICONTROL Labels]** dal pannello a sinistra.

![L&#39;area di lavoro etichette all&#39;interno di Autorizzazioni con etichette evidenziate nel pannello sinistro.](../../images/ui/labels/labels-home.png){zoomable="yes"}

Le etichette sono suddivise per tipo e appartengono a una delle seguenti categorie:

| Tipo | Descrizione |
| --- | --- |
| [Contratto](../../../data-governance/labels/reference.md#contract){target="_blank"} | Questa categoria viene utilizzata per categorizzare i dati che hanno obblighi contrattuali o sono relativi ai criteri di governance dei dati della tua organizzazione. |
| [Identità](../../../data-governance/labels/reference.md#identity){target="_blank"} | Questa categoria viene utilizzata per categorizzare i dati che possono identificare direttamente o indirettamente una persona. |
| [Sensibile](../../../data-governance/labels/reference.md#sensitive){target="_blank"} | Questa categoria viene utilizzata per categorizzare i dati considerati sensibili dalla tua organizzazione. |
| [Ecosistema partner](../../../data-governance/labels/reference.md#partner){target="_blank"} | Questa categoria viene utilizzata per categorizzare i dati ottenuti da origini esterne all’organizzazione. |
| Coinvolgimento responsabile | Questa categoria contiene un&#39;etichetta singola, **[!UICONTROL Potential for Bias]**, che riflette i dati che potrebbero introdurre distorsioni. |
| Personalizzato | Questa categoria include le etichette create dall’organizzazione. |

Per filtrare le etichette, selezionare l&#39;icona del filtro (![icona filtro](/help/images/icons/filter.png)), quindi selezionare il tipo di etichetta desiderato dal menu a discesa **[!UICONTROL Type]**.

![L&#39;area di lavoro delle etichette con l&#39;opzione filtro espansa e l&#39;elenco a discesa dei tipi evidenziato.](../../images/ui/labels/label-filter.png){zoomable="yes"}

Per visualizzare una singola etichetta, selezionarne il nome dall&#39;elenco. Viene visualizzata la pagina dei dettagli dell’etichetta. Le etichette di base di Adobe sono **non** modificabili.

![Pagina dei dettagli di una singola etichetta.](../../images/ui/labels/label-details.png){zoomable="yes"}

## Creare un’etichetta personalizzata {#create-custom-label}

>[!CONTEXTUALHELP]
>id="platform_abac_labelusage"
>title="Utilizzo delle etichette"
>abstract="Puoi utilizzare etichette personalizzate per applicare ai dati configurazioni di governance dei dati e di controllo degli accessi."

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about_create"
>title="Creare una nuova etichetta"
>abstract="Puoi creare etichette personalizzate per adattarle alle esigenze della tua organizzazione. Le etichette personalizzate possono essere utilizzate per applicare ai dati sia le configurazioni di governance dei dati che di controllo degli accessi."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=it#manage-labels" text="Gestire le etichette personalizzate"

>[!NOTE]
>
>Per creare un&#39;etichetta personalizzata, è necessario un ruolo contenente le autorizzazioni **[!UICONTROL Manage Usage Labels]** e la sandbox `Prod`.

Per creare una nuova etichetta, selezionare **[!UICONTROL Labels]** dal pannello sinistro dell&#39;area di lavoro **[!UICONTROL Permissions]**, quindi selezionare **[!UICONTROL Create label]**.

![Area di lavoro etichette con l&#39;opzione Crea etichetta evidenziata.](../../images/ui/labels/create-label.png){zoomable="yes"}

Viene visualizzata la finestra di dialogo **[!UICONTROL Create new label]** in cui viene richiesto di immettere **[!UICONTROL Name]**, **[!UICONTROL Friendly name]** e **[!UICONTROL Description]**.

>[!IMPORTANT]
>
> Impossibile modificare l&#39;etichetta [!UICONTROL Name] dopo la creazione e l&#39;eliminazione dell&#39;etichetta non è attualmente supportata.

Seleziona **[!UICONTROL Confirm]** per completare la creazione dell&#39;etichetta.

![La finestra di dialogo Crea nuova etichetta con Nome, Nome descrittivo e Descrizione è stata compilata ed è stata evidenziata l&#39;opzione Conferma.](../../images/ui/labels/create-new-label.png){zoomable="yes"}

## Modificare un’etichetta personalizzata {#edit-custom-label}

Sebbene non sia possibile modificare l&#39;etichetta personalizzata **[!UICONTROL Name]**, è possibile modificare **[!UICONTROL Friendly name]** e **[!UICONTROL Description]**. Per modificare un&#39;etichetta personalizzata, selezionarla dall&#39;elenco nell&#39;area di lavoro **[!UICONTROL Labels]**.

![Area di lavoro etichette con l&#39;etichetta evidenziata.](../../images/ui/labels/select-label.png){zoomable="yes"}

Modificare uno dei campi e quindi fare clic in un punto qualsiasi all&#39;esterno della casella di testo per salvare le modifiche. Sullo schermo verrà visualizzato un messaggio di conferma e il nome **[!UICONTROL Modified by]** e la data **[!UICONTROL Modified]** cambieranno.

![Visualizzazione della pagina dei dettagli dell&#39;etichetta con il messaggio &quot;aggiornato correttamente&quot;.](../../images/ui/labels/edit-label.png){zoomable="yes"}

## Passaggi successivi

Ora che conosci meglio le etichette, puoi iniziare a [applicarle agli schemi](../../../xdm/tutorials/labels.md).
