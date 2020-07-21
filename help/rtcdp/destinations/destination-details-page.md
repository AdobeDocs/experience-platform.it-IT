---
title: Pagina Dettagli destinazioni
seo-title: Pagina Dettagli destinazioni
description: 'La pagina dei dettagli per una singola destinazione fornisce una panoramica dei dettagli di destinazione, come il nome di destinazione, l''ID, i segmenti mappati alla destinazione, e i controlli per modificare l''attivazione e per attivare e disattivare il flusso di dati. '
seo-description: 'La pagina dei dettagli per una singola destinazione fornisce una panoramica dei dettagli di destinazione, come il nome di destinazione, l''ID, i segmenti mappati alla destinazione, e i controlli per modificare l''attivazione e per attivare e disattivare il flusso di dati. '
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---


# Pagina dei dettagli sulla destinazione {#destinations-details-page}

La pagina dei dettagli per una singola destinazione fornisce una panoramica dei dettagli di destinazione, come il nome di destinazione, l&#39;ID, i segmenti mappati alla destinazione, e i controlli per modificare l&#39;attivazione e per attivare e disattivare il flusso di dati. Per visualizzare questi dettagli, andate a **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** e fate clic sul nome della destinazione con cui desiderate lavorare.

I componenti core di una singola destinazione sono:

* 1 - Nome e ID della destinazione
* 2 - Segmenti attivati per la destinazione
* 3 - Informazioni sulla barra a destra
* 4 - Controlli per modificare l&#39;attivazione e attivare/disattivare il flusso di dati

![Pagina Destinazioni numerata](/help/rtcdp/destinations/assets/destination-page-numbered.png)

Passate a una singola pagina di destinazione per ottenere una panoramica dei dettagli di destinazione, ad esempio:

## 1. Nome e ID della destinazione

Nell’URL della pagina potete visualizzare il nome della destinazione nell’intestazione della pagina e l’ID di destinazione.

## 2. Segmenti attivati per la destinazione

In questa sezione vengono visualizzati i segmenti attualmente mappati sulla destinazione e ulteriori informazioni su di essi. Per ulteriori informazioni, consulta la tabella seguente:

| Elemento | Descrizione |
---------|----------|
| Nome segmento | Nome del segmento. |
| Descrizione segmento | Descrizione del segmento. |
| Data inizio | Data in cui questi segmenti vengono attivati nella destinazione. |
| Data fine | Data in cui questi segmenti cesseranno di essere attivati sulla destinazione. |
| ID mappatura | *Non disponibile per le destinazioni* di e-mail marketing. Indica l&#39;ID tramite il quale il segmento è noto nella piattaforma di destinazione. |

## 3. Informazioni sulla barra a destra

La barra laterale destra include informazioni sulla destinazione. Per ulteriori informazioni, consulta la tabella seguente:

| Elemento | Descrizione |
---------|----------|
| Piattaforma | Rappresenta la piattaforma di destinazione a cui vengono inviati i tipi di pubblico. Per ulteriori informazioni, consulta Catalogo [delle](/help/rtcdp/destinations/destinations-catalog.md) destinazioni. |
| Descrizione | Puoi modificare la descrizione del flusso di destinazione. |
| Categoria | Indica il tipo di destinazione. Per ulteriori informazioni, consulta Catalogo [delle](/help/rtcdp/destinations/destinations-catalog.md) destinazioni. |
| Tipo connessione | Indica in quale modulo le audience vengono inviate alla destinazione. Può essere **[!UICONTROL Cookie]** o **[!UICONTROL Profile-based]**. |
| Frequenza | Indica la frequenza con cui le audience vengono inviate alla destinazione. Può essere **[!UICONTROL Streaming]** o **[!UICONTROL Batch]**. |
| Identità | Rappresenta lo spazio nomi identità accettato dalla destinazione. Ad esempio, il campo Identità può essere GAID, IDFA, email. Per tutti gli spazi dei nomi di identità accettati, vedere Spazi dei nomi standard nella panoramica [dello spazio dei nomi dell&#39;](../../identity-service/namespaces.md)identità. |
| Creato da | Indica l&#39;utente che ha creato il flusso di destinazione. |
| Creato | Indica la data e l&#39;ora UTC in cui è stato creato il flusso di destinazione. |

## 4. Controlli per modificare l&#39;attivazione e attivare/disattivare il flusso di dati

Il controllo di attivazione Modifica consente di modificare i segmenti mappati alla destinazione. Premere Modifica attivazione per aprire il flusso di lavoro [di attivazione del](/help/rtcdp/destinations/activate-destinations.md)segmento.

Utilizzate l&#39; **opzione Attiva/Disattiva** per avviare e mettere in pausa l&#39;esportazione dei dati verso una destinazione.