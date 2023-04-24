---
keywords: Experience Platform;home;argomenti popolari;controllo accessi;controllo accessi basato su attributi;
title: Guida end-to-end per il controllo dell'accesso basato su attributi
description: Questo documento fornisce una guida end-to-end sul controllo degli accessi basato su attributi in Adobe Experience Platform
exl-id: 7e363adc-628c-4a66-a3bd-b5b898292394
source-git-commit: 004f6183f597132629481e3792b5523317b7fb2f
workflow-type: tm+mt
source-wordcount: '1726'
ht-degree: 19%

---

# Guida end-to-end per il controllo degli accessi basato su attributi

Il controllo dell&#39;accesso basato su attributi è una funzionalità di Adobe Experience Platform che offre ai clienti multi-brand e a tutela della privacy una maggiore flessibilità per gestire l&#39;accesso degli utenti. È possibile concedere o negare l’accesso a singoli oggetti, ad esempio campi e segmenti dello schema, con criteri basati sugli attributi e sul ruolo dell’oggetto. Questa funzione ti consente di concedere o revocare l’accesso a singoli oggetti per utenti Platform specifici della tua organizzazione.

Questa funzionalità ti consente di classificare campi dello schema, segmenti e così via con etichette che definiscono ambiti di utilizzo organizzativi o dati. Puoi applicare queste stesse etichette a percorsi, offerte e altri oggetti in Adobe Journey Optimizer. In parallelo, gli amministratori possono definire i criteri di accesso ai campi dello schema Experience Data Model (XDM) e gestire meglio gli utenti o i gruppi (utenti interni, esterni o di terze parti) a cui possono accedere.

>[!NOTE]
>
>Questo documento si concentra sul caso d&#39;uso delle politiche di controllo degli accessi. Se stai cercando di impostare criteri per governare il **use** dei dati anziché a quali utenti di Platform hanno accesso, consulta la guida end-to-end in [governance dei dati](../../data-governance/e2e.md) invece.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../xdm/home.md): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
   * [Nozioni di base sulla composizione dello schema](../../xdm/schema/composition.md): Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’Editor di schema](../../xdm/tutorials/create-schema-ui.md): Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [Servizio di segmentazione di Adobe Experience Platform](../../segmentation/home.md): Il motore di segmentazione in [!DNL Platform] utilizzato per creare segmenti di pubblico dai profili cliente in base ai comportamenti e agli attributi dei clienti.

### Panoramica del caso d’uso

È disponibile un esempio di flusso di lavoro per il controllo degli accessi basato su attributi, in cui puoi creare e assegnare ruoli, etichette e criteri per configurare se gli utenti possono o meno accedere a risorse specifiche dell’organizzazione. Questa guida utilizza un esempio di limitazione dell’accesso ai dati sensibili per illustrare il flusso di lavoro. Questo caso d’uso è descritto di seguito:

Sei un fornitore di servizi sanitari e vuoi configurare l’accesso alle risorse della tua organizzazione.

* Il team di marketing interno deve essere in grado di accedere a **[!UICONTROL PHI/Dati sanitari regolamentati]** dati.
* La tua agenzia esterna non dovrebbe essere in grado di accedere **[!UICONTROL PHI/Dati sanitari regolamentati]** dati.

A questo scopo, devi configurare ruoli, risorse e criteri.

Sarà possibile:

* [Etichettare i ruoli per gli utenti](#label-roles): Utilizzare l&#39;esempio di un fornitore di assistenza sanitaria (ACME Business Group) il cui gruppo di marketing lavora con agenzie esterne.
* [Etichettare le risorse (campi e segmenti di schema)](#label-resources): Assegna **[!UICONTROL PHI/Dati sanitari regolamentati]** alle risorse e ai segmenti dello schema.
* 
   * [Attiva il criterio che li collegherà: ](#policy): Abilita i criteri predefiniti per impedire l’accesso ai campi e ai segmenti dello schema connettendo le etichette delle risorse alle etichette del tuo ruolo. Gli utenti con etichette corrispondenti avranno quindi accesso al campo dello schema e al segmento in tutte le sandbox.

## Autorizzazioni

[!UICONTROL Autorizzazioni] è l’area di Experience Cloud in cui gli amministratori possono definire ruoli utente e criteri per gestire le autorizzazioni per funzioni e oggetti all’interno di un’applicazione di prodotto.

Attraverso [!UICONTROL Autorizzazioni], puoi creare e gestire i ruoli e assegnare le autorizzazioni di risorse desiderate per questi ruoli. [!UICONTROL Le autorizzazioni ti consentono inoltre di gestire le etichette, le sandbox e gli utenti associati a un ruolo specifico.]

Se non disponi di privilegi di amministratore, contatta l’amministratore di sistema per ottenere l’accesso.

Una volta disponibili i privilegi di amministratore, vai a [Adobe Experience Cloud](https://experience.adobe.com/) e accedi utilizzando le tue credenziali Adobe. Una volta effettuato l&#39;accesso, il **[!UICONTROL Panoramica]** viene visualizzata la pagina della tua organizzazione per la quale disponi dei privilegi di amministratore. Questa pagina mostra i prodotti a cui l’organizzazione è abbonata, insieme ad altri controlli per aggiungere utenti e amministratori all’organizzazione. Seleziona **[!UICONTROL Autorizzazioni]** per aprire l’area di lavoro per l’integrazione con Platform.

![Immagine che mostra il prodotto Autorizzazioni selezionato in Adobe Experience Cloud](../images/flac-ui/flac-select-product.png)

Viene visualizzata l’area di lavoro Autorizzazioni per l’interfaccia utente di Platform, che si apre nella **[!UICONTROL Ruoli]** pagina.

## Applicare etichette a un ruolo {#label-roles}

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about"
>title="Cosa sono le etichette?"
>abstract="Le etichette consentono di classificare set di dati e campi in base ai criteri di utilizzo applicati a tali dati. Platform fornisce diverse etichette di utilizzo dei dati principali definite da Adobe, che coprono un’ampia gamma di restrizioni comuni applicabili alla governance dei dati. Ad esempio, le etichette “S” per dati sensibili (ad esempio, dati RHD, Regulated Health Data) consentono di classificare i dati che fanno riferimento a informazioni sanitarie protette (PHI, Protected Health Information). Puoi anche definire etichette personalizzate che soddisfino le esigenze della tua organizzazione."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=it#understanding-data-usage-labels" text="Panoramica delle etichette di utilizzo dei dati"

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about_create"
>title="Creare una nuova etichetta"
>abstract="Puoi creare etichette personalizzate per adattarle alle esigenze della tua organizzazione. Le etichette personalizzate possono essere utilizzate per applicare ai dati sia le configurazioni di governance dei dati che di controllo degli accessi."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=it#manage-labels" text="Gestire le etichette personalizzate"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about"
>title="Cosa sono i ruoli?"
>abstract="I ruoli consentono di classificare i tipi di utenti che interagiscono con l’istanza Platform e sono elementi fondamentali nei criteri di controllo degli accessi. Un ruolo dispone di un determinato set di autorizzazioni e i membri dell’organizzazione possono essere assegnati a uno o più ruoli, a seconda dell’ambito di accesso di visualizzazione o scrittura necessario."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=it" text="Gestire i ruoli"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about_create"
>title="Creare un nuovo ruolo"
>abstract="Puoi creare un nuovo ruolo per classificare meglio gli utenti che accedono all’istanza Platform. Ad esempio, puoi creare un ruolo per un gruppo marketing interno e applicare l’etichetta RHD a tale ruolo, consentendo al gruppo di accedere a informazioni sanitarie protette (PHI). In alternativa, puoi anche creare un ruolo per un ente esterno e negargli l’accesso ai dati PHI non applicando l’etichetta RHD a quel ruolo."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=it#create-a-new-role" text="Creare un nuovo ruolo"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_details"
>title="Panoramica del ruolo"
>abstract="Nella finestra di dialogo della panoramica del ruolo vengono visualizzate le risorse e le sandbox a cui un determinato ruolo può accedere."

I ruoli sono modi per classificare i tipi di utenti che interagiscono con la tua istanza di Platform e sono blocchi costitutivi dei criteri di controllo degli accessi. Un ruolo dispone di un determinato set di autorizzazioni e i membri dell’organizzazione possono essere assegnati a uno o più ruoli, a seconda dell’ambito di accesso di cui hanno bisogno.

Per iniziare, seleziona **[!UICONTROL ACME Business Group]** dal **[!UICONTROL Ruoli]** pagina.

![Immagine che mostra il ruolo aziendale ACME selezionato in Ruoli](../images/abac-end-to-end-user-guide/abac-select-role.png)

Quindi, seleziona **[!UICONTROL Etichette]** quindi seleziona **[!UICONTROL Aggiungi etichette]**.

![Immagine che mostra Aggiungi etichette selezionate nella scheda Etichette](../images/abac-end-to-end-user-guide/abac-select-add-labels.png)

Viene visualizzato un elenco di tutte le etichette dell’organizzazione. Seleziona **[!UICONTROL RHD]** per aggiungere l’etichetta **[!UICONTROL PHI/Dati sanitari regolamentati]**. Lasciare che accanto all’etichetta venga visualizzato un segno di spunta blu, quindi selezionare **[!UICONTROL Salva]**.

![Immagine che mostra l’etichetta RHD selezionata e salvata](../images/abac-end-to-end-user-guide/abac-select-role-label.png)

>[!NOTE]
>
>Quando aggiungi un gruppo di organizzazioni a un ruolo, tutti gli utenti di tale gruppo verranno aggiunti al ruolo . Eventuali modifiche al gruppo dell&#39;organizzazione (utenti rimossi o aggiunti) verranno aggiornate automaticamente all&#39;interno del ruolo .

## Applicare etichette ai campi dello schema {#label-resources}

Ora che hai configurato un ruolo utente con il [!UICONTROL RHD] etichetta, il passaggio successivo consiste nell’aggiungere la stessa etichetta alle risorse che si desidera controllare per quel ruolo.

Seleziona **[!UICONTROL Schemi]** dalla navigazione a sinistra, quindi seleziona **[!UICONTROL Medicale ACME]** dall’elenco degli schemi visualizzati.

![Immagine che mostra lo schema ACME Healthcare selezionato dalla scheda Schemi](../images/abac-end-to-end-user-guide/abac-select-schema.png)

Quindi, seleziona **[!UICONTROL Etichette]** per visualizzare un elenco dei campi associati allo schema. Da qui è possibile assegnare etichette a uno o più campi contemporaneamente. Seleziona la **[!UICONTROL Glucosio nel sangue]** e **[!UICONTROL LivelloInsulina]** campi, quindi selezionare **[!UICONTROL Applicare etichette di accesso e governance dei dati]**.

![Immagine che mostra la selezione di BloodGlucosio e InsulinLevel e applica le etichette di accesso e governance dei dati selezionate](../images/abac-end-to-end-user-guide/abac-select-schema-labels-tab.png)

La **[!UICONTROL Modificare le etichette]** viene visualizzata una finestra di dialogo che consente di scegliere le etichette da applicare ai campi dello schema. Per questo caso d’uso, seleziona la **[!UICONTROL PHI/Dati sanitari regolamentati]** etichetta, quindi seleziona **[!UICONTROL Salva]**.

![Immagine che mostra l’etichetta RHD selezionata e salvata](../images/abac-end-to-end-user-guide/abac-select-schema-labels.png)

>[!NOTE]
>
>Quando un’etichetta viene aggiunta a un campo, l’etichetta viene applicata alla risorsa principale del campo (classe o gruppo di campi). Se la classe o il gruppo di campi padre è utilizzato da altri schemi, questi schemi erediteranno la stessa etichetta.

## Applicare etichette ai segmenti

Una volta completata l’etichettatura dei campi dello schema, puoi iniziare a etichettare i segmenti.

Seleziona **[!UICONTROL Segmenti]** dalla navigazione a sinistra. Viene visualizzato un elenco dei segmenti disponibili nell’organizzazione. In questo esempio, i due segmenti seguenti devono essere etichettati in quanto contengono dati di integrità sensibili:

* Glucosio nel sangue >100
* Insulina &lt;50

Seleziona **[!UICONTROL Glucosio nel sangue >100]** per iniziare a etichettare il segmento.

![Immagine che mostra il glucosio nel sangue >100 selezionato dalla scheda Segmenti](../images/abac-end-to-end-user-guide/abac-select-segment.png)

Il segmento **[!UICONTROL Dettagli]** viene visualizzata la schermata . Seleziona **[!UICONTROL Gestisci accesso]**.

![Immagine che mostra la selezione di Gestione accesso](../images/abac-end-to-end-user-guide/abac-segment-fields-manage-access.png)

La **[!UICONTROL Modificare le etichette]** viene visualizzata una finestra di dialogo che consente di scegliere le etichette da applicare al segmento. Per questo caso d’uso, seleziona la **[!UICONTROL PHI/Dati sanitari regolamentati]** etichetta, quindi seleziona **[!UICONTROL Salva]**.

![Immagine che mostra la selezione dell’etichetta RHD e il salvataggio selezionato](../images/abac-end-to-end-user-guide/abac-select-segment-labels.png)

Ripeti i passaggi precedenti con **[!UICONTROL Insulina &lt;50]**.

## Attivare il criterio di controllo accessi {#policy}

Il criterio di controllo accessi predefinito sfrutterà le etichette per definire quali ruoli utente hanno accesso a risorse specifiche di Platform. In questo esempio, l’accesso ai campi e ai segmenti dello schema verrà negato in tutte le sandbox agli utenti che non si trovano in un ruolo con le etichette corrispondenti nel campo dello schema.

Per attivare il criterio di controllo accessi, selezionare [!UICONTROL Autorizzazioni] dalla navigazione a sinistra, quindi seleziona **[!UICONTROL Criteri]**.

![Elenco dei criteri visualizzati](../images/abac-end-to-end-user-guide/abac-policies-page.png)

Quindi, seleziona i puntini di sospensione (`...`) accanto al nome dei criteri e un elenco a discesa visualizza i controlli per modificare, attivare, eliminare o duplicare il ruolo. Seleziona **[!UICONTROL Attiva]** dal menu a discesa .

![Menu a discesa per attivare i criteri](../images/abac-end-to-end-user-guide/abac-policies-activate.png)

Viene visualizzata la finestra di dialogo attiva criterio che richiede di confermare l’attivazione. Seleziona **[!UICONTROL Conferma]**.

![Finestra di dialogo Attiva criterio](../images/abac-end-to-end-user-guide/abac-activate-policies-dialog.png)

Viene ricevuta la conferma dell’attivazione dei criteri e vieni restituito al [!UICONTROL Criteri] pagina.

![Attiva conferma criteri](../images/abac-end-to-end-user-guide/abac-policies-confirm-activate.png)

<!-- ## Create an access control policy {#policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="What are policies?"
>abstract="Policies are statements that bring attributes together to establish permissible and impermissible actions. Every organization comes with a default policy that you must activate to define rules for resources like segments and schema fields. Default policies can neither be edited nor deleted. However, default policies can be activated or deactivated."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en" text="Manage policies"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about_create"
>title="Create a policy"
>abstract="Create a policy to define the actions that your users can and cannot take against your segments and schema fields."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en#create-a-new-policy" text="Create a policy"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_permitdeny"
>title="Configure permissible and impermissible actions for a policy"
>abstract="A <b>deny access to</b> policy will deny users access when the criteria is met. Combined with <b>The following being false</b> - all users will be denied access unless they meet the matching criteria set. This type of policy allows you to protect a sensitive resource and only allow access to users with matching labels. <br>A <b>permit access to</b> policy will permit users access when the criteria are met. When combined with <b>The following being true</b> - users will be given access if they meet the matching criteria set. This does not explicitly deny access to users, but adds a permit access. This type of policy allows you to give additional access to resource and in addition to those users who might already have access through role permissions."</br>
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en#edit-a-policy" text="Edit a policy"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_resource"
>title="Configure permissions for a resource"
>abstract="A resource is the asset or object that a user can or cannot access. Resources can be segments or schemas fields. You can configure write, read, or delete permissions for segments and schema fields."

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_condition"
>title="Edit conditions"
>abstract="Apply conditional statements to your policy to configure user access to certain resources. Select match all to require users to have roles with the same labels as a resource to be permitted access. Select match any to require users to have a role with just one label matching a label on a resource. Labels can either be defined as core or custom labels, with core labels representing labels created and provided by Adobe and custom labels representing labels that you created for your organization."

Access control policies leverage labels to define which user roles have access to specific Platform resources. Policies can either be local or global and can override other policies. In this example, access to schema fields and segments will be denied in all sandboxes for users who don't have the corresponding labels in the schema field.

>[!NOTE]
>
>A "deny policy" is created to grant access to sensitive resources because the role grants permission to the subjects. The written policy in this example **denies** you access if you are missing the required labels.

To create an access control policy, select **[!UICONTROL Permissions]** from the left navigation and then select **[!UICONTROL Policies]**. Next, select **[!UICONTROL Create policy]**.

![Image showing Create policy being selected in the Permissions](../images/abac-end-to-end-user-guide/abac-create-policy.png)

The **[!UICONTROL Create new policy]** dialog appears, prompting you to enter a name and an optional description. Select **[!UICONTROL Confirm]** when finished.

![Image showing the Create new policy dialog and selecting Confirm](../images/abac-end-to-end-user-guide/abac-create-policy-details.png)

To deny access to the schema fields, use the dropdown arrow and select **[!UICONTROL Deny access to]** and then select **[!UICONTROL No resource selected]**. Next, select **[!UICONTROL Schema Field]** and then select **[!UICONTROL All]**.

![Image showing Deny access and resources selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema.png)

The table below shows the conditions available when creating a policy:

| Conditions | Description |
| --- | --- |
| The following being false| When 'Deny access to' is set, access will be restricted if the user does not meet the criteria selected. |
| The following being true| When 'Permit access to' is set, access will be permitted if the user meets the selected criteria. |
| Matches any| The user has a label that matches any label applied to a resource. |
| Matches all| The user has all labels that matches all labels applied to a resource. |
| Core label| A core label is an Adobe-defined label that is available in all Platform instances.|
| Custom label| A custom label is a label that has been created by your organization.|

Select **[!UICONTROL The following being false]** and then select **[!UICONTROL No attribute selected]**. Next, select the user **[!UICONTROL Core label]**, then select **[!UICONTROL Matches all]**. Select the resource **[!UICONTROL Core label]** and finally select **[!UICONTROL Add resource]**.

![Image showing the conditions being selected and Add resource being selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema-expression.png)

>[!TIP]
>
>A resource is the asset or object that a subject can or cannot access. Resources can be segments or schemas.

To deny access to the segments, use the dropdown arrow and select **[!UICONTROL Deny access to]** and then select **[!UICONTROL No resource selected]**. Next, select **[!UICONTROL Segment]** and then select **[!UICONTROL All]**.

Select **[!UICONTROL The following being false]** and then select **[!UICONTROL No attribute selected]**. Next, select the user **[!UICONTROL Core label]**, then select **[!UICONTROL Matches all]**. Select the resource **[!UICONTROL Core label]** and finally select **[!UICONTROL Save]**.

![Image showing conditions selected and Save being selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-segment.png)

Select **[!UICONTROL Activate]** to activate the policy, and a dialog appears which prompts you to confirm activation. Select **[!UICONTROL Confirm]** and then select **[!UICONTROL Close]**.

![Image showing the Policy being activated ](../images/abac-end-to-end-user-guide/abac-create-policy-activation.png) -->

## Passaggi successivi

È stata completata l’applicazione di etichette a un ruolo, campi di schema e segmenti. All’agenzia esterna assegnata a questi ruoli è impedito di visualizzare queste etichette e i relativi valori nello schema, nel set di dati e nella visualizzazione del profilo. A questi campi è inoltre impedito di essere utilizzati nella definizione del segmento quando si utilizza il Generatore di segmenti.

Per ulteriori informazioni sul controllo degli accessi basato su attributi, consulta la sezione [panoramica sul controllo dell&#39;accesso basato sugli attributi](./overview.md).
