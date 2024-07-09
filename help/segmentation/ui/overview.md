---
solution: Experience Platform
title: Guida dell’interfaccia utente del servizio di segmentazione
description: Scopri come creare e gestire tipi di pubblico e definizioni di segmenti nell’interfaccia utente di Adobe Experience Platform.
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: acfe91144175e136955ffd9f0cdae2c351217c16
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 1%

---

# Guida dell’interfaccia utente di Segmentation Service

[!DNL Adobe Experience Platform Segmentation Service] fornisce un’interfaccia utente per la creazione e la gestione dei tipi di pubblico e delle definizioni dei segmenti.

## Introduzione

L’utilizzo dei tipi di pubblico e delle definizioni dei segmenti richiede una comprensione dei vari [!DNL Experience Platform] servizi coinvolti nella segmentazione. Prima di leggere questa guida utente, consulta la documentazione dei seguenti servizi:

- [[!DNL Segmentation Service]](../home.md): [!DNL Segmentation Service] consente di segmentare i dati memorizzati in [!DNL Experience Platform] che si riferisce a singoli utenti (come clienti, potenziali clienti, utenti o organizzazioni) in gruppi più piccoli.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): consente la creazione di profili cliente collegando le identità da diverse origini dati acquisite in [!DNL Platform].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Platform] organizza i dati sull’esperienza del cliente. Per utilizzare al meglio la segmentazione, assicurati che i dati vengano acquisiti come profili ed eventi in base alla [best practice per la modellazione dei dati](../../xdm/schema/best-practices.md).

Devi inoltre comprendere i seguenti termini chiave utilizzati in questo documento e la loro differenza:

- **Pubblico**: una raccolta di persone che condividono comportamenti e/o caratteristiche simili. Questa raccolta di persone può essere generata da Adobe Experience Platform utilizzando le definizioni dei segmenti (pubblico generato da Platform), la composizione del pubblico o da fonti esterne, come caricamenti personalizzati (pubblico generato esternamente).
- **Definizione del segmento**: regole utilizzate da Adobe Experience Platform per descrivere le caratteristiche o il comportamento chiave di un pubblico target.
- **Segmento**: atto di separazione dei profili in tipi di pubblico.

## Panoramica

Nell’interfaccia utente di Experience Platform, seleziona **[!UICONTROL Tipi di pubblico]** nel menu di navigazione a sinistra per aprire **[!UICONTROL Panoramica]** scheda che visualizza [!UICONTROL Tipi di pubblico] dashboard.

>[!NOTE]
>
>Se la tua organizzazione non utilizza ancora Platform e non dispone ancora di set di dati di profilo attivi o criteri di unione creati, il [!UICONTROL Tipi di pubblico] dashboard non visibile. Al contrario, [!UICONTROL Panoramica] Nella scheda vengono visualizzati collegamenti e documentazione per aiutarti a iniziare a utilizzare i tipi di pubblico.

### [!UICONTROL Tipi di pubblico] dashboard {#segments-dashboard}

Il **[!UICONTROL Tipi di pubblico]** la dashboard illustra le metriche chiave relative ai dati sul pubblico della tua organizzazione.

Per ulteriori informazioni, visita [guida della dashboard di audiences](../../dashboards/guides/audiences.md).

![Viene visualizzato il dashboard del pubblico. Mostra vari widget, tra cui la dimensione del pubblico, i profili per identità, la sovrapposizione delle identità e la tendenza di modifica della dimensione del pubblico.](../../dashboards/images/segments/dashboard-overview.png)

## Sfogliare {#browse}

Seleziona la **[!UICONTROL Sfoglia]** per visualizzare Audience Portal. Audience Portal fornisce un elenco di tutti i tipi di pubblico che appartengono alla tua organizzazione e alla sandbox e include dettagli quali il conteggio dei profili, l’origine, la data di creazione, la data dell’ultima modifica, i tag e il raggruppamento.

Inoltre, Audience Portal consente di creare nuovi tipi di pubblico utilizzando Segment Builder (Generatore di segmenti) o Audience Composition (Composizione pubblico), nonché di importare in Platform tipi di pubblico generati esternamente.

Per ulteriori informazioni su Audience Portal, leggi [Panoramica di Audience Portal](./audience-portal.md).

## Composizioni {#compositions}

Seleziona la **[!UICONTROL Composizioni]** per visualizzare un elenco di tutti i tipi di pubblico generati tramite la Composizione del pubblico per la tua organizzazione.

![Un elenco di tipi di pubblico creati in Composizione pubblico per la tua organizzazione.](../images/ui/overview/compositions.png)

Per impostazione predefinita, questa visualizzazione elenca informazioni sui tipi di pubblico, tra cui nome, stato, data di creazione, data di creazione, data dell’ultimo aggiornamento e data dell’ultimo aggiornamento di.

Accanto a ogni pubblico è presente un’icona con i puntini di sospensione. Selezionando questa opzione viene visualizzato un elenco delle azioni rapide disponibili per il pubblico.

| Azione | Descrizione |
| ------ | ----------- |
| Duplica | Copia il pubblico selezionato. |
| Gestisci accesso | Gestisce le etichette di accesso che appartengono al pubblico. Per ulteriori informazioni sulle etichette di accesso, consulta la documentazione su [gestione delle etichette](../../access-control/abac/ui/labels.md). |
| Elimina | Elimina il pubblico selezionato. Tipi di pubblico utilizzati nelle destinazioni a valle o dipendenti da altri tipi di pubblico **non può** essere soppressa. Per ulteriori informazioni sull’eliminazione del pubblico, consulta la sezione [domande frequenti sulla segmentazione](../faq.md#lifecycle-states). |

È possibile selezionare ![Personalizza tabella](../images/ui/overview/customize-table.png) per modificare i campi visualizzati.

![Viene evidenziato il pulsante Personalizza tabella. Selezionando questo pulsante puoi personalizzare i campi visualizzati nella pagina Composizioni pubblico.](../images/ui/overview/compositions-select-customize-table.png)

Viene visualizzato un popover che elenca tutti i campi che possono essere visualizzati nella tabella.

![Attributi che possono essere visualizzati per la sezione Composizione.](../images/ui/overview/compositions-customize-table.png)

| Campo | Descrizione |
| ----- | ----------- | 
| [!UICONTROL Nome] | Il nome del pubblico. |
| [!UICONTROL Stato] | Stato del pubblico. I valori possibili per questo campo includono `Draft`, `Inactive`, e `Published`. |
| [!UICONTROL Creato] | L’ora e la data di creazione del pubblico. |
| [!UICONTROL Creato da] | Nome della persona che ha creato il pubblico. |
| [!UICONTROL Aggiornato] | Ora e data dell’ultimo aggiornamento del pubblico. |
| [!UICONTROL Aggiornato da] | Nome dell’ultima persona che ha aggiornato il pubblico. |

Per visualizzare la modalità di composizione del pubblico, seleziona il nome di un pubblico all’interno del [!UICONTROL Tipi di pubblico] scheda.

Viene visualizzata la pagina Composizione pubblico con i blocchi predefiniti che compongono il pubblico. Per ulteriori dettagli su come utilizzare Composizione del pubblico, leggi [Guida dell’interfaccia utente di Audience Composition](./audience-composition.md).

## Segmentazione in streaming {#streaming-segmentation}

La segmentazione in streaming è la capacità di eseguire la segmentazione su [!DNL Platform] quasi in tempo reale, concentrandosi sulla ricchezza dei dati. Con la segmentazione in streaming, la qualificazione per la segmentazione ora avviene quando i dati arrivano in [!DNL Platform], riducendo la necessità di pianificare ed eseguire processi di segmentazione.

Ulteriori informazioni sulla segmentazione dello streaming sono disponibili nella sezione [guida utente sulla segmentazione in streaming](./streaming-segmentation.md).

>[!NOTE]
>
>Affinché la segmentazione in streaming funzioni, devi abilitare la segmentazione pianificata per l’organizzazione. Per informazioni dettagliate sull’abilitazione della segmentazione pianificata, consulta [la sezione segmentazione streaming in questa guida utente](#scheduled-segmentation).

## Segmentazione Edge {#edge-segmentation}

La segmentazione di Edge è la capacità di valutare i tipi di pubblico in Platform istantaneamente al limite, abilitando casi di utilizzo di personalizzazione della stessa pagina e della pagina successiva.

Ulteriori informazioni sulla segmentazione Edge sono disponibili nella sezione [guida dell’interfaccia utente per la segmentazione Edge](./edge-segmentation.md)

## Violazioni dei criteri

>[!NOTE]
>
>Le violazioni dei criteri si applicano solo se stai creando un pubblico assegnato a una destinazione.

Una volta completata la creazione del pubblico, questo verrà analizzato da Governance dei dati di Adobe Experience Platform per garantire che non vi siano violazioni dei criteri all’interno del pubblico. Consulta la [Panoramica sulla governance dei dati](../../data-governance/home.md) per ulteriori informazioni.

![Vengono visualizzate le violazioni dei criteri per il pubblico.](../images/ui/overview/audience-dule-policy-violations.png)

## Passaggi successivi e risorse aggiuntive {#next-steps}

Il [!DNL Segmentation Service] L’interfaccia utente offre un flusso di lavoro avanzato che consente di creare tipi di pubblico commerciabili da [!DNL Real-Time Customer Profile] dati.

Per ulteriori informazioni su [!DNL Segmentation Service], continua a leggere la documentazione. Per scoprire come utilizzare il [!DNL Segmentation Service] API, leggi le [[!DNL Segmentation Service] guida per sviluppatori](../api/overview.md).
