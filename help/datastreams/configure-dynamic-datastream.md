---
title: Creare configurazioni di flussi di dati dinamici
description: Scopri come creare configurazioni di flussi di dati dinamici, per indirizzare i dati a vari servizi di Experience Cloud, in base a regole.
hide: true
hidefromtoc: true
badge: label="Beta" type="Informative"
source-git-commit: 86416dc11f92a774cda5d95365d3981a637a5595
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 1%

---


# Creare configurazioni di flussi di dati dinamici

>[!AVAILABILITY]
>
>* L’opzione per definire configurazioni di stream di dati dinamici è attualmente in Beta e disponibile per un numero limitato di clienti. Per ricevere l’accesso a questa funzionalità, contatta il rappresentante del tuo Adobe. La documentazione e le funzionalità sono soggette a modifiche.

Per impostazione predefinita, l&#39;Edge Network di Experience Platform invia tutti gli eventi che raggiungono uno stream di dati a tutti i [servizi](configure.md#add-services) di Experience Cloud che hai abilitato per gli stream di dati. Questo potrebbe non essere sempre il flusso di lavoro ideale per te, a seconda dei casi d’uso.

Le configurazioni dello stream di dati dinamici risolvono questo problema attraverso set di regole configurabili dall’utente che puoi definire per ogni servizio abilitato per lo stream di dati e che determinano quale soluzione Experience Cloud deve ricevere ogni tipo di dati.

## Prerequisiti {#prerequisites}

Per creare una configurazione dinamica per lo stream di dati, è necessario soddisfare due condizioni:

* Devi avere creato *almeno* uno stream di dati con cui lavorare. Per informazioni dettagliate, consulta la documentazione su come [creare uno stream di dati](configure.md).
* È necessario avere *almeno* un servizio Experience Cloud aggiunto allo stream di dati. Per informazioni dettagliate, consulta la documentazione su come [aggiungere un servizio](configure.md#add-services) a uno stream di dati.

Dopo aver creato uno stream di dati e aggiunto un servizio di Experience Cloud, puoi [creare una configurazione dinamica](#create-dynamic-configuration).

## Creare una configurazione dello stream di dati dinamico {#create-dynamic-configuration}

Dopo che hai [creato uno stream di dati](configure.md) e [aggiunto un servizio](configure.md#add-services), segui i passaggi seguenti per aggiungere una configurazione dinamica al servizio.

1. Vai alla pagina **[!UICONTROL Raccolta dati]** > **[!UICONTROL Flussi di dati]** e seleziona lo stream di dati creato.

   ![Immagine dell&#39;interfaccia utente dei flussi di dati con l&#39;elenco dei flussi di dati.](assets/configure-dynamic-datastream/select-datastream.png)

1. Selezionare l&#39;opzione **[!UICONTROL Modifica]** nel servizio per il quale si desidera definire una configurazione dinamica.

   ![Immagine dell&#39;interfaccia utente dei flussi di dati che mostra i servizi aggiunti a un flusso di dati.](assets/configure-dynamic-datastream/select-service.png)

1. Nella pagina **[!UICONTROL Configura]**, selezionare **[!UICONTROL Salva e modifica configurazione dinamica]**.

   ![Immagine dell&#39;interfaccia utente dei flussi di dati che mostra la pagina di configurazione dello stream di dati.](assets/configure-dynamic-datastream/save-and-edit.png)

1. Selezionare **[!UICONTROL Aggiungi configurazione dinamica]**.

   ![Immagine dell&#39;interfaccia utente dei flussi di dati che mostra la configurazione dinamica senza messaggio di regola aggiunta.](assets/configure-dynamic-datastream/add-dynamic-config.png)

1. Dal pannello **[!UICONTROL Risorse]**, trascina e rilascia gli elementi con cui desideri creare la regola sul lato destro della finestra. Puoi combinare più risorse per creare regole complesse.

   Utilizza le opzioni di ogni risorsa, ad esempio **[!UICONTROL è uguale a]**, **[!UICONTROL è diverso da]**, **[!UICONTROL esiste]** e altro per ottimizzare le regole.

   ![Immagine dell&#39;interfaccia utente dei flussi di dati che mostra la regola di configurazione dinamica.](assets/configure-dynamic-datastream/drag-resources.png)

1. Nella sezione **[!UICONTROL Configurazione]**, attiva/disattiva i servizi che desideri abilitare o disabilitare per ogni regola, a seconda che si desideri che i dati vengano inviati a ogni servizio. Se si disattiva l&#39;interruttore, la regola è disabilitata e *tutti i dati* verranno inviati al servizio upstream.

   ![Immagine dell&#39;interfaccia utente dei flussi di dati che mostra la regola di configurazione dinamica.](assets/configure-dynamic-datastream/enable-service.png)

1. Al termine della configurazione delle regole, seleziona **[!UICONTROL Salva]**.

## Considerazioni sulla priorità delle regole {#considerations}

Puoi definire più regole per ogni configurazione dello stream di dati dinamico. Tuttavia, se i dati corrispondono alle condizioni di più regole, viene presa in considerazione solo la prima regola corrispondente nell’elenco e tutte le altre regole corrispondenti vengono ignorate.

Per ottenere il comportamento di indirizzamento dei dati desiderato, presta attenzione all’ordine in cui disponi le regole.

Per configurare l&#39;ordine delle regole, è possibile trascinare e rilasciare le finestre delle regole nell&#39;ordine desiderato.

![GIF che mostra come modificare l&#39;ordine delle regole tramite trascinamento.](assets/configure-dynamic-datastream/move-rules.gif)