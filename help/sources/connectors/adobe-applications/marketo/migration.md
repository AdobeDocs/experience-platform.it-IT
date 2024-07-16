---
title: Migrare la mappatura ECID da persona ad attività utilizzando l’origine Marketo Engage
description: Scopri come migrare la mappatura ECID dal set di dati persona al set di dati attività utilizzando l’origine Marketo Engage.
exl-id: bcc91c53-aeca-4d7c-89b5-cf025d0357a0
source-git-commit: d03fcf06fb63ad2484ded3b85fc11ae45661babc
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# Migra mapping ECID da set di dati [!DNL Person] a set di dati [!DNL Activity]

È possibile migrare la mappatura ECID dal set di dati [!DNL Marketo Engage Person] al set di dati [!DNL Activity] per fornire un comportamento più stabile di acquisizione dei dati e gestione delle identità. Inoltre, questa migrazione tratta i seguenti argomenti:

| Problema | Soluzione |
| --- | --- |
| Se il set di dati [!DNL Marketo Person] contiene collegamenti a più ECID, l&#39;acquisizione dei dati non riesce se il numero totale di identità [ in un record Experience Data Model (XDM) supera il 20](../../../../identity-service/guardrails.md). | Migrando la mappatura del campo ECID a [!DNL Activity], puoi garantire che il numero di identità dal flusso di dati [!DNL Marketo Person] rimanga entro il limite e quindi consentire l&#39;acquisizione dei dati. |
| Ogni volta che il set di dati [!DNL Marketo Person] viene acquisito con ECID, la marca temporale in tutti gli ECID del set di dati [!DNL Marketo Person] viene aggiornata con l&#39;ultima marca temporale aggiornata del record Persona. Ciò potrebbe comportare l&#39;eliminazione [errata di identità più recenti dal grafo delle identità](../../../../identity-service/guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated). | Migrando le mappature dei campi ECID a [!DNL Activity], Identity Service può riflettere correttamente la marca temporale di ECID e il meccanismo &quot;first in first out&quot; di Identity Service fornirà un comportamento più stabile. |
| Quando gli ECID vengono acquisiti tramite il flusso di dati [!DNL Marketo Person], i nuovi ECID aggiunti non vengono acquisiti in Experience Platform a meno che non siano presenti aggiornamenti al record [!DNL Person] in [!DNL Marketo]. | Quando un nuovo ECID è collegato al record [!DNL Person] in [!DNL Marketo], puoi acquisire i dati ECID tramite un flusso di dati [!DNL Marketo Activity] e richiedere immediatamente un aggiornamento del grafo delle identità all&#39;Experience Platform. |

In sostanza, devi:

* Aggiorna il flusso di dati [!DNL Marketo Activity].
* Aggiorna il flusso di dati [!DNL Marketo Person].

## Aggiorna flusso di dati [!DNL Marketo Activity] {#update-activity-dataflow}

Per aggiornare il flusso di dati di [!DNL Marketo Activity], attenersi alla procedura seguente:

* Nell&#39;interfaccia utente di Experience Platform, passa all&#39;area di lavoro *Sources* e trova il flusso di dati esistente per i dati [!DNL Marketo Activity].
* Dato che il flusso di dati è abilitato, seleziona i puntini di sospensione (`...`) accanto al nome del flusso di dati, quindi seleziona **[!UICONTROL Aggiorna flusso di dati]**.
* Quindi, seleziona **[!UICONTROL Avanti]** fino a raggiungere l&#39;interfaccia *Mapping*.
* Nell&#39;interfaccia *Mapping*, selezionare **[!UICONTROL Nuovo campo]**, quindi **[!UICONTROL Aggiungi campo calcolato]**. Da qui, devi aggiungere quanto segue:

| Set di dati di Source | Campo di destinazione XDM |
| --- | --- |
| `iif(${web\.ecid} != null, to_object('ECID', arrays_to_objects('id', explode(last(split(${web\.ecid}, ":")), " "))), null)` | `identityMap` |

>[!NOTE]
>
>Se l&#39;aggiornamento a un flusso di dati [!DNL Marketo] esistente consiste solo nell&#39;aggiunta o nella rimozione del campo di mappatura ECID, il flusso di dati ignora automaticamente il processo di retrocompilazione dello storico. L’acquisizione di nuovi dati si verifica solo quando si verificano tipi di attività come &quot;visita la pagina web&quot; e &quot;fai clic sulla pagina web&quot;.

## Aggiorna flusso di dati [!DNL Marketo Person] {#update-person-dataflow}

Per aggiornare il flusso di dati di [!DNL Marketo Person], attenersi alla procedura seguente:

* Nell&#39;interfaccia utente di Experience Platform, passa all&#39;area di lavoro *Sources* e trova il flusso di dati esistente per i dati [!DNL Marketo Person].
* Dato che il flusso di dati è abilitato, seleziona i puntini di sospensione (`...`) accanto al nome del flusso di dati, quindi seleziona **[!UICONTROL Aggiorna flusso di dati]**.
* Quindi, seleziona **[!UICONTROL Avanti]** fino a raggiungere l&#39;interfaccia *Mapping*.
* Nell&#39;interfaccia *Mapping*, rimuovere il campo calcolato associato a `identityMap`, quindi selezionare **[!UICONTROL Next]** e **[!UICONTROL Save &amp; Ingest]**.

>[!NOTE]
>
>Se l&#39;aggiornamento a un flusso di dati [!DNL Marketo] esistente consiste solo nell&#39;aggiunta o nella rimozione del campo di mappatura ECID, il flusso di dati ignora automaticamente il processo di retrocompilazione dello storico. La marca temporale degli ECID precedentemente acquisiti rimarrà invariata. Vengono aggiornati solo quando vengono acquisiti nuovi dati che corrispondono agli ECID esistenti.

## Passaggi successivi

Dopo aver letto questo documento, saprai come migrare la mappatura ECID dal set di dati [!DNL Marketo Person] al set di dati [!DNL Marketo Activity]. Per ulteriori informazioni, leggere i seguenti [!DNL Marketo] documenti:

* [Crea un flusso di dati per acquisire [!DNL Marketo] i dati in Experience Platform](../../../tutorials/ui/create/adobe-applications/marketo.md).
* [Guida alla mappatura dei campi](../mapping/marketo.md).
