---
solution: Experience Platform
title: Guida dell’interfaccia utente del servizio di segmentazione
description: Scopri come creare e gestire tipi di pubblico e definizioni di segmenti nell’interfaccia utente di Adobe Experience Platform.
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 1%

---

# Guida dell’interfaccia utente di Segmentation Service

[!DNL Adobe Experience Platform Segmentation Service] fornisce un&#39;interfaccia utente per la creazione e la gestione di tipi di pubblico e definizioni di segmenti.

## Introduzione

L&#39;utilizzo dei tipi di pubblico e delle definizioni dei segmenti richiede la comprensione dei vari servizi [!DNL Experience Platform] coinvolti nella segmentazione. Prima di leggere questa guida utente, consulta la documentazione dei seguenti servizi:

- [[!DNL Segmentation Service]](../home.md): [!DNL Segmentation Service] consente di segmentare in gruppi più piccoli i dati archiviati in [!DNL Experience Platform] relativi a singoli utenti (ad esempio clienti, potenziali clienti, utenti o organizzazioni).
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): consente la creazione di profili cliente collegando identità da origini dati diverse acquisite in [!DNL Platform].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): framework standardizzato tramite il quale [!DNL Platform] organizza i dati sull&#39;esperienza del cliente. Per utilizzare al meglio la segmentazione, assicurati che i dati vengano acquisiti come profili ed eventi in base alle [best practice per la modellazione dei dati](../../xdm/schema/best-practices.md).

Devi inoltre comprendere i seguenti termini chiave utilizzati in questo documento e la loro differenza:

- **Pubblico**: un insieme di persone che condividono comportamenti e/o caratteristiche simili. Questa raccolta di persone può essere generata da Adobe Experience Platform utilizzando le definizioni dei segmenti (pubblico generato da Platform), la composizione del pubblico o da fonti esterne, come caricamenti personalizzati (pubblico generato esternamente).
- **Definizione del segmento**: le regole utilizzate da Adobe Experience Platform per descrivere le caratteristiche o il comportamento chiave di un pubblico di destinazione.
- **Segmento**: azione di separazione dei profili in tipi di pubblico.

## Panoramica

Nell&#39;interfaccia utente di Experience Platform, seleziona **[!UICONTROL Tipi di pubblico]** nell&#39;area di navigazione a sinistra per aprire la scheda **[!UICONTROL Panoramica]** contenente la dashboard [!UICONTROL Tipi di pubblico].

>[!NOTE]
>
>Se la tua organizzazione ha poca esperienza con Platform e non dispone ancora di set di dati di profilo attivi o criteri di unione creati, la dashboard [!UICONTROL Tipi di pubblico] non è visibile. Nella scheda [!UICONTROL Panoramica] sono invece visualizzati collegamenti e documentazione per aiutarti a iniziare a utilizzare i tipi di pubblico.

### [!UICONTROL Tipi di pubblico] dashboard {#segments-dashboard}

La dashboard **[!UICONTROL Tipi di pubblico]** presenta le metriche chiave relative ai dati sul pubblico della tua organizzazione.

Per ulteriori informazioni, visita la [guida dashboard tipi di pubblico](../../dashboards/guides/audiences.md).

![Viene visualizzato il dashboard del pubblico. Mostra vari widget, tra cui la dimensione del pubblico, i profili per identità, la sovrapposizione delle identità e la tendenza di modifica della dimensione del pubblico.](../../dashboards/images/segments/dashboard-overview.png)

## Sfogliare {#browse}

Seleziona la scheda **[!UICONTROL Sfoglia]** per visualizzare il Portale pubblico. Audience Portal fornisce un elenco di tutti i tipi di pubblico che appartengono alla tua organizzazione e alla sandbox e include dettagli quali il conteggio dei profili, l’origine, la data di creazione, la data dell’ultima modifica, i tag e il raggruppamento.

Inoltre, Audience Portal consente di creare nuovi tipi di pubblico utilizzando Segment Builder (Generatore di segmenti) o Audience Composition (Composizione pubblico), nonché di importare in Platform tipi di pubblico generati esternamente.

Per ulteriori informazioni su Audience Portal, consulta la [panoramica di Audience Portal](./audience-portal.md).

## Composizioni {#compositions}

Seleziona la scheda **[!UICONTROL Composizioni]** per visualizzare un elenco di tutti i tipi di pubblico generati tramite la composizione del pubblico per la tua organizzazione.

![Elenco di tipi di pubblico creati in Composizione pubblico per la tua organizzazione.](../images/ui/overview/compositions.png)

Per impostazione predefinita, questa visualizzazione elenca informazioni sui tipi di pubblico, tra cui nome, stato, data di creazione, data di creazione, data dell’ultimo aggiornamento e data dell’ultimo aggiornamento di.

Accanto a ogni pubblico è presente un’icona con i puntini di sospensione. Selezionando questa opzione viene visualizzato un elenco delle azioni rapide disponibili per il pubblico.

