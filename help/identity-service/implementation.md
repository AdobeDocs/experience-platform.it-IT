---
title: Guida all’implementazione per il servizio Identity
description: Scopri come vengono elaborati i dati forniti a Adobe Experience Platform prima di essere utilizzati da Identity Service per creare grafici delle identità.
source-git-commit: bdda234c44b63999d7582857975afa64fdb93605
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 0%

---

# Guida all’implementazione per il servizio Identity

Questo documento fornisce informazioni su come vengono elaborati i dati forniti a Adobe Experience Platform prima di essere utilizzati da Identity Service per creare un grafico delle identità per un determinato cliente.

## Decidere sui campi di identità

A seconda della strategia di raccolta dati aziendale, i campi dati etichettati come identità determinano quali dati includere nella mappa delle identità. Per ottenere il massimo beneficio da Experienci Platform e dalle identità cliente più complete possibili, devi caricare dati sia online che offline.

* I dati online sono dati che descrivono la presenza e il comportamento online, ad esempio nomi utente e indirizzi e-mail.

* I dati offline si riferiscono a dati che non sono direttamente correlati alla presenza online, come gli ID provenienti dai sistemi CRM. Questo tipo di dati rende le identità più solide e supporta la coesione dei dati tra sistemi diversi.

## Creare spazi dei nomi di identità aggiuntivi

Sebbene Experienci Platform offra diversi spazi dei nomi standard, potrebbe essere necessario creare spazi dei nomi aggiuntivi per categorizzare correttamente le identità. Per ulteriori informazioni, consulta la guida su [creazione di spazi dei nomi personalizzati per l’organizzazione](./namespaces.md).

>[!NOTE]
>
>Gli spazi dei nomi di identità sono un qualificatore per le identità. Di conseguenza, una volta creato, uno spazio dei nomi non può essere eliminato.

## Includere dati di identità in Experience Data Model (XDM)

In quanto framework standardizzato tramite il quale Experienci Platform organizza i dati dei clienti, Experience Data Model (XDM) consente la condivisione e la comprensione dei dati tra Experienci Platform e altri servizi che interagiscono con Experienci Platform. Per ulteriori informazioni, consulta [Panoramica del sistema XDM](../xdm/home.md).

Sia gli schemi di record che quelli di serie temporali forniscono i mezzi per includere i dati di identità. Quando i dati vengono acquisiti, il grafico delle identità crea nuove relazioni tra frammenti di dati da spazi dei nomi diversi se tali frammenti condividono dati di identità comuni.

## Etichettare i campi XDM come identità

Qualsiasi campo di tipo `string` negli schemi che implementano classi XDM di record o serie temporali, può essere etichettato come un campo di identità. Di conseguenza, tutti i dati acquisiti in quel campo verrebbero considerati dati di identità.

I campi di identità consentono anche il collegamento di identità se condividono dati PII comuni.
Ad esempio, etichettando i campi del numero di telefono come campi di identità, il servizio Identity traccia automaticamente le relazioni con gli altri utenti che utilizzano lo stesso numero di telefono.

>[!NOTE]
>
>* I campi di tipo matrice e mappa non sono supportati e non possono essere contrassegnati ed etichettati come campi di identità.
>* Lo spazio dei nomi delle identità risultanti viene fornito quando il campo viene etichettato.

## Configurare un set di dati per Identity Service

Durante il processo di acquisizione in streaming, Identity Service estrae automaticamente i dati di identità dai dati di record e serie temporali. Tuttavia, prima che i dati possano essere acquisiti, devono essere abilitati per il servizio Identity. Leggi l’esercitazione su  [configurazione di un set di dati per Real-Time Customer Profile e Identity Service tramite API](../profile/tutorials/dataset-configuration.md) per ulteriori informazioni.

## Acquisire dati in Identity Service

Il servizio Identity sfrutta i dati conformi a XDM inviati all’Experience Platform da [acquisizione batch](../ingestion/batch-ingestion/overview.md) o [acquisizione in streaming](../ingestion/streaming-ingestion/overview.md).

Il video seguente ha lo scopo di illustrare il servizio Identity. Questo video illustra come etichettare i campi dati come identità, acquisire i dati di identità e verificare che siano stati inseriti nel grafico privato del servizio Adobe Experience Platform Identity.

>[!WARNING]
>
>L’interfaccia utente di Experience Platform mostrata nel video seguente non è aggiornata. Consulta la documentazione per le schermate e le funzionalità più recenti dell’interfaccia utente.

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)