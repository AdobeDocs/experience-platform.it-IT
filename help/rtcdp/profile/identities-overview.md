---
keywords: identità rtcdp;rtcdp identità;real-time cdp identità
title: Identità in Real-time Customer Data Platform
description: Il servizio Adobe Experience Platform Identity consente di ottenere una migliore visione dei clienti e del loro comportamento, collegando le identità tra dispositivi e sistemi diversi.
feature: Get Started, Identities
exl-id: 2b0d84de-9710-412e-ace7-56e3977245aa
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---

# Panoramica sulle identità

Adobe Experience Platform [!DNL Identity Service] ti aiuta a ottenere una migliore visione dei tuoi clienti e del loro comportamento collegando le identità tra dispositivi e sistemi diversi. In genere, i clienti interagiscono con il marchio su più canali, ad esempio navigando sul sito web online, effettuando un acquisto in negozio, aderendo al programma fedeltà o chiamando un help desk per il supporto, per citarne alcuni. In questi diversi sistemi, è stata creata un&#39;identità per il cliente e [!DNL Identity Service] consente di unire tali identità per visualizzare il quadro completo.

Ora, invece di cinque clienti distinti che interagiscono con il tuo marchio attraverso cinque canali diversi, puoi vedere che si tratta dello stesso cliente e assicurarti che essi ricevano un’esperienza coerente, personalizzata e rilevante tramite ogni interazione. Man mano che si scoprono ulteriori informazioni sul cliente (ad esempio, un browser anonimo del sito web decide di registrarsi a un account e di effettuare l’accesso), tali informazioni vengono unite insieme e l’immagine del cliente diventa sempre più chiara.

## Spazio dei nomi delle identità

Gli spazi dei nomi delle identità sono un componente di [!DNL Identity Service] e fungono da indicatori che forniscono ulteriore contesto alle identità dei clienti. Un esempio di spazio dei nomi ID comunemente utilizzato è &quot;E-mail&quot;, dove l’utilizzo dello stesso indirizzo e-mail su più siti web consente di unire diverse identità, ciascuna con un ID cliente univoco, come appartenenti in realtà allo stesso cliente. [!DNL Experience Platform] consente di utilizzare gli spazi dei nomi ID per cercare singoli profili all&#39;interno dell&#39;interfaccia utente. Per ulteriori informazioni sulla visualizzazione dei profili, consulta la [panoramica sulla navigazione dei profili](profile-browse.md). Per ulteriori informazioni sugli spazi dei nomi di identità, consulta la [panoramica dello spazio dei nomi di identità](../../identity-service/features/namespaces.md).

## Grafici delle identità

Un grafo di identità è una mappa delle relazioni tra identità diverse, che ti fornisce una rappresentazione visiva di come il cliente interagisce con il tuo marchio su canali diversi. Tutti i grafici delle identità dei clienti sono gestiti e aggiornati collettivamente dal servizio Identity, in risposta all’attività del cliente.

[!DNL Identity Service] gestisce un grafo di identità visibile solo alla tua organizzazione e basato sui tuoi dati. [!DNL Identity Service] aumenta il grafico quando un record di dati acquisito contiene più di un&#39;identità, aggiungendo una relazione tra le identità trovate.

## Passaggi successivi

Le identità e le relazioni tra di esse vengono definite e gestite da [!DNL Identity Service] e sfruttate da [!DNL Real-Time Customer Profile] per creare un quadro completo di ogni singolo cliente e delle relative interazioni. Per ulteriori informazioni, visita la [documentazione del servizio Identity](../../identity-service/home.md).
