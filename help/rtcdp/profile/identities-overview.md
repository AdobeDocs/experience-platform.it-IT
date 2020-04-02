---
title: Identità e spazi dei nomi di identità
seo-title: Servizio Adobe Experience Platform Identity
description: description
seo-description: descrizione SEO
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87

---


# Identità in CDP in tempo reale

Adobe Experience Platform Identity Service ti aiuta a ottenere una visione migliore dei tuoi clienti e del loro comportamento collegando le identità tra dispositivi e sistemi. In genere, i clienti interagiscono con il tuo marchio su più canali, tra cui visitare il sito Web online, effettuare un acquisto in-store, partecipare al programma fedeltà o chiamare un help desk per il supporto, per citarne alcuni. Tra questi diversi sistemi, esiste un&#39;identità creata per quel cliente, e Identity Service permette di unire queste identità per vedere il quadro completo.

Ora, invece di cinque clienti separati che interagiscono con il tuo marchio su cinque canali diversi, puoi vedere che si tratta dello stesso cliente e accertarti che riceva un&#39;esperienza coerente, personalizzata e rilevante attraverso ogni interazione. Man mano che si rendono note ulteriori informazioni sul cliente (ad esempio, un browser anonimo del sito Web decide di registrarsi per un account e di effettuare l’accesso), le informazioni vengono unite insieme e l’immagine del cliente diventa sempre più chiara.

## Spazi dei nomi delle identità

Gli spazi dei nomi delle identità sono un componente di Servizio identità e fungono da indicatori che forniscono contesto aggiuntivo alle identità dei clienti. Un esempio dello spazio dei nomi ID comunemente usato sarebbe &quot;E-mail&quot;, dove l&#39;uso dello stesso indirizzo e-mail in più siti Web consente di unire diverse identità diverse, ognuna con un ID cliente univoco, che appartengono effettivamente allo stesso cliente. Experience Platform consente di utilizzare gli spazi dei nomi ID per cercare singoli profili all&#39;interno dell&#39;interfaccia utente. Per ulteriori informazioni sulla visualizzazione dei profili, consultate la panoramica [del visualizzatore dei](/help/rtcdp/profile/profile-viewer.md)profili. Per ulteriori informazioni sugli spazi dei nomi di identità, vedere la panoramica [dello spazio dei nomi di](../../identity-service/namespaces.md)identità.

## Grafici di identità

Un grafico di identità è una mappa di relazioni tra diversi spazi dei nomi di identità, che fornisce una rappresentazione visiva di come il cliente interagisce con il proprio marchio tra canali diversi. Tutti i grafici dell&#39;identità del cliente vengono gestiti collettivamente e aggiornati da Identity Service in tempo quasi reale, in risposta all&#39;attività del cliente.

Servizio identità gestisce un grafico di identità visibile solo dalla tua organizzazione e basato sui dati, detto grafico privato. Il servizio identità amplia il grafico privato quando un record di dati assimilato contiene più identità, aggiungendo una relazione tra le identità trovate.

## Passaggi successivi

Le identità e le relazioni tra di esse sono definite e mantenute dal Servizio identità e sfruttate dal Profilo cliente in tempo reale per creare un quadro completo di ogni singolo cliente e delle sue interazioni. Per ulteriori informazioni, consulta la documentazione [del servizio](../../identity-service/home.md)identità.