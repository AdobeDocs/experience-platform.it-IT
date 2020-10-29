---
product: experience-platform
audience: user
user-guide-title: Guida al sistema Experience Data Model (XDM)
breadcrumb-title: Guida a Data Model (XDM)
user-guide-description: Utilizza le classi e i mixin Experience Data Model (XDM) per standardizzare i dati dell’esperienza.
translation-type: tm+mt
source-git-commit: 0a5b6bab6a0a11a572a4cd5de95b33f8d61d34bc
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 18%

---


# Experience Data Model (XDM) System {#xdm}

* [Panoramica del sistema XDM](home.md)
* Schemi {#schema}
   * [Nozioni di base sulla composizione dello schema](schema/composition.md)
   * [Best practice per la modellazione dei dati](schema/best-practices.md)
   * [Vincoli del tipo di campo XDM](schema/field-constraints.md)
   * [Dizionario campo XDM](schema/field-dictionary.md)
   * Casi di utilizzo dello schema {#use-cases}
      * [Mixina di consenso sulla privacy](schema/privacy-consent.md)
* Classi {#classes}
   * [Profilo singolo XDM](./classes/individual-profile.md)
   * [XDM ExperienceEvent](./classes/experienceevent.md)
* Mixin {#mixins}
   * Mixine profilo {#profile}
      * [IdentityMap](./mixins/profile/identitymap.md)
      * [Dettagli demografici](./mixins/profile/person-details.md)
      * [Dettagli contatto personale](./mixins/profile/personal-details.md)
      * [Dettagli iscrizione segmento](./mixins/profile/segmentation.md)
      * [Dettagli contatto di lavoro](./mixins/profile/work-details.md)
   * Mixins evento {#event}
      * [Dettagli ID utente finale](./mixins/event/enduserids.md)
      * [Dettagli ambiente](./mixins/event/environment-details.md)
   * [Aggiornamenti dei nomi misti](./mixins/name-updates.md)
* Tipi di dati {#data-types}
   * [Beacon](./data-types/beacon.md)
   * [Dettagli del browser](./data-types/browser-details.md)
   * [Dispositivo](./data-types/device.md)
   * [Indirizzo e-mail](./data-types/email-address.md)
   * [Ambiente](./data-types/environment.md)
   * [Geo](./data-types/geo.md)
   * [Cerchio geografico](./data-types/geo-circle.md)
   * [Coordinate geografiche](./data-types/geo-coordinates.md)
   * [Dettagli interazione geografica](./data-types/geo-interaction-details.md)
   * [Forma geografica](./data-types/geo-shape.md)
   * [Identità](./data-types/identity.md)
   * [Nome della persona](./data-types/person-name.md)
   * [Numero di telefono](./data-types/phone-number.md)
   * [Inserisci contesto](./data-types/place-context.md)
   * [Dettagli POI](./data-types/poi-details.md)
   * [Interazione POI](./data-types/poi-interaction.md)
   * [Indirizzo postale](./data-types/postal-address.md)
* API del Registro di sistema dello schema {#api}
   * [Introduzione](api/getting-started.md)
   * [Elenco delle risorse](api/list-resources.md)
   * [Cercare una risorsa](api/look-up-resource.md)
   * [Aggiornare una risorsa](api/update-resource.md)
   * [Sostituire una risorsa](api/replace-resource.md)
   * [Elimina una risorsa](api/delete-resource.md)
   * [Creazione di una classe](api/create-class.md)
   * [Creare un mixin](api/create-mixin.md)
   * [Creazione di un tipo di dati](api/create-data-type.md)
   * [Creare uno schema](api/create-schema.md)
   * [Unioni](api/unions.md)
   * [Descrittori](api/descriptors.md)
   * [Schemi ad hoc](api/ad-hoc.md)
   * [Appendice](api/appendix.md)
* Tutorial {#tutorials}
   * [Creare uno schema (API)](tutorials/create-schema-api.md)
   * [Creare uno schema (interfaccia utente)](tutorials/create-schema-ui.md)
   * [Definire una relazione tra due schemi (API)](tutorials/relationship-api.md)
   * [Definire una relazione tra due schemi (interfaccia utente)](tutorials/relationship-ui.md)
   * [Creare uno schema ad hoc (API)](tutorials/ad-hoc.md)
* [Guida alla risoluzione dei problemi](troubleshooting-guide.md)
* [Riferimento API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)
* [Note sulla versione della piattaforma](https://www.adobe.com/go/platform-release-notes-en)