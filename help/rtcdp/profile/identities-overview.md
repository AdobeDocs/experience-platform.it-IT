---
keywords: identità rtcdp;rtcdp identità;real-time cdp identità
title: Identità in Real-time Customer Data Platform
description: Il servizio Adobe Experience Platform Identity consente di ottenere una migliore visione dei clienti e del loro comportamento, collegando le identità tra dispositivi e sistemi diversi.
exl-id: 2b0d84de-9710-412e-ace7-56e3977245aa
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# Panoramica sulle identità

Adobe Experience Platform [!DNL Identity Service] consente di ottenere una visione migliore dei clienti e del loro comportamento, collegando le identità tra dispositivi e sistemi diversi. In genere, i clienti interagiscono con il marchio su più canali, ad esempio navigando sul sito web online, effettuando un acquisto in negozio, aderendo al programma fedeltà o chiamando un help desk per il supporto, per citarne alcuni. In questi sistemi multipli, viene creata un’identità per quel cliente e [!DNL Identity Service] rende possibile unire queste identità per vedere il quadro completo.

Ora, invece di cinque clienti distinti che interagiscono con il tuo marchio attraverso cinque canali diversi, puoi vedere che si tratta dello stesso cliente e assicurarti che essi ricevano un’esperienza coerente, personalizzata e rilevante tramite ogni interazione. Man mano che si scoprono ulteriori informazioni sul cliente (ad esempio, un browser anonimo del sito web decide di registrarsi a un account e di effettuare l’accesso), tali informazioni vengono unite insieme e l’immagine del cliente diventa sempre più chiara.

## Spazio dei nomi delle identità

Gli spazi dei nomi delle identità sono un componente di [!DNL Identity Service] e fungono da indicatori che forniscono ulteriore contesto alle identità dei clienti. Un esempio di spazio dei nomi ID comunemente utilizzato è &quot;E-mail&quot;, dove l’utilizzo dello stesso indirizzo e-mail su più siti web consente di unire diverse identità, ciascuna con un ID cliente univoco, come appartenenti in realtà allo stesso cliente. [!DNL Experience Platform] consente di utilizzare gli spazi dei nomi ID per cercare singoli profili all’interno dell’interfaccia utente. Per ulteriori informazioni sulla visualizzazione dei profili, consulta [panoramica sulla navigazione del profilo](profile-browse.md). Per ulteriori informazioni sugli spazi dei nomi di identità, consulta [panoramica dello spazio dei nomi delle identità](../../identity-service/namespaces.md).

## Grafici delle identità

Un grafo di identità è una mappa delle relazioni tra diversi spazi dei nomi di identità, che ti fornisce una rappresentazione visiva di come il cliente interagisce con il tuo marchio su canali diversi. Tutti i grafici delle identità dei clienti sono gestiti e aggiornati collettivamente da [!DNL Identity Service] quasi in tempo reale, in risposta all’attività del cliente.

[!DNL Identity Service] gestisce un grafo di identità visibile solo dalla tua organizzazione e basato sui tuoi dati, o grafo privato. [!DNL Identity Service] potenzia il grafico privato quando un record di dati acquisito contiene più di un’identità, aggiungendo una relazione tra le identità trovate.

## Passaggi successivi

Le identità e le relazioni tra di esse sono definite e mantenute da [!DNL Identity Service] e utilizzati da [!DNL Real-Time Customer Profile] per creare un quadro completo di ogni singolo cliente e delle sue interazioni. Per ulteriori informazioni, visita il [Documentazione del servizio Identity](../../identity-service/home.md).
