---
title: Migrare la mappatura ECID da persona ad attività utilizzando l’origine Marketo Engage
description: Scopri come migrare la mappatura ECID dal set di dati persona al set di dati attività utilizzando l’origine Marketo Engage.
source-git-commit: 0c695e11e7d7c14ef7e047cd007668e1099bf127
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# Migra mappatura ECID da [!DNL Person] set di dati a [!DNL Activity] set di dati

È possibile eseguire la migrazione della mappatura ECID dal [!DNL Marketo Engage Person] set di dati al tuo [!DNL Activity] set di dati per fornire un comportamento più stabile di acquisizione dei dati e gestione delle identità. Inoltre, questa migrazione tratta i seguenti argomenti:

| Problema | Soluzione |
| --- | --- |
| Quando [!DNL Marketo Person] il set di dati contiene collegamenti a più ECID, l’acquisizione dei dati non riesce quando [il numero totale di identità in un record Experience Data Model (XDM) supera 20](../../../../identity-service/guardrails.md). | Migrando il mapping dei campi ECID a [!DNL Activity], puoi assicurarti che il numero di identità provenienti da [!DNL Marketo Person] il flusso di dati rimane entro il limite e consente quindi l’acquisizione dei dati con esito positivo. |
| Ogni volta che [!DNL Marketo Person] viene acquisito con gli ECID, la marca temporale su tutti gli ECID da [!DNL Marketo Person] Il set di dati viene aggiornato con l’ultima marca temporale aggiornata del record Persona. Questo potrebbe comportare [eliminazione errata di identità più recenti dal grafico delle identità](../../../../identity-service/guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated). | Migrando le mappature dei campi ECID in [!DNL Activity], il servizio Identity può riflettere correttamente la marca temporale degli ECID e il meccanismo &quot;first in first out&quot; del servizio Identity fornirà un comportamento più stabile. |
| Quando gli ECID vengono acquisiti tramite [!DNL Marketo Person] flusso di dati, i nuovi ECID aggiunti non vengono acquisiti in Experienci Platform a meno che non ci siano aggiornamenti a [!DNL Person] registrare in [!DNL Marketo]. | Quando un nuovo ECID è collegato al [!DNL Person] registrare in [!DNL Marketo], è possibile acquisire i dati ECID tramite una [!DNL Marketo Activity] flusso di dati e richiede immediatamente un aggiornamento del grafo delle identità su Experienci Platform. |

In sostanza, devi:

* Aggiorna il tuo [!DNL Marketo Activity] flusso di dati.
* Aggiorna il tuo [!DNL Marketo Person] flusso di dati.

## Aggiorna [!DNL Marketo Activity] flusso di dati {#update-activity-dataflow}

Per aggiornare il tuo [!DNL Marketo Activity] flusso di dati:

* Nell’interfaccia utente di Experienci Platform, passa a *Sorgenti* e trovare il flusso di dati esistente per [!DNL Marketo Activity] dati.
* Dato che il flusso di dati è abilitato, seleziona i puntini di sospensione (`...`) accanto al nome del flusso di dati, quindi seleziona **[!UICONTROL Aggiorna flusso di dati]**.
* Quindi, seleziona **[!UICONTROL Successivo]** fino a raggiungere il *Mappatura* di rete.
* In *Mappatura* interfaccia, seleziona **[!UICONTROL Nuovo campo]** e quindi seleziona **[!UICONTROL Aggiungi campo calcolato]**. Da qui, devi aggiungere quanto segue:

| Set di dati di origine | Campo di destinazione XDM |
| --- | --- |
| `iif(${web\.ecid} != null, to_object('ECID', arrays_to_objects('id', explode(last(split(${web\.ecid}, ":")), " "))), null)` | `identityMap` |

>[!NOTE]
>
>Se l’aggiornamento a un [!DNL Marketo] il flusso di dati consiste solo nell’aggiungere o rimuovere il campo di mappatura ECID, quindi il flusso di dati ignora automaticamente il processo di backfill storico. L’acquisizione di nuovi dati si verifica solo quando si verificano tipi di attività come &quot;visita la pagina web&quot; e &quot;fai clic sulla pagina web&quot;.

## Aggiorna [!DNL Marketo Person] flusso di dati {#update-person-dataflow}

Per aggiornare il tuo [!DNL Marketo Person] flusso di dati:

* Nell’interfaccia utente di Experienci Platform, passa a *Sorgenti* e trovare il flusso di dati esistente per [!DNL Marketo Person] dati.
* Dato che il flusso di dati è abilitato, seleziona i puntini di sospensione (`...`) accanto al nome del flusso di dati, quindi seleziona **[!UICONTROL Aggiorna flusso di dati]**.
* Quindi, seleziona **[!UICONTROL Successivo]** fino a raggiungere il *Mappatura* di rete.
* In *Mappatura* , rimuovi il campo calcolato associato a `identityMap` e quindi seleziona **[!UICONTROL Successivo]** e **[!UICONTROL Salva e acquisisci]**.

>[!NOTE]
>
>Se l’aggiornamento a un [!DNL Marketo] il flusso di dati consiste solo nell’aggiungere o rimuovere il campo di mappatura ECID, quindi il flusso di dati ignora automaticamente il processo di backfill storico. La marca temporale degli ECID precedentemente acquisiti rimarrà invariata. Vengono aggiornati solo quando vengono acquisiti nuovi dati che corrispondono agli ECID esistenti.

## Passaggi successivi

Una volta letto questo documento, saprai come migrare la mappatura ECID dal tuo [!DNL Marketo Person] set di dati a [!DNL Marketo Activity] set di dati. Per ulteriori informazioni, leggere quanto segue [!DNL Marketo] documenti:

* [Creare un flusso di dati da acquisire [!DNL Marketo] dati da Experience Platform](../../../tutorials/ui/create/adobe-applications/marketo.md).
* [Guida alla mappatura dei campi](../mapping/marketo.md).