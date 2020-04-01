---
keywords: Experience Platform;getting started;attribution ai;popular topics
solution: Experience Platform
title: Guida introduttiva all’interfaccia di attribuzione AI
topic: Getting started
translation-type: tm+mt
source-git-commit: 14d47f99f1edd7734245b25b7c39f3a71e7aac50

---


# Guida introduttiva all’interfaccia di attribuzione AI

Le guide seguenti richiedono una conoscenza approfondita dei vari servizi Adobe Experience Platform coinvolti nell&#39;utilizzo di Attribution AI. Prima di iniziare le esercitazioni, consulta i documenti seguenti:

- [Panoramica](../../xdm/home.md)del sistema XDM (Experience Data Model): XDM è il framework fondamentale che consente ad Adobe Experience Cloud, basato su Experience Platform, di inviare il messaggio giusto alla persona giusta, sul canale giusto, al momento giusto. La metodologia su cui è basata Experience Platform, XDM System, rende operativi gli schemi di Experience Data Model per l&#39;utilizzo da parte dei servizi della piattaforma.
- [Nozioni di base sulla composizione](../../xdm/schema/composition.md)dello schema: Questo documento fornisce un&#39;introduzione agli schemi di Experience Data Model (XDM) e ai blocchi costitutivi, ai principi e alle procedure ottimali per la composizione degli schemi da utilizzare in Adobe Experience Platform.
- [Creazione di schemi](../../xdm/tutorials/create-schema-ui.md): Questa esercitazione descrive i passaggi necessari per creare uno schema utilizzando l&#39;Editor di schema in Experience Platform.

L&#39;AI di attribuzione richiede che i set di dati siano conformi allo schema Eventi esperienza cliente (CEE), che è un mixin in XDM ( [Experience Data Model](../../xdm/home.md) ). Per implementare o modificare questi dati, contattate il supporto Adobe all&#39;indirizzo attributionai-support@adobe.com. Se i dati sulla spesa media sono presenti, potete eseguire ulteriori analisi, ad esempio ricavi incrementali e ROI. Se i dati del profilo cliente sono disponibili, potete attribuire ulteriormente i crediti al livello del profilo cliente.

## Terminologia

- **Evento di conversione:** Qualsiasi evento digitale o interazione digitale che i clienti fanno per indicare una pietra miliare verso un obiettivo, ad esempio le registrazioni delle conferenze. Altri esempi includono conversioni a pagamento, registrazioni di account gratuite o qualificazioni per una caratteristica.

- **Punto di contatto:** Qualsiasi evento digitale o interazione digitale che i clienti fanno nel percorso verso un obiettivo. Alcuni esempi includono le attività di marketing relative al periodo precedente l&#39;acquisto, la visualizzazione delle impression pubblicitarie visualizzate e i clic di ricerca a pagamento.

## Accesso e query ai punteggi

>[!NOTE] Se non è necessario eseguire query o accedere ai punteggi non elaborati, è possibile saltare questo passaggio e passare alla guida [all&#39;interfaccia](./user-guide.md)utente.

Accedere e interrogare i punteggi per Attribution AI è fatto tramite Snowflake. Al momento, è necessario inviare tramite e-mail il supporto Adobe all&#39;indirizzo attributionai-support@adobe.com per configurare e ricevere le credenziali per l&#39;account del lettore per Snowflake o per l&#39;esportazione in massa di dati non elaborati.

Una volta che il supporto Adobe ha elaborato la richiesta, vi viene fornito un URL per l’account del lettore a Snowflake e le credenziali corrispondenti riportate di seguito:

- URL fiocco di neve
- Nome utente
- Password

## Passaggi successivi

Una volta pronti e dotati di tutte le credenziali e gli schemi, iniziate seguendo la guida [all&#39;interfaccia utente AI di](./user-guide.md)Attribution. Questa guida illustra come creare un’istanza e inviarla per la formazione e il punteggio.