| Azione | Descrizione |
| ------ | ----------- |
| Duplica | Copia il pubblico selezionato. |
| Gestisci accesso | Gestisce le etichette di accesso che appartengono al pubblico. Per ulteriori informazioni sulle etichette di accesso, consulta la documentazione su [gestione delle etichette](../../access-control/abac/ui/labels.md). |
| Elimina | Elimina il pubblico selezionato. I tipi di pubblico utilizzati nelle destinazioni a valle o dipendenti in altri tipi di pubblico **non possono** essere eliminati. Per ulteriori informazioni sull&#39;eliminazione del pubblico, leggere le [domande frequenti sulla segmentazione](../faq.md#lifecycle-states). |

È possibile selezionare l&#39;icona ![Personalizza tabella](/help/images/icons/column-settings.png) per modificare i campi visualizzati.

![Il pulsante Personalizza tabella è evidenziato. La selezione di questo pulsante consente di personalizzare i campi visualizzati nella pagina Composizioni pubblico.](../images/ui/overview/compositions-select-customize-table.png)

Viene visualizzato un popover che elenca tutti i campi che possono essere visualizzati nella tabella.

![Attributi che è possibile visualizzare per la sezione Composizione.](../images/ui/overview/compositions-customize-table.png)

| Campo | Descrizione |
| ----- | ----------- | 
| [!UICONTROL Nome] | Il nome del pubblico. |
| [!UICONTROL Stato] | Stato del pubblico. I valori possibili per questo campo includono `Draft`, `Inactive` e `Published`. |
| [!UICONTROL Creato] | L’ora e la data di creazione del pubblico. |
| [!UICONTROL Creato da] | Nome della persona che ha creato il pubblico. |
| [!UICONTROL Aggiornato] | Ora e data dell’ultimo aggiornamento del pubblico. |
| [!UICONTROL Aggiornato da] | Nome dell’ultima persona che ha aggiornato il pubblico. |

Per visualizzare la composizione del pubblico, seleziona il nome di un pubblico nella scheda [!UICONTROL Tipi di pubblico].

Viene visualizzata la pagina Composizione pubblico con i blocchi predefiniti che compongono il pubblico. Per ulteriori dettagli su come utilizzare la composizione del pubblico, consulta la [guida dell&#39;interfaccia utente per la composizione del pubblico](./audience-composition.md).

## Segmentazione in streaming {#streaming-segmentation}

La segmentazione in streaming consente di eseguire la segmentazione su [!DNL Platform] in tempo quasi reale, concentrandosi al contempo sulla ricchezza dei dati. Con la segmentazione in streaming, la qualificazione per la segmentazione ora avviene quando i dati arrivano in [!DNL Platform], riducendo la necessità di pianificare ed eseguire processi di segmentazione.

Ulteriori informazioni sulla segmentazione streaming sono disponibili nella [guida utente per la segmentazione streaming](./streaming-segmentation.md).

>[!NOTE]
>
>Affinché la segmentazione in streaming funzioni, devi abilitare la segmentazione pianificata per l’organizzazione. Per informazioni dettagliate sull&#39;abilitazione della segmentazione pianificata, consulta [la sezione segmentazione in streaming in questa guida utente](#scheduled-segmentation).

## Segmentazione Edge {#edge-segmentation}

La segmentazione di Edge è la capacità di valutare i tipi di pubblico in Platform istantaneamente al limite, abilitando casi di utilizzo di personalizzazione della stessa pagina e della pagina successiva.

Ulteriori informazioni sulla segmentazione Edge sono disponibili nella [guida dell&#39;interfaccia utente per la segmentazione Edge](./edge-segmentation.md)

## Violazioni dei criteri

>[!NOTE]
>
>Le violazioni dei criteri si applicano solo se stai creando un pubblico assegnato a una destinazione.

Una volta completata la creazione del pubblico, questo verrà analizzato da Governance dei dati di Adobe Experience Platform per garantire che non vi siano violazioni dei criteri all’interno del pubblico. Per ulteriori informazioni, vedere [Panoramica sulla governance dei dati](../../data-governance/home.md).

![Vengono visualizzate le violazioni dei criteri per il pubblico.](../images/ui/overview/audience-dule-policy-violations.png)

## Passaggi successivi e risorse aggiuntive {#next-steps}

L&#39;interfaccia utente di [!DNL Segmentation Service] offre un flusso di lavoro avanzato che consente di creare tipi di pubblico commerciabili dai dati di [!DNL Real-Time Customer Profile].

Per ulteriori informazioni su [!DNL Segmentation Service], continuare a leggere la documentazione. Per informazioni sull&#39;utilizzo dell&#39;API [!DNL Segmentation Service], leggere la [[!DNL Segmentation Service] guida per gli sviluppatori](../api/overview.md).
