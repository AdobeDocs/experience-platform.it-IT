---
title: Dettagli membro sanitario Schema Field Group
description: Questo documento fornisce una panoramica del gruppo di campi schema Dettagli membri sanitari.
source-git-commit: a51079ff1686ecae3e5fe9f0170b28bc16bcef86
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 3%

---

# [!UICONTROL Dettagli dei membri del settore sanitario] gruppo di campi schema

[!UICONTROL Dettagli dei membri del settore sanitario] è un gruppo di campi di schema standard per [[!DNL XDM Individual Profile] Classe](../../classes/individual-profile.md) che acquisisce i dettagli di una persona che ha o riceverà assistenza medica o cure, ad esempio informazioni di contatto, medico primario e informazioni di piano.

![Struttura del gruppo di campi](../../images/field-groups/healthcare-member-details/structure.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `billingAddress` | [[!UICONTROL Indirizzo postale]](../../data-types/postal-address.md) | Indirizzo di fatturazione della persona. |
| `faxPhone` | [[!UICONTROL Numero di telefono]](../../data-types/phone-number.md) | Il numero di fax della persona. |
| `homeAddress` | [[!UICONTROL Indirizzo postale]](../../data-types/postal-address.md) | L&#39;indirizzo di casa della persona. |
| `homePhone` | [[!UICONTROL Numero di telefono]](../../data-types/phone-number.md) | Il numero di telefono di casa della persona. |
| `mailingAddress` | [[!UICONTROL Indirizzo postale]](../../data-types/postal-address.md) | Indirizzo postale della persona. |
| `memberDetails` | Oggetto | Oggetto che contiene informazioni dettagliate sugli attributi e le relazioni della persona in relazione all&#39;assistenza sanitaria. Consulta la sezione [sottosezione](#memberDetails) per ulteriori informazioni sulla struttura dell&#39;oggetto. |
| `mobilePhone` | [[!UICONTROL Numero di telefono]](../../data-types/phone-number.md) | Il numero di cellulare della persona. |
| `person` | [[!UICONTROL Utente]](../../data-types/person.md) | Un singolo attore, contatto o proprietario collegato all&#39;appartenenza all&#39;assistenza sanitaria della persona. |
| `personalEmail` | [[!UICONTROL Indirizzo e-mail]](../../data-types/email-address.md) | Indirizzo e-mail personale della persona. |
| `shippingAddress` | [[!UICONTROL Indirizzo postale]](../../data-types/postal-address.md) | L&#39;indirizzo di spedizione della persona. |

{style=&quot;table-layout:auto&quot;}

## `memberDetails` {#memberDetails}

`memberDetails` è un oggetto che contiene informazioni dettagliate sugli attributi e le relazioni della persona in relazione all&#39;assistenza sanitaria. La struttura `memberDetails` è descritto di seguito.

![struttura MemberDetails](../../images/field-groups/healthcare-member-details/memberDetails.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `emergencyContact` | Oggetto | Acquisisce i seguenti dati di contatto di emergenza per la persona: <ul><li>`fullName`: (Stringa) Nome completo del contatto di emergenza.</li><li>`phone`: (Stringa) Il numero di telefono del contatto di emergenza.</li><li>`relationshipToMember`: (Stringa) Il rapporto del contatto di emergenza con la persona.</li></ul> |
| `medications` | Array di oggetti | Elenca i dettagli dei farmaci presenti e passati associati alla persona. Ogni elemento array è un oggetto che acquisisce i seguenti dettagli: <ul><li>`refillLocation`: ([[!UICONTROL Indirizzo postale]](../../data-types/postal-address.md)) Posizione di ricarica del farmaco.</li><li>`ID`: (Stringa) ID farmaco.</li><li>`isCurrent`: (Booleano) Indica se il farmaco è corrente o passato.</li><li>`numberOfRefills`: (Intero) Il numero di ricariche prescritte dal fornitore del farmaco.</li><li>`startDate`: (DataOra) La data in cui la persona ha iniziato a prendere il farmaco.</li></ul> |
| `multipleBirth` | Oggetto | Acquisisce i dettagli relativi alle nascite multiple: <ul><li>`isMultipleBirth`: (Booleano) Indica se la persona ha dato più nascite.</li><li>`multipleBirthNumber`: (Numero intero) Il numero di neonati se `isMultipleBirth` è vero.</li></ul> |
| `plans` | Array di oggetti | Elenca i dettagli dei piani medici attuali e passati associati alla persona. Ogni elemento array è un oggetto che acquisisce i seguenti dettagli: <ul><li>`coverageEndDate`: (DateTime) La data in cui termina la copertura del piano.</li><li>`coverageStartDate`: (DateTime) Data di inizio della copertura del piano.</li><li>`isActive`: (Booleano) Indica se il piano è attivo.</li><li>`planId`: (Stringa) L&#39;ID del piano.</li></ul> |
| `primaryCarePhysicians` | Array di oggetti | Elenca i dettagli dei medici di base associati alla persona. Ogni elemento array è un oggetto che acquisisce i seguenti dettagli: <ul><li>`endDate`: (DateTime) La data in cui il medico della cura primaria ha terminato la cura della persona.</li><li>`fullname`: (Stringa) Nome completo del medico.</li><li>`providerId`: (Stringa) Identificatore univoco del medico.</li><li>`startDate`: (DateTime) La data in cui il medico della cura primaria ha iniziato a prendersi cura della persona.</li></ul> |
| `specialists` | Array di oggetti | Elenca i dettagli degli specialisti sanitari associati alla persona. Ogni elemento array è un oggetto che acquisisce i seguenti dettagli: <ul><li>`fullname`: (Stringa) Nome completo dello specialista.</li><li>`providerId`: (Stringa) Un identificatore univoco per lo specialista.</li><li>`specialty`: (Stringa) La specialità del fornitore (ad esempio anestesia, urologia, radiologia, dermatologia e così via).</li></ul> |
| `beneficiaryRelationship` | Stringa | Il rapporto beneficiario con l&#39;operatore sanitario se la persona è dipendente (ad esempio se stessa, il coniuge, il figlio e così via). |
| `billingAccountID` | Stringa | Identificatore univoco per l&#39;account di fatturazione della persona. |
| `dateAgeCollected` | DateTime | Data di raccolta dell&#39;età della persona. |
| `deceasedDate` | DateTime | La data in cui la persona è morta se è deceduta. |
| `isDeceased` | Booleano | Indica se la persona è deceduta. |
| `isDependent` | Booleano | Indica se la persona è dipendente. |
| `nationality` | Stringa | Il rapporto giuridico tra la persona e il suo stato, rappresentato utilizzando il codice Alpha-2 ISO 3166-1. |
| `preferredAvailability` | Stringa | La disponibilità di giorno e ora preferita della persona per un appuntamento. |
| `primaryMemberID` | Stringa | Identificatore univoco dell&#39;utente con sottoscrizione principale se la persona è dipendente. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.schema.json)

Per ulteriori informazioni su come utilizzare questo gruppo di campi per servire comuni, consulta la documentazione dello schema del settore [casi d&#39;uso del settore sanitario](../../schema/industries/healthcare.md).
