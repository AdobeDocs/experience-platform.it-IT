---
title: Account correlati in Real-Time CDP B2B Edition
type: Documentation
description: Una panoramica e ulteriori informazioni sulla funzione relativa agli account in Experience Platform Real-time CDP B2B.
exl-id: 37fd2cdb-87c0-4e5e-9599-ad4f397f7c28
source-git-commit: 5be8eac1603f1b81e45b4c0aeace5c2017b46149
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 5%

---

# Account correlati in Real-Time CDP B2B Edition

## Panoramica {#overview}

Le imprese B2B spesso presentano le informazioni sui clienti memorizzate in più sistemi, ciascuno dei quali include solo dati parziali o persino in conflitto per la stessa entità aziendale nel mondo reale. Questo crea una grande sfida nell&#39;ottenere una visione accurata dei loro clienti, riducendo così l&#39;efficienza e l&#39;efficacia dei loro sforzi di marketing e vendita B2B.

| ID | Nome | Sito web | Industria | Stato | Telefono | Ha un&#39;opportunità aperta con importo > `$1 million` |
|---|---|---|---|---|---|---|
| 1 | Acme | acme.com | Software | CA | (408)536-6000 |  |
| 2 | Acme | acm.com | Software | CA | 4085366000 | x |
| 3 | Acme Inc |  |  | CA | (408)5366000 |  |
| 4 | Servizio di consulenza Acme | `http://www.acme.com/consulting` | Consulenza tecnologica | NY | (212) 471-0904 | x |
| 5 | IT Acme |  |  | CA |  |  |

{style=&quot;table-layout:auto&quot;}

Con i relativi conti, [!DNL Real-time CDP B2B] ora mostra un elenco di account simili all’account che stai esplorando.

![Schermata che mostra gli account correlati nell’interfaccia utente di Experience Platform.](/help/rtcdp/b2b-ai-ml-services/assets/related-accounts-in-ui.png)

Utilizza questa funzione per visualizzare i profili di account correlati per un profilo di account nell’interfaccia utente di Experience Platform e quindi includi gli account correlati nelle definizioni dei segmenti per ampliare la portata o applicare criteri più ampi nei segmenti.

## Come funziona {#how-it-works}

I lavori di apprendimento automatico eseguiti quotidianamente utilizzano un algoritmo gerarchico per raggruppare profili account simili in gruppi basati su tre fattori:

* Collegamento account padre
* Dominio Web
* Nome account

A seguito di un processo di elaborazione completato, ogni membro del gruppo di profili account viene contrassegnato con l&#39;elenco Account correlati. È possibile visualizzare l’elenco nella **Account correlati** della pagina Profilo account e utilizza gli account correlati nelle definizioni dei segmenti.

Consulta la documentazione per ulteriori informazioni sul [lavori relativi all’arricchimento dei profili](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).

## Come visualizzare gli account correlati {#how-to-view}

Puoi visualizzare gli account correlati per un account che stai navigando nell’interfaccia utente di Experience Platform.

Consulta la documentazione per ulteriori informazioni sul [come trovare account correlati nell’interfaccia utente](/help/rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab).

## Come utilizzare account correlati {#how-to-use}

Puoi utilizzare account e account correlati nella segmentazione. La decisione di utilizzare account correlati nelle definizioni dei segmenti dipende dal tuo caso d’uso di marketing. Ad esempio, puoi utilizzare account correlati per campagne di marketing e-mail o pubblicitarie in cui puoi accettare una precisione inferiore in cambio di una portata più ampia.

Vedi [esempio di segmentazione](/help/rtcdp/segmentation/b2b.md#related-accounts) che utilizza account correlati.
