---
title: Lead per corrispondenza account in Real-Time CDP B2B
type: Documentation
description: Panoramica e ulteriori informazioni sulla funzione di corrispondenza del lead to account nell’Experience Platform CDP B2B.
exl-id: 2f853599-6bca-4ba6-bbba-131a49d8854e
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 3%

---

# Lead per corrispondenza account in Real-Time CDP B2B

## Panoramica {#overview}

Il marketing basato sugli account è una strategia sempre più importante per il marketing B2B. Il marketing basato su account offre i seguenti vantaggi chiave per acquisire clienti specifici di alto valore:

- Clear ROI
- Allineamento vendite e marketing
- Un approccio personalizzato
- Meno risorse sprecate
- Un ciclo di vendita più breve

Il marketing basato su account consente di collegare persone conosciute e visitatori web anonimi agli account di vendita. Questo consente ai team di marketing di interagire con potenziali lead dagli account di destinazione all’inizio del percorso di clienti per aumentare le possibilità di conversione. Un record di persona nota include in genere una parte o tutte le informazioni seguenti:

- Nome della persona
- Indirizzo e-mail
- Numero di contatto
- Nome dell’azienda
- Sito web dell&#39;azienda
- Titolo del processo
- Posizione

La corrispondenza dei lead con account consente di unire profili di persone noti ai profili di account. Puoi quindi segmentare ed eseguire il targeting dei dati in un contesto B2B come account, opportunità e così via. I profili personali possono essere classificati nelle tre categorie seguenti:

- **Profilo della persona dell’account:** Il profilo persona è già associato ad almeno un profilo account attraverso la relazione da un’origine dati. Ciò implica che esiste almeno un frammento di contatto.

>[!NOTE]
>
> I profili della persona dell’account non vengono confrontati quando si eseguono processi di corrispondenza lead a account.

- **Profilo persona nota:** Il profilo di persona NON è associato ad alcun profilo di account e almeno uno dei seguenti attributi di profilo di persona ha un valore:

   - Indirizzo e-mail
   - Nome dell’azienda
   - Sito web dell&#39;azienda

- **Profilo utente anonimo:** Il profilo di persona NON è associato ad alcun profilo di account e nessuno dei seguenti attributi di profilo di persona ha un valore:

   - Indirizzo e-mail
   - Nome dell’azienda
   - Sito web dell&#39;azienda

>[!NOTE]
>
> Un profilo persona può essere correlato a più profili account. Tuttavia, il processo di corrispondenza lead to account corrisponderà solo alla migliore corrispondenza. Se è necessario un set di corrispondenze più ampio, associa il lead alla corrispondenza del conto con la funzione account correlata.

## Come funziona {#how-it-works}

I lavori eseguiti quotidianamente utilizzano fattori deterministici e probabilistici per abbinare i profili di lead noti senza le associazioni di account esistenti. I profili lead noti avranno a disposizione uno dei seguenti attributi:

- b2b.companyName
- b2b.companyWebsite
- workEmail

>[!NOTE]
>
> L&#39;attributo b2b.personKey.sourceKey deve esistere.

Gli attributi b2b.companyName, b2b.companyWebsite e b2b.personKey.sourceKey possono essere situati nel gruppo di campi b2b nello schema persona B2B.

![Schema della persona B2B che mostra gli attributi](/help/rtcdp/accounts/images/b2b-person-schema.png)

L&#39;attributo workEmail può essere trovato come gruppo di campi di primo livello nello schema persona B2B.

![Schema delle persone B2B che mostra workEmail](/help/rtcdp/accounts/images/b2b-person-workemail.png)

La migliore corrispondenza tra i profili è possibile solo se il punteggio di corrispondenza supera una soglia di affidabilità interna. I risultati vengono salvati in un nuovo set di dati di sistema della relazione XDM della persona dell’account esistente.

Il servizio di corrispondenza lead to account viene eseguito quando diventa disponibile un nuovo snapshot del profilo persona, che è una volta ogni 24 ore. Consulta la documentazione per ulteriori informazioni sul [configurazione della corrispondenza tra lead e account](/help/rtcdp/accounts/account-profile-ui-guide.md).

## Come visualizzare l&#39;output corrispondente del lead a conto {#how-to-view}

Dopo l&#39;esecuzione del processo, i risultati vengono salvati in un nuovo set di dati della relazione XDM della persona dell&#39;account esistente.

Per visualizzare in anteprima il set di dati, seleziona **[!UICONTROL Anteprima set di dati]** in alto a destra.

![Nuovo set di dati](/help/rtcdp/accounts/images/b2b-dataset-output.png)

Il set di dati include le informazioni dell’account corrispondenti e il punteggio di corrispondenza per il set di dati scelto. La **[!UICONTROL Origine relazione]** Il campo indica se proviene dal processo di corrispondenza lead to account.

![Anteprima dei punteggi e dell’output di affidabilità del set di dati](/help/rtcdp/accounts/images/b2b-dataset-preview.png)

## Monitoraggio dei processi di corrispondenza dei lead all’account {#monitoring-jobs}

Puoi monitorare lo stato del processo e le metriche associate per tutti i processi di corrispondenza dei lead a account tramite il dashboard.

Consulta la documentazione per ulteriori informazioni sul [monitoraggio dei processi per la corrispondenza dei lead con account](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
