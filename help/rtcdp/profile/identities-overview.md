---
keywords: identità rtcdp;identità rtcdp;identità cdp in tempo reale
title: Identità nella piattaforma dati cliente in tempo reale
description: Adobe Experience Platform Identity Service ti aiuta a ottenere una visione migliore dei tuoi clienti e del loro comportamento collegando le identità tra dispositivi e sistemi.
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---


# Identità nella piattaforma dati cliente in tempo reale

Adobe Experience Platform [!DNL Identity Service] consente di avere una visione migliore dei clienti e del loro comportamento collegando identità tra dispositivi e sistemi. In genere, i clienti interagiscono con il tuo marchio su più canali, tra cui visitare il sito Web online, effettuare un acquisto in-store, partecipare al programma fedeltà o chiamare un help desk per il supporto, per citarne alcuni. Tra questi diversi sistemi, esiste un&#39;identità creata per quel cliente, e [!DNL Identity Service] consente di unire queste identità per vedere il quadro completo.

Ora, invece di cinque clienti separati che interagiscono con il tuo marchio su cinque canali diversi, puoi vedere che si tratta dello stesso cliente e accertarti che riceva un&#39;esperienza coerente, personalizzata e rilevante attraverso ogni interazione. Man mano che si rendono note ulteriori informazioni sul cliente (ad esempio, un browser anonimo del sito Web decide di registrarsi per un account e di effettuare l’accesso), le informazioni vengono unite insieme e l’immagine del cliente diventa sempre più chiara.

## Spazi dei nomi delle identità

Gli spazi dei nomi delle identità sono un componente di [!DNL Identity Service] e fungono da indicatori che forniscono contesto aggiuntivo alle identità dei clienti. Un esempio dello spazio dei nomi ID comunemente usato sarebbe &quot;E-mail&quot;, dove l&#39;uso dello stesso indirizzo e-mail in più siti Web consente di unire diverse identità diverse, ognuna con un ID cliente univoco, che appartengono effettivamente allo stesso cliente. [!DNL Experience Platform] consente di utilizzare gli spazi dei nomi ID per cercare singoli profili all’interno dell’interfaccia utente. Per ulteriori informazioni sulla visualizzazione dei profili, consultate la [panoramica del visualizzatore dei profili](/help/rtcdp/profile/profile-viewer.md). Per ulteriori informazioni sugli spazi dei nomi di identità, vedere la [panoramica dello spazio dei nomi di identità](../../identity-service/namespaces.md).

## Grafici di identità

Un grafico di identità è una mappa di relazioni tra diversi spazi dei nomi di identità, che fornisce una rappresentazione visiva di come il cliente interagisce con il proprio marchio tra canali diversi. Tutti i grafici dell&#39;identità del cliente vengono gestiti e aggiornati collettivamente da [!DNL Identity Service] in tempo quasi reale, in risposta all&#39;attività del cliente.

[!DNL Identity Service] gestisce un grafico di identità visibile solo dalla tua organizzazione e basato sui dati, detto grafico privato. [!DNL Identity Service] amplia il grafico privato quando un record di dati acquisito contiene più identità, aggiungendo una relazione tra le identità trovate.

## Passaggi successivi

Le identità e le relazioni tra di esse sono definite e mantenute da [!DNL Identity Service] e sfruttate da [!DNL Real-time Customer Profile] per creare un quadro completo di ciascun cliente e delle sue interazioni. Per ulteriori informazioni, consultare la [documentazione del servizio identità](../../identity-service/home.md).