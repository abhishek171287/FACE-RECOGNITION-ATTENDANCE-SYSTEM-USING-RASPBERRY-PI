# FACE-RECOGNITION-ATTENDANCE-SYSTEM-USING-RASPBERRY-PI
## Data Model

```mermaid
classDiagram
    class Allergy{
        -id : String
        -patientId : String
        -display : String
        -reactions : List~String~
        -severity : String
        -Allergy(Builder)
        +getId() String
        +getPatientId() String
        +getDisplay() String
        +getReactions() List~String~
        +getSeverity() String
        +copy() Builder
        +toString() String
        +hashCode() int
        +equals(Object) boolean
        +mapById(Collection~Allergy~) Map~String, Allergy~
        +groupById(Collection~Allergy~) Map~String, List~Allergy~~
        +getIds(Collection~Allergy~) List~String~
        +groupByPatientId(Collection~Allergy~) Map~String, List~Allergy~~
        +getPatientIds(Collection~Allergy~) List~String~
        +groupByReactions(Collection~Allergy~) Map~String, List~Allergy~~
        +getReactions(Collection~Allergy~) List~String~
    }
    
    class Attributes{
        +BEST_ENCNTR_ID_KEY : TypedKey~String~
        +BIRTH_DATE_TIME_WITH_PRECISION_KEY : TypedKey~String~
        +PATIENT_SSN_KEY : TypedKey~String~
        +ABSOLUTE_BIRTH_DATE_TIME_KEY : TypedKey~String~
        +UPDT_CNT_KEY : TypedKey~Long~
        +UPDT_DT_TM_KEY : TypedKey~Calendar~
        -Attributes()
    }
    
    class BirthDateTime{
        -year : Integer
        -month : Short
        -day : Short
        -hour : Byte
        -minute : Byte
        -second : Byte
        -nano : Integer
        -zoneId : String
        -BirthDateTime(Builder)
        -checkValidValue(ChronoField,N) ~N extends Number~
        +getYear() Integer
        +getMonth() Short
        +getDay() Short
        +getHour() Byte
        +getMinute() Byte
        +getSecond() Byte
        +getNano() Integer
        +getZoneId() String
        +toLocalDate() LocalDate
        +toLocalTime() LocalTime
        +toLocalDateTime() LocalDateTime
        +toTimeMillis() Long
        +copy() Builder
        +toString() String
        +hashCode() int
        +equals(Object) boolean
  }
  
    class FamilyContactInfo {
        -id : String
        -patientId : String
        -firstName : String
        -lastName : String
        -relationshipsToPatient : List~String~
        -phones : List~Phone~
        -FamilyContactInfo(Builder)
        +getId() String
        +getPatientId() String
        +getFirstName() String
        +getLastName() String
        +getRelationshipsToPatient() List~String~
        +getPhones() List~Phone~
        +copy() Builder
        +toString() String
        +hashCode() int
        +equals(Object) boolean
        +mapById(Collection~FamilyContactInfo~) Map~String, FamilyContactInfo~
        +groupById(Collection~FamilyContactInfo~) Map~String, List~FamilyContactInfo~~
        +getIds(Collection~FamilyContactInfo~) List~String~
        +groupByPatientId(Collection~FamilyContactInfo~) Map~String, List~FamilyContactInfo~~
        +getPatientIds(Collection~FamilyContactInfo~) List~String~
   }

    class Patient{
        -id : String
        -firstName : String
        -middleName : String
        -lastName : String
        -nameSuffix : String
        -identifiers : List~PatientIdentifier~
        -birthDateTime : BirthDateTime
        -gender : Gender
        -attributes : ContextMap
        -Patient(Builder)
        +getId() String
        +getFirstName() String
        +getMiddleName() String
        +getLastName() String
        +getNameSuffix() String
        +getIdentifiers() List<PatientIdentifier>
        +getBirthDateTime() BirthDateTime
        +getGender() Gender
        +getAttributes() ContextMap
        +copy() Builder
        +toString() String
        +hashCode() int
        +equals(Object) boolean
        +mapById(Collection~Patient~) Map~String, Patient~
        +groupById(Collection~Patient~) Map~String, List~Patient~~
        +getIds(Collection~Patient~) List~String~
        +groupByFirstName(Collection~Patient~) Map~String, List~Patient~~
        +getFirstNames(Collection~Patient~) List~String~
        +groupByMiddleName(Collection~Patient~) Map~String, List~Patient~
        +getMiddleNames(Collection~Patient~) List~String~
        +groupByLastName(Collection~Patient~) Map~String, List~Patient~~
        +getLastNames(Collection~Patient~) List~String~
        +groupByNameSuffix(Collection~Patient~) Map~String, List~Patient~~
        +getNameSuffixes(Collection~Patient~) List~String~
        +mapByIdentifiers(Collection~Patient~) Map~PatientIdentifier, Patient~
        +groupByIdentifiers(Collection~Patient~) Map~PatientIdentifier, List~Patient~~
        +getIdentifiers(Collection~Patient~) List~PatientIdentifier~
        +groupByBirthDateTime(Collection~Patient~) Map~BirthDateTime, List~Patient~~
        +getBirthDateTimes(Collection~Patient~) List~BirthDateTime~
  }

    class Gender{
        <<enumeration>>
        UNKNOWN
        MALE
        FEMALE
        OTHER
  }

    class PatientChangeEvent{
        -current : Patient
        -previous : Patient
        -changeType : ChangeType
        -PatientChangeEvent(Builder)
        +getCurrent() Patient
        +getPrevious() Patient
        +getChangeType() ChangeType
        +isAdded() boolean
        +isRemoved() boolean
        +copy() Builder
        +toString() String
        +hashCode() int
        +equals(Object) boolean
  }


    class ChangeType{
        <<enumeration>>
        ADD
        UPDATE
        REMOVE
        PATIENT_ALLERGY_CHANGE
        PATIENT_ENCNTR_MOVE
        PATIENT_COMBINE
        PATIENT_UNCOMBINE
        PATIENT_HIDE
        PATIENT_UNHIDE
        UNKNOWN
  }

    class PatientContactDetails{
        -patientId : String
        -patientContactInfo : List~PatientContactInfo~
        -phones : List~Phone~
        -PatientContactDetails(Builder)
        +getPatientId() String
        +getPatientContactInfo() List~PatientContactInfo~
        +getPhones() List~Phone~
        +copy() Builder
        +toString() String
        +hashCode() int
        +equals(Object) boolean
        +groupByPatientId(Collection~PatientContactDetails~) Map~String, List~PatientContactDetails~~
        +getPatientIds(Collection~PatientContactDetails~) List~String~
  }

    class PatientContactInfo{
        -patientId : String
        -streetLines : List~String~
        -city : String
        -state: String
        -zip : String
        -country : String
        -phones : List~String~ [deprecated]
        -priority : Long
        -type : String
        -email : String
        -PatientContactInfo(Builder)
        +getPatientId() String
        +getStreetLines() List~String~
        +getFullSameLineStreetAddress() String
        +getFullMultipleLinesStreetAddress() String
        +getCity() String
        +getState() String
        +getZip() String
        +getCountry() String
        +getPhones() List~String~
        +getPriority() Long
        +getType() String
        +getEmail() String
        +copy() Builder
        +toString() String
        +hashCode() int
        +equals(Object) boolean
        +groupByPatientId(Collection~PatientContactInfo~) Map~String, List~PatientContactInfo~~
        +getPatientIds(Collection~PatientContactInfo~) List~String~
        +groupByType(Collection~PatientContactInfo~) Map~String, List~PatientContactInfo~~
        +getTypes(Collection~PatientContactInfo~) List~String~
  }

    class PatientIdentifier{
        -assigner : String
        -type : String
        -value : String
        -oid : String
        -PatientIdentifier(Builder)
        +getAssigner() String
        +getType() String
        +getValue() String
        +getOid(): String
        +copy() Builder
        +toString() String
        +hashCode() int
        +equals(Object) boolean
  }

    class Phone{
        -number : String
        -display : String
        -meaning : String
        -priority : Long
        -type : String
        -Phone(Builder)
        +getNumber() String
        +getDisplay() String
        +getMeaning() String
        +getPriority() Long
        +getType() String
        +copy() Builder
        +toString() String
        +hashCode() int
        +equals(Object) boolean
        +groupByType(Collection~Phone~) Map~String, List~Phone~~
        +getTypes(Collection~Phone~) List~String~
  }

    class RegisteredFacilityInfo{
        -organizationId : String
        -patientId : String
        -typeMeaning : String
        -endEffectiveDateTime : Long
        -RegisteredFacilityInfo(Builder)
        +getOrganizationId() String
        +getPatientId() String
        +getTypeMeaning() String
        +getEndEffectiveDateTime() Long
        +copy() Builder
        +toString() String
        +hashCode() int
        +equals(Object) boolean
        +groupByOrganizationId(Collection~RegisteredFacilityInfo~) Map~String, List~RegisteredFacilityInfo~~
        +getOrganizationIds(Collection~RegisteredFacilityInfo~) List~String~
        +groupByPatientId(Collection~RegisteredFacilityInfo~) Map~String, List~RegisteredFacilityInfo~~
        +getPatientIds(Collection~RegisteredFacilityInfo~) List~String~
  }

Patient *--> Gender : Enumeration
PatientChangeEvent *--> ChangeType : Enumeration
FamilyContactInfo "*" *--> "1" Phone : \n\n\n\n phones
Patient "*" *--> "1" PatientIdentifier : \n\n\n\n identifiers
Patient "1" *--> "1" BirthDateTime : birthDateTime
PatientChangeEvent "1" *--> "1" Patient : current
PatientContactDetails "*" *--> "1" PatientContactInfo : patientContactInfo
PatientContactDetails "1" *--> "*" Phone : phones

```
## mermaid
[![](https://mermaid.ink/img/pako:eNrNWttu2zgQ_RVDT3GbPPQ1KAr4ojRGbDmwlRbtemEwEm1zVxa9ugR1i_rbd0hJFimSkq1kNwmCIuIMh4eHM8Mh2V-WR31sXVtegOJ4SNA6QttF2IEf3tLpBQGO1vtfWRv7uSJ-57ozTyISroXWHUoIDpORVuiTeBegvU4UYeQlhIYxCMckTg6ZxkFQifETjkii7Z7ju-inJPBx1C1F79cY0Fx0lT5McF-gNciHGWCDdFZgBrkeM9Oa57B1Rjy6Y-05akGQ0ExX12mD4s0AlgtkJEwEAf4nRUF8MX38C3tJt_NIaYBRKChs0a6_h8kOKNDFoR9y4g7dzgTt8glcFsstzSSi6Ym9OReF6FBdilhvwERgNmy5UM8a_WimFYhyvZ8FosGMiuG3FIkJiB7TBMdCML7v23N3aTsDx50tR8Plnf0NosTd77B_h_eaGfVHM_d2Oey59tIdTezl1xF83s_swWg-mjrN_e977sh23OV8foJyrz-fjh9gqOqojT0f7ofuEiZV1RxTjR78upOq5gAFOPRRJCaSksKLrsSwyHOfRMlmiBLski0W894eowhGGIUJXosxe7WlYbJhyWlDo0TMelnGq7RuaMrM9PcJFm2QEHCp7TH2aOir7SEKqRbMTxpifRKWJqZJmFfeBnt_f0EB8eGfFF8MNhEN6Q3BgX_pdDsHp4N_JEBq3HHS7SOOKu79DfiB1KRAYrIJo4jlNJkMnmqzNKsKboEoliOliXNjnCutaM7p0oocYMwE7zsnTZdzEzqmHgoYbSzZF3-rGpzUXIP9rbchahXfkiZrmJAgIHxvoa-yafCgEEPiBm1JsB_AGkICG4Ur2nlmPbAiUQwLssU6IQxplEU4QDyFbsgudmme1s2lw24DK3ssLe7ZlyhWJvbSdcRNMVGDfIxqxTPtdGurDj7HY2FSnfEbKDwUzis7qCpvKkaaLHImVKX6AkVntEWp8jLY9OXLSRAhmMVQzi01x29tiG6J7we4TQCH0D5PVyvyQyclPmAjK4KjMmaLqRcSMX4fxS2NbZLit6C3hl0Ls133M_9DkKBjSQBSRiVscbA-gkYRdGdmhqbInxwpbJcanCORBoWSsSIbfFS4_CR3kSuErolOppoRCTpVRplQrLO0pL6BNJRzUQnHorUp5eh7iw7bkF5KA_VJpXSjZ41-NNMKhOCr56EwuXwrFMeAeBYThZVWEISgexaI0s6ZOHJHLiPbCEOJ9Xrnbmex3uEbbDam9wKdnJaM-CS1emySah08SfGQF8fifpqlP2E7_fgRh-kWR7xu-yQk2Afnzpl-dcqGSW9sl183tvw9dW_tmWbAHOBgg8I1tp8qe7mXRlFWEOd6Yi0c4SdC01gr9Lg9dnpm--DxQ90HhYENW-IgwwBZWhmG1zI5DJO8HJxtHhok70nc833MNl4105N4hrf0ySD9H09Q8qqV8zjFVXrDoeA39-zepPye2ZPpF-G7uJHpjcf27PO35eC253zWyPNLIn3nwXTSHzkawYNjFN2OhtoOcrvg9gZPzurXIU4QCcS7rfoj5E7qzQ-lcsWoP0E0nQi1oAyO3nT4U4FcdE-A-PZOcXUHHC1hNVthRfGkg45pjOomWetgjOWTvStOIgy1AhFcRb1c8AxvEnECG4am_SfZ6dQ9moZJpLUkO2uOoPOHjyGXezCI_6eU3wnNn0nki6OrJEvrinm8BSJ1Ao3ntguBeclj7a3FTRoEcyiKmGbWB1J8hOPYdLoC_UkaJGQX8D7xKZ0GhscYjjO74NPJvpOdyWC2cqbwl2JYf1mTL5l61wfCfAvUmbbZwr2Bd6XTE4Pp6kOj1SIlnHQ_w_n8DwAyu-dj0-eqsg4WUxUokHXILzCUUDXF9hO7wtcJqP6-RwFgiPhejsXgmTVOmz0q6GVTAhnk-vX8uboaLHTFFQj5g8eZT9tbMA4t2sR-dq7mkAxrkj3HtHrKnmQYTSmsTX56nRykRDevmXQBzQWNMZx3bwjbGV6DAo6wf4M8EgBV1TKDRmtg-Cev8Ufnv5Qwd5iY_QhOn_ZqxTA_YeEetOJTepQGZ5pKgFu-e7glbNMWpkH-ek9esi9VKBDcQs-kzs0Mmoc6suOThmrxCvHSsPV78smIeRAVb3fvrq4-5dco4Ll2eSI-qghXDpn2QLyskHqoL5UL693CyrotrA_wJ49s6LcAEMVvJyu0S1Bqr-r2WLUgPF2IZj7IZvqVB4tH-YZdM2HFRPnmmV_2lN2k85FxDvKRWT1Hm-0JSN4JTBbkWZcWrASUpr51bfEcuLCSDYaJWUCW5eMVgpJ9YS3C36CKUojhfehZ1ysISnxppTsfiMj_D1re-vtfYJFbLg?type=png)](https://mermaid.live/edit#pako:eNrNWttu2zgQ_RVDT3GbPPQ1KAr4ojRGbDmwlRbtemEwEm1zVxa9ugR1i_rbd0hJFimSkq1kNwmCIuIMh4eHM8Mh2V-WR31sXVtegOJ4SNA6QttF2IEf3tLpBQGO1vtfWRv7uSJ-57ozTyISroXWHUoIDpORVuiTeBegvU4UYeQlhIYxCMckTg6ZxkFQifETjkii7Z7ju-inJPBx1C1F79cY0Fx0lT5McF-gNciHGWCDdFZgBrkeM9Oa57B1Rjy6Y-05akGQ0ExX12mD4s0AlgtkJEwEAf4nRUF8MX38C3tJt_NIaYBRKChs0a6_h8kOKNDFoR9y4g7dzgTt8glcFsstzSSi6Ym9OReF6FBdilhvwERgNmy5UM8a_WimFYhyvZ8FosGMiuG3FIkJiB7TBMdCML7v23N3aTsDx50tR8Plnf0NosTd77B_h_eaGfVHM_d2Oey59tIdTezl1xF83s_swWg-mjrN_e977sh23OV8foJyrz-fjh9gqOqojT0f7ofuEiZV1RxTjR78upOq5gAFOPRRJCaSksKLrsSwyHOfRMlmiBLski0W894eowhGGIUJXosxe7WlYbJhyWlDo0TMelnGq7RuaMrM9PcJFm2QEHCp7TH2aOir7SEKqRbMTxpifRKWJqZJmFfeBnt_f0EB8eGfFF8MNhEN6Q3BgX_pdDsHp4N_JEBq3HHS7SOOKu79DfiB1KRAYrIJo4jlNJkMnmqzNKsKboEoliOliXNjnCutaM7p0oocYMwE7zsnTZdzEzqmHgoYbSzZF3-rGpzUXIP9rbchahXfkiZrmJAgIHxvoa-yafCgEEPiBm1JsB_AGkICG4Ur2nlmPbAiUQwLssU6IQxplEU4QDyFbsgudmme1s2lw24DK3ssLe7ZlyhWJvbSdcRNMVGDfIxqxTPtdGurDj7HY2FSnfEbKDwUzis7qCpvKkaaLHImVKX6AkVntEWp8jLY9OXLSRAhmMVQzi01x29tiG6J7we4TQCH0D5PVyvyQyclPmAjK4KjMmaLqRcSMX4fxS2NbZLit6C3hl0Ls133M_9DkKBjSQBSRiVscbA-gkYRdGdmhqbInxwpbJcanCORBoWSsSIbfFS4_CR3kSuErolOppoRCTpVRplQrLO0pL6BNJRzUQnHorUp5eh7iw7bkF5KA_VJpXSjZ41-NNMKhOCr56EwuXwrFMeAeBYThZVWEISgexaI0s6ZOHJHLiPbCEOJ9Xrnbmex3uEbbDam9wKdnJaM-CS1emySah08SfGQF8fifpqlP2E7_fgRh-kWR7xu-yQk2Afnzpl-dcqGSW9sl183tvw9dW_tmWbAHOBgg8I1tp8qe7mXRlFWEOd6Yi0c4SdC01gr9Lg9dnpm--DxQ90HhYENW-IgwwBZWhmG1zI5DJO8HJxtHhok70nc833MNl4105N4hrf0ySD9H09Q8qqV8zjFVXrDoeA39-zepPye2ZPpF-G7uJHpjcf27PO35eC253zWyPNLIn3nwXTSHzkawYNjFN2OhtoOcrvg9gZPzurXIU4QCcS7rfoj5E7qzQ-lcsWoP0E0nQi1oAyO3nT4U4FcdE-A-PZOcXUHHC1hNVthRfGkg45pjOomWetgjOWTvStOIgy1AhFcRb1c8AxvEnECG4am_SfZ6dQ9moZJpLUkO2uOoPOHjyGXezCI_6eU3wnNn0nki6OrJEvrinm8BSJ1Ao3ntguBeclj7a3FTRoEcyiKmGbWB1J8hOPYdLoC_UkaJGQX8D7xKZ0GhscYjjO74NPJvpOdyWC2cqbwl2JYf1mTL5l61wfCfAvUmbbZwr2Bd6XTE4Pp6kOj1SIlnHQ_w_n8DwAyu-dj0-eqsg4WUxUokHXILzCUUDXF9hO7wtcJqP6-RwFgiPhejsXgmTVOmz0q6GVTAhnk-vX8uboaLHTFFQj5g8eZT9tbMA4t2sR-dq7mkAxrkj3HtHrKnmQYTSmsTX56nRykRDevmXQBzQWNMZx3bwjbGV6DAo6wf4M8EgBV1TKDRmtg-Cev8Ufnv5Qwd5iY_QhOn_ZqxTA_YeEetOJTepQGZ5pKgFu-e7glbNMWpkH-ek9esi9VKBDcQs-kzs0Mmoc6suOThmrxCvHSsPV78smIeRAVb3fvrq4-5dco4Ll2eSI-qghXDpn2QLyskHqoL5UL693CyrotrA_wJ49s6LcAEMVvJyu0S1Bqr-r2WLUgPF2IZj7IZvqVB4tH-YZdM2HFRPnmmV_2lN2k85FxDvKRWT1Hm-0JSN4JTBbkWZcWrASUpr51bfEcuLCSDYaJWUCW5eMVgpJ9YS3C36CKUojhfehZ1ysISnxppTsfiMj_D1re-vtfYJFbLg)

```mermaid
%%{init: {'theme':'forest'}}%%
sequenceDiagram
    actor Consumer
    participant PatientClient as Patient Client
    participant PatientService as Patient Service

    Consumer ->>+ PatientClient : getPatients(PatientQualifier)
    PatientClient ->>+ PatientService : getPatients(GetPatientsTransaction.Request)
    rect rgb(211,255,255)
        alt PatientQualifer is NULL
            rect rgb(255,69,0)
                PatientService --x Consumer : Qualifier cannot be null
            end    
        else PatientQualifier is not NULL
            rect rgb(111,222,211)
                PatientService ->>+ PatientService  : getRetrievableAttributes(GetPatientsTransaction.Request)
                note left of PatientService : Building the secondary attributes to retrieve
                alt request has attributes
                    rect rgb(250,250,210)
                        PatientService ->>+ PatientService : keysFromAttributes(attributes)
                        deactivate PatientService
                        note left of PatientService: This helps retrieve allergies,patient contact,family contact \n and registered facility information
                    end
                end
                deactivate PatientService
                alt patient IDs is not empty
                    rect rgb(230,230,250)
                        PatientService ->>+ PatientService  : getPatientsByInternalIdentifiers(patientBaseSearchByQualifier, proxySupportFalse)
                        note left of PatientService : Patient IDs are passed for search. Proxy is not supported.Client calls are only eligible.
                        PatientService ->>+ PatientService  : getDAOByLogicalDomainId(OrganizationId(), proxySupportFalse)
                        note left of PatientService: Proxy is not supported.Client calls are only supported.
                        deactivate PatientService
                        PatientService ->>+ PatientService : toArrayAttributes(attributes)
                        deactivate PatientService
                        PatientService ->>+ PatientDataAccess : getPatientsByInternalIdentifiers(internalIds,organizationId,PatientRetrievableAttribute)
                        PatientDataAccess ->>+ PatientDataAccess : retrieveEncounter(additionalAttributes)
                        deactivate PatientDataAccess
                        PatientDataAccess ->>+ PatientDataAccess : retrieveEncounterWithType(additionalAttributes)
                        deactivate PatientDataAccess
                        PatientDataAccess ->>+ PatientDataAccess : retrieveBirthDateTmPrecision(additionalAttributes)
                        deactivate PatientDataAccess
                        PatientDataAccess ->>+ PatientSearchByInternalIdsTransaction :  searchByInternalIdsQualifier\n(PatientBaseSearchBy,retrieveEncounter,encounterType,retrieveBirthDateTmPrecision)
                        PatientSearchByInternalIdsTransaction -->>- PatientDataAccess : SearchByInternalIdsQualifier
                        PatientDataAccess ->>+ PatientAllergyDecorator : addAllergy("getPatientsByInternalIdentifiers API", patients, additionalAttributes)
                        PatientAllergyDecorator -->>- PatientDataAccess : Retrieved patient allergies
                        PatientDataAccess ->>+ PatientFamilyContactDecorator : retrieveFamilyContacts(patients, ids, additionalAttributes)
                        PatientFamilyContactDecorator -->>- PatientDataAccess : Retrieved patient family contacts
                        PatientDataAccess ->>+ FamilyContactMapper : addFamilyContactInformation(patients, ids, patientFamilyContactMap)
                        Note right of FamilyContactMapper : Maps the family contact information to the patient
                        FamilyContactMapper ->>- PatientDataAccess : Patient with family contact information
                        PatientDataAccess ->>+ PersonOrganizationRelationDecorator : retrievePersonOrganizationRelation(patients,ids,additionalAttributes)
                        PersonOrganizationRelationDecorator -->>- PatientDataAccess :  Retrieved person organization relation
                        PatientDataAccess ->>+ OrganizationRelationMapper : addOrgReltnInformation(millDomain,patients,patientIds,orgMap)
                        Note right of OrganizationRelationMapper : Maps the organization relation information to the patient
                        OrganizationRelationMapper -->>- PatientDataAccess : Patient with organization relation information
                        PatientDataAccess -->>- PatientService : patients
                        deactivate PatientService
                    end    
                else identifiers are not empty
                    rect rgb(152,251,152)
                        PatientService ->>+ PatientService : hasValidIdentifiers(Identifiers)
                        note left of PatientService : Identifiers are passed for search
                        deactivate PatientService
                        PatientService ->>+ PatientService : getPatientsBySearchCriteria(PatientSearchByCriteria, proxySupportFalse)
                        note left of PatientService : Proxy is not supported.Client calls are only supported.
                        PatientService ->>+ PatientService : getDAOByLogicalDomainId(OrganizationId(), proxySupportFalse)
                        note left of PatientService : Proxy is not supported.Client calls are only supported.
                        deactivate PatientService
                        PatientService ->>+ PatientService : toArrayAttributes(attributes)
                        deactivate PatientService
                        PatientService ->>+ PatientDataAccess : getPatientsBySearchCriteria(PatientSearchByCriteria,PatientRetrievableAttribute)
                        PatientDataAccess ->>+ PatientDataAccess : retrieveEncounter(additionalAttributes)
                        deactivate PatientDataAccess
                        PatientDataAccess ->>+ PatientDataAccess : retrieveEncounterWithType(additionalAttributes)
                        deactivate PatientDataAccess
                        PatientDataAccess ->>+ PatientDataAccess : retrieveBirthDateTmPrecision(additionalAttributes)
                        deactivate PatientDataAccess
                        PatientDataAccess ->>+ PatientAllergyDecorator : addAllergy("getPatientsBySearchCriteria API", patients, additionalAttributes)
                        PatientAllergyDecorator -->>- PatientDataAccess : Retrieved patient allergies
                        PatientDataAccess ->>+ PatientFamilyContactDecorator : retrieveFamilyContacts(patients, ids, additionalAttributes)
                        PatientFamilyContactDecorator -->>- PatientDataAccess : Retrieved patient family contacts
                        PatientDataAccess ->>+ PatientDataAccess : patientCollectionToMap(patient collection)
                        Note right of PatientDataAccess : Transform patient collection to map of patients
                        deactivate PatientDataAccess
                        PatientDataAccess ->>+ FamilyContactMapper : addFamilyContactInformation(patients, ids, patientFamilyContactMap)
                        Note right of FamilyContactMapper : Maps the family contact information to the patient
                        FamilyContactMapper -->>- PatientDataAccess : Patient with family contact information
                        PatientDataAccess ->>+ PersonOrganizationRelationDecorator : retrievePersonOrganizationRelation(patients,ids,additionalAttributes)
                        PersonOrganizationRelationDecorator -->>- PatientDataAccess :  Retrieved person organization relation
                        PatientDataAccess ->>+ OrganizationRelationMapper : addOrgReltnInformation(millDomain,patients,patientIds,orgMap)
                        Note right of OrganizationRelationMapper : Maps the organization relation information to the patient
                        OrganizationRelationMapper -->>- PatientDataAccess : Patient with organization relation information
                        PatientDataAccess -->>- PatientService : patients
                        deactivate PatientService    
                    end    
                else Patient first name and/or last name is not empty
                    rect rgb(255,218,185)
                        PatientService ->>+ PatientService : hasValidPatientFirstName(patientQualifier)
                        deactivate PatientService
                        PatientService ->>+ PatientService : hasValidPatientLastName(patientQualifier)
                        deactivate PatientService
                        alt valid qualifier option on request
                            rect rgb(221,160,221)
                                PatientService ->>+ PatientService : hasValidPatientFirstName(patientQualifier)
                                note left of PatientService : if patient has valid first name
                                PatientService ->>+ PatientService : hasValidPatientLastName(patientQualifier)
                                note left of PatientService : if patient has valid last name
                                deactivate PatientService
                                deactivate PatientService
                                PatientService ->>+ PatientService : getPatientsBySearchCriteria(PatientSearchByCriteria, proxySupportFalse)
                                note left of PatientService : Proxy is not supported.Client calls are only supported.
                                PatientService ->>+ PatientService : getDAOByLogicalDomainId(OrganizationId(), proxySupportFalse)
                                note left of PatientService : Proxy is not supported.Client calls are only supported.
                                deactivate PatientService
                                PatientService ->>+ PatientService : toArrayAttributes(attributes)
                                deactivate PatientService
                                PatientService ->>+ PatientDataAccess : getPatientsBySearchCriteria(PatientSearchByCriteria,PatientRetrievableAttribute)
                                PatientDataAccess ->>+ PatientDataAccess : retrieveEncounter(additionalAttributes)
                                deactivate PatientDataAccess
                                PatientDataAccess ->>+ PatientDataAccess : retrieveEncounterWithType(additionalAttributes)
                                deactivate PatientDataAccess
                                PatientDataAccess ->>+ PatientDataAccess : retrieveBirthDateTmPrecision(additionalAttributes)
                                deactivate PatientDataAccess
                                PatientDataAccess ->>+ PatientSearchByCriteriaTransaction : searchByCriteriaQualifier(PatientSearchByCriteria,retrieveEncounter,encounterType,retrieveBirthDateTmPrecision))
                                PatientSearchByCriteriaTransaction -->>- PatientDataAccess : SearchByCriteriaQualifier
                                PatientDataAccess ->>+ PatientAllergyDecorator: addAllergy("getPatientsBySearchCriteria API", patients, additionalAttributes)
                                PatientAllergyDecorator -->>- PatientDataAccess : Retrieved patient allergies
                                PatientDataAccess ->>+ PatientFamilyContactDecorator : retrieveFamilyContacts(patients, ids, additionalAttributes)
                                PatientFamilyContactDecorator -->>- PatientDataAccess : Retrieved patient family contacts
                                PatientDataAccess ->>+ PatientDataAccess : patientCollectionToMap(patient collection)
                                Note right of PatientDataAccess : Transform patient collection to map of patients
                                deactivate PatientDataAccess
                                PatientDataAccess ->>+ FamilyContactMapper : addFamilyContactInformation(patients, ids, patientFamilyContactMap)
                                Note right of FamilyContactMapper : Maps the family contact information to the patient
                                FamilyContactMapper -->>- PatientDataAccess : Patient with family contact information
                                PatientDataAccess ->>+ PersonOrganizationRelationDecorator : retrievePersonOrganizationRelation(patients,ids,additionalAttributes)
                                PersonOrganizationRelationDecorator -->>- PatientDataAccess :  Retrieved person organization relation
                                PatientDataAccess ->>+ OrganizationRelationMapper : addOrgReltnInformation(millDomain,patients,patientIds,orgMap)
                                Note right of OrganizationRelationMapper : Maps the organization relation information to the patient
                                OrganizationRelationMapper -->>- PatientDataAccess : Patient with organization relation information
                                PatientDataAccess -->>- PatientService : patients
                            end
                        else invalid qualifier
                            rect rgb(255,69,0)
                                PatientService --x- Consumer : Invalid qualifier option\n on request
                            end    
                        end
                        deactivate PatientService
                    end    
                end    
            end
        PatientService ->>+ PatientService : Converting all the legacy patients to iBus patients
        deactivate PatientService
        PatientService ->>+ PatientService : Filter out the unwanted non-qualifying patients based on patient IDs
        deactivate PatientService
        PatientService ->>+ PatientService : decoratePatients(legacyPatientList,request,allergyList,\n patientContactInfoList,patientContactDetailsList,\n familyContactInfoList,registeredFacilityInfoList,patientConverter)
        note right of PatientService : Decorate the patients with additional attributes if applicable
        
        PatientService -->>- PatientClient :  GetPatientsTransaction.Reply
        PatientClient -->>- Consumer : GetPatientsTransaction.Reply
        Consumer ->>+ GetPatientsTransaction : GetPatientsTransaction.Reply.getPatients()
        note right of GetPatientsTransaction : Returns the patients from the last reply. This method will never return null, however the return value is unmodifiable.
        GetPatientsTransaction -->>- Consumer : List<Patient>
        Consumer ->>+ GetPatientsTransaction : GetPatientsTransaction.Reply.getAllergies()
        note right of GetPatientsTransaction : Returns the allergies from the last reply. This method will never return null, however the return value is unmodifiable.
        GetPatientsTransaction -->>- Consumer : List<Allergy>
        Consumer ->>+ GetPatientsTransaction : GetPatientsTransaction.Reply.getPatientContactInfo()
        note right of GetPatientsTransaction : Returns the patient contact info from the last reply. This method will never return null, however the return value is unmodifiable.
        GetPatientsTransaction -->>- Consumer : List<PatientContactInfo>
        Consumer ->>+ GetPatientsTransaction : GetPatientsTransaction.Reply.getFamilyContactInfo()
        note right of GetPatientsTransaction : Returns the family contact info from the last reply. This method will never return null, however the return value is unmodifiable.
        GetPatientsTransaction -->- Consumer : List<FamilyContactInfo>
        Consumer ->>+ GetPatientsTransaction : GetPatientsTransaction.Reply.getRegisteredFacilityInfo()
        note right of GetPatientsTransaction : Returns the registered facility info from the last reply. This method will never return null, however the return value is unmodifiable.
        GetPatientsTransaction -->- Consumer  : List<RegisteredFacilityInfo>
    
        end
    end
```
