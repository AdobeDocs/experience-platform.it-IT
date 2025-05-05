---
title: Lead per la corrispondenza dell’account in Real-Time CDP B2B
type: Documentation
description: Panoramica e ulteriori informazioni sulla funzione di corrispondenza lead-account in Experience Platform CDP B2B.
feature: Get Started, Profiles, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/it/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 2f853599-6bca-4ba6-bbba-131a49d8854e
source-git-commit: 4ba609e777716b1b38f5b143587e5476d851e344
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 3%

---

# Lead per la corrispondenza dell’account in Real-Time CDP B2B

## Panoramica {#overview}

Il marketing basato sull’account è una strategia sempre più importante per il marketing B2B. Il marketing basato su account offre i seguenti vantaggi chiave per acquisire clienti specifici di alto valore:

- Cancella ROI
- Allineamento vendite e marketing
- Un approccio personalizzato
- Riduzione dello spreco di risorse
- Un ciclo di vendita più breve

Il marketing basato sull&#39;account consente di collegare i clienti noti agli account di vendita. Questo consente ai team di marketing di interagire con potenziali lead provenienti dagli account di destinazione nelle prime fasi del percorso del cliente per aumentare le possibilità di conversione. Un record di persona noto include in genere una parte o tutte le seguenti informazioni:

- Nome della persona
- Indirizzo e-mail
- Numero di contatto
- Nome società
- Sito Web della società
- Qualifica
- Posizione

## Come funziona {#how-it-works}

I processi eseguiti quotidianamente utilizzano fattori deterministici e probabilistici per abbinare profili lead noti senza associazioni di account esistenti. I profili lead noti avranno a disposizione uno dei seguenti attributi:

- b2b.companyName
- b2b.companyWebsite
- workEmail

>[!NOTE]
>
> L’attributo b2b.personKey.sourceKey deve esistere.

Gli attributi b2b.companyName, b2b.companyWebsite e b2b.personKey.sourceKey possono essere posizionati nel gruppo di campi b2b nello schema persona B2B.

![Schema persona B2B con attributi](/help/rtcdp/accounts/images/b2b-person-schema.png)

L’attributo workEmail si trova come gruppo di campi di livello superiore nello schema persona B2B.

![Schema persona B2B che mostra workEmail](/help/rtcdp/accounts/images/b2b-person-workemail.png)

I profili avranno una corrispondenza migliore solo se il punteggio di corrispondenza supera la soglia di affidabilità interna. I risultati vengono salvati in un nuovo set di dati di sistema dell’XDM di relazione account-persona esistente.

Il servizio di corrispondenza lead-account viene eseguito quando diventa disponibile una nuova istantanea del profilo persona, che viene eseguita ogni 24 ore. Consulta la documentazione per ulteriori informazioni sulla [configurazione del lead per corrispondenza account](/help/rtcdp/accounts/account-profile-ui-guide.md).

## Come visualizzare l’output di corrispondenza lead-account {#how-to-view}

Dopo l’esecuzione del processo, i risultati vengono salvati in un nuovo set di dati dell’XDM di relazione account-persona esistente.

Per visualizzare l&#39;anteprima del set di dati, seleziona **[!UICONTROL Anteprima set di dati]** in alto a destra.

![Nuovo set di dati](/help/rtcdp/accounts/images/b2b-dataset-output.png)

Il set di dati include le informazioni dell’account corrispondenti e il punteggio di corrispondenza per il set di dati scelto. Il campo **[!UICONTROL Relazione Source]** indica se proviene dal processo di corrispondenza lead-account.

![Anteprima risultati e punteggi di attendibilità del set di dati](/help/rtcdp/accounts/images/b2b-dataset-preview.png)

## Monitoraggio dei processi di corrispondenza lead-account {#monitoring-jobs}

Puoi monitorare lo stato del processo e le metriche associate per qualsiasi lead in corrispondenza dell’account attraverso il dashboard.

Consulta la documentazione per ulteriori informazioni sui [processi di monitoraggio per la corrispondenza lead-account](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
