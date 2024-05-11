---
title: Creare un filtro data
description: Scopri come filtrare le informazioni personalizzate per data.
source-git-commit: 17ad52864bbca09844c0241b6451e6811bd8f413
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 0%

---

# Creare un filtro data {#create-date-filter}

Per filtrare le informazioni in base alla data, è necessario aggiungere parametri alle query SQL che possono accettare vincoli di data. Questa operazione viene eseguita come parte del flusso di lavoro per la creazione di insight in modalità query pro. Consulta la [documentazione della modalità query pro](#query-pro-mode) per scoprire come immettere SQL per gli approfondimenti.

I parametri di query consentono di lavorare con i dati dinamici in quanto fungono da segnaposto per i valori aggiunti in fase di esecuzione. Questi valori dei segnaposto possono essere aggiornati tramite l’interfaccia utente e consentono agli utenti meno tecnici di aggiornare le informazioni in base a intervalli di date.

Se non conosci i parametri di query, consulta la documentazione per [istruzioni su come implementare query con parametri](../../../../query-service/ui/parameterized-queries.md).

## Applicare un filtro data al dashboard {#apply-date-filter}

Per applicare un filtro data, seleziona **[!UICONTROL Aggiungi filtro]**, quindi **[!UICONTROL Filtro data]** dal menu a discesa della vista dashboard.

![Un dashboard personalizzato con Aggiungi filtro e il relativo menu a discesa evidenziato.](../../../images/customizable-insights/add-filter.png)

## Modifica il codice SQL per includere i parametri di query della data {#include-date-parameters}

Quindi, assicurati che il codice SQL includa i parametri di query per consentire un intervallo di date. Se non sono ancora stati incorporati i parametri di query nell&#39;istruzione SQL, modificare le informazioni per includere tali parametri. Consulta la documentazione per istruzioni su come [modificare un approfondimento](../query-pro-mode.md#edit).

>[!TIP]
>
>Si consiglia di aggiungere `$START_DATE` e `$END_DATE` parametri dell’istruzione SQL in ciascuno dei grafici per i quali si desidera abilitare i filtri di data.

>[!NOTE]
>
>I filtri di data non supportano vincoli di tempo. Il filtro si applica solo agli intervalli di date. Ciò significa che se hai più rapporti in un periodo di 24 ore, non puoi distinguere tra diverse ore all’interno dello stesso giorno. Per questo motivo, si consiglia di assegnare al componente tempo la forma di data.

Se il modello dati o le tabelle che si sta analizzando hanno un componente tempo, è possibile raggruppare i dati per data e quindi applicare questi filtri data.

L&#39;istruzione SQL di esempio seguente illustra come incorporare `$START_DATE` e `$END_DATE` parametri e utilizzi `cast` per inquadrare il componente tempo come una data.

```sql
SELECT Sum(personalization_consent_count) AS Personalization,
       Sum(datacollection_consent_count)  AS Datacollection,
       Sum(datasharing_consent_count)     AS Datasharing
FROM   fact_daily_consent_aggregates f
       INNER JOIN dim_consent_valued
               ON f.consent_value_id = d.consent_value_id
WHERE  f.date BETWEEN Upper(Coalesce(Cast('$START_DATE' AS date), '')) AND Upper
                      (
                             Coalesce(Cast('$END_DATE' AS date), ''))
       AND ( ( Upper(Coalesce($consent_value_filter, '')) IN ( '', 'NULL' ) )
              OR ( f.consent_value_id IN ( $consent_value_filter ) ) )
LIMIT  0; 
```

La schermata seguente evidenzia i vincoli di data incorporati nell’istruzione SQL e le coppie di valori chiave dei parametri della query.

>[!NOTE]
>
>Durante la composizione dell’istruzione in modalità query pro, è necessario fornire valori di esempio per ciascun parametro al fine di eseguire l’istruzione SQL e generare il grafico. I valori di esempio forniti durante la composizione dell’istruzione vengono sostituiti dai valori effettivi selezionati per il filtro data (o globale) in fase di esecuzione.

![Il [!UICONTROL Immetti SQL] con i parametri di data evidenziati nel linguaggio SQL.](../../../images/customizable-insights/sql-date-parameters.png)

## Abilita i parametri di data in ogni informazione approfondita {#enable-date-parameters}

Dopo aver incorporato i parametri appropriati nell’istruzione SQL delle informazioni, `Start_date` e `End_date` le variabili sono ora disponibili come interruttori nel compositore widget. Consulta la [sezione popolamento widget modalità query pro](#populate-widget) per informazioni su come modificare un approfondimento.

Dal compositore widget, seleziona attiva per abilitare `Start_date` e `End_date` parametri.

![Il compositore widget con Start_date e End_date viene evidenziato.](../../../images/customizable-insights/widget-composer-date-filter-toggles.png)

Quindi, seleziona i parametri di query appropriati dai menu a discesa.

![Il compositore widget con il menu a discesa Start_date evidenziato.](../../../images/customizable-insights/widget-composer-date-filter-dropdown.png)

Infine, seleziona **[!UICONTROL Salva e chiudi]** per tornare alla dashboard. I filtri di data sono ora abilitati per tutte le informazioni che hanno parametri di data di inizio e di fine.

## Utilizzare il filtro data

Per utilizzare un filtro data personalizzato, seleziona l’icona del calendario e scegli un inizio e una fine dalla vista del calendario.

>[!IMPORTANT]
>
>La semplice aggiunta di un filtro per data non modificherà i grafici. Devi modificare ciascuna informazione per includere la data di inizio e di fine scelte.

![Un dashboard personalizzato con il calendario del filtro data evidenziato.](../../../images/customizable-insights/date-filter.png)

Dopo aver selezionato un intervallo di date dal dashboard, le informazioni che contengono parametri di data nel codice SQL visualizzeranno le opzioni del filtro data nel compositore widget.

>[!NOTE]
>
>Quando selezioni un intervallo di date sul dashboard, vengono visualizzati i pulsanti per i filtri di date nell’ambito del flusso di lavoro di creazione delle informazioni approfondite.

## Eliminare un filtro data {#delete-date-filter}

Per rimuovere il filtro data, seleziona l’icona Elimina filtro (![Icona Elimina filtro.](../../../images/customizable-insights/delete-filter-icon.png)).

![Dashboard personalizzato con l’icona di eliminazione del filtro evidenziata.](../../../images/customizable-insights/delete-date-filter.png)
