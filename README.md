# FACE-RECOGNITION-ATTENDANCE-SYSTEM-USING-RASPBERRY-PI
# Patient Client and Data Model

## Data Model

```mermaid
classDiagram
    class Allergy{
        -String id
        -String patientId
        -String display
        -List~String~ reactions
        -String severity
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
        +mapById(Collection~Allergy~)$ Map&lt;String, Allergy&gt;
        +groupById(Collection~Allergy~)$ Map&lt;String, List~Allergy~&gt;
        +getIds(Collection~Allergy~)$ List~String~
        +groupByPatientId(Collection~Allergy~)$ Map&lt;String, List~Allergy~&gt;
        +getPatientIds(Collection~Allergy~)$ List~String~
        +groupByReactions(Collection~Allergy~)$ Map&lt;String, List~Allergy~&gt;
        +getReactions(Collection~Allergy~)$ List~String~
    }

    class Attributes{
        +TypedKey~String~  BEST_ENCNTR_ID_KEY$
        +TypedKey~String~ BIRTH_DATE_TIME_WITH_PRECISION_KEY$
        +TypedKey~String~ PATIENT_SSN_KEY$
        +TypedKey~String~ ABSOLUTE_BIRTH_DATE_TIME_KEY$
        +TypedKey~Long~ UPDT_CNT_KEY$
        +TypedKey~Calendar~ UPDT_DT_TM_KEY$
        -Attributes()
    }

    class BirthDateTime{
        -Integer year
        -Short month
        -Short day
        -Byte hour
        -Byte minute
        -Byte second
        -Integer nano
        -String zoneId
        -BirthDateTime(Builder)
        -checkValidValue(ChronoField, N)$ &lt;N extends Number&gt;
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
    
    class FamilyContactInfo{
        -String id
        -String patientId
        -String firstName
        -String lastName
        -List~String~ relationshipsToPatient
        -List~Phone~ phones
        -FamilyContactInfo(Builder)
        +getId() String
        +getPatientId() String
        +getFirstName() String
        +getLastName() String
        +getRelationshipsToPatient() List~String~
        +getPhones() List~Phone~       
        +copy() Builder
        +toString() String
        public int hashCode()
        public boolean equals(final Object object)
        +mapById(Collection~FamilyContactInfo~)$ Map&lt;String, FamilyContactInfo&gt;
        +groupById(Collection~FamilyContactInfo~)$ Map&lt;String, List~FamilyContactInfo~&gt;
        +getIds(Collection~FamilyContactInfo~)$ List~String~
        +groupByPatientId(Collection~FamilyContactInfo~)$ Map&lt;String, List~FamilyContactInfo~&gt;
        +getPatientIds(Collection~FamilyContactInfo~)$ List~String~
    }

    class Patient{
        -String id
        -String firstName
        -String middleName
        -String lastName
        -String nameSuffix
        -List~PatientIdentifier~ identifiers
        -BirthDateTime birthDateTime
        -Gender gender
        -ContextMap attributes
        -Patient(Builder)
        +getId() String
        +getFirstName() String
        +getMiddleName() String
        +getLastName() String
        +getNameSuffix() String
        +getIdentifiers() List~PatientIdentifier~
        +getBirthDateTime() BirthDateTime
        +getGender() Gender
        +getAttributes() ContextMap
        +getAttribute(TypedKey~T~) ~T~
        +getAttribute(TypedKey~T~, T) ~T~
        +copy() Builder
        +toString() String
        +hashCode() int
        +equals(Object) boolean
        +mapById(Collection~Patient~)$ Map&lt;String, Patient&gt;
        +groupById(Collection~Patient~)$ Map&lt;String, List~Patient~&gt;
        +getIds(Collection~Patient~)$ List~String~
        +groupByFirstName(Collection~Patient~)$ Map&lt;String, List~Patient~&gt;
        +getFirstNames(Collection~Patient~)$ List~String~
        +groupByMiddleName(Collection~Patient~)$ Map&lt;String, List~Patient~&gt;
        +getMiddleNames(Collection~Patient~)$ List~String~
        +groupByLastName(Collection~Patient~)$ Map&lt;String, List~Patient~&gt;
        +getLastNames(Collection~Patient~)$ List~String~
        +groupByNameSuffix(Collection~Patient~)$ Map&lt;String, List~Patient~&gt;
        +getNameSuffixes(Collection~Patient~)$ List~String~
        +mapByIdentifiers(Collection~Patient~)$ Map&lt;PatientIdentifier, Patient&gt;
        +groupByIdentifiers(Collection~Patient~)$ Map&lt;PatientIdentifier, List~Patient~&gt;
        +getIdentifiers(Collection~Patient~)$ List~PatientIdentifier~
        +groupByBirthDateTime(Collection~Patient~)$ Map&lt;BirthDateTime, List~Patient~&gt;
        +getBirthDateTimes(Collection~Patient~)$ List~BirthDateTime~
    }

    class Gender{
        <<enumeration>>
        UNKNOWN
        MALE
        FEMALE
        OTHER
    }

    class PatientChangeEvent{
        -Patient current
        -Patient previous
        -ChangeType changeType
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
        -String patientId
        -List~PatientContactInfo~ patientContactInfo
        -List~Phone~ phones
        -PatientContactDetails(Builder)
        +getPatientId() String
        +getPatientContactInfo() List~PatientContactInfo~
        +getPhones() List~Phone~
        +copy() Builder
        +toString() String
        +hashCode() int
        +equals(Object) boolean
        +groupByPatientId(Collection~PatientContactDetails~)$ Map&lt;String, List~PatientContactDetails~&gt;
        +getPatientIds(Collection~PatientContactDetails~)$ List~String~
    }

    class PatientContactInfo{
        -String patientId
        -List~String~ streetLines
        -String city
        -String state
        -String zip
        -String country
        -List~String~ phones [Deprecated]
        -Long priority
        -String type
        -String email
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
        +groupByPatientId(Collection~PatientContactInfo~)$ Map&lt;String, List~PatientContactInfo~&gt;
        +getPatientIds(Collection~PatientContactInfo~)$ List~String~
        +groupByType(Collection~PatientContactInfo~)$ Map&lt;String, List~PatientContactInfo~&gt;
        +getTypes(Collection~PatientContactInfo~)$ List~String~
    }

    class PatientIdentifier{
        -String assigner
        -String type
        -String value
        -String oid
        -PatientIdentifier(Builder)
        +getAssigner() String
        +getType() String
        +getValue() String
        +getOid() String
        +copy() Builder
        +toString() String
        +hashCode() int
        +equals(Object) boolean
    }

    class Phone{
        -String number
        -String display
        -String meaning
        -Long priority
        -String type
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
        +groupByType(Collection~Phone~)$ Map&lt;String, List~Phone~&gt;
        +getTypes(Collection~Phone~)$ List~String~
    }

    class RegisteredFacilityInfo{
        -String organizationId
        -String patientId
        -String typeMeaning
        -Long endEffectiveDateTime
        -RegisteredFacilityInfo(Builder)
        +getOrganizationId() String
        +getPatientId() String
        +getTypeMeaning() String
        +getEndEffectiveDateTime() Long
        +copy() Builder
        +toString() String
        +hashCode() int
        +equals(Object) boolean
        +groupByOrganizationId(Collection~RegisteredFacilityInfo~)$ Map&lt;String, List~RegisteredFacilityInfo~&gt;
        +getOrganizationIds(Collection~RegisteredFacilityInfo~)$ List~String~
        +groupByPatientId(Collection~RegisteredFacilityInfo~)$ Map&lt;String, List~RegisteredFacilityInfo~&gt;
        +getPatientIds(Collection~RegisteredFacilityInfo~) List~String~
    }

    Patient *--> Gender : Enumeration
    PatientChangeEvent *--> ChangeType : Enumeration
    FamilyContactInfo "1" *--> "*" Phone : phones\n\n\n\n
    Patient "1" *--> "*" PatientIdentifier : \n\n\n\n identifiers
    Patient "1" *--> "1" BirthDateTime : birthDateTime
    PatientChangeEvent "1" *--> "1" Patient : current
    PatientChangeEvent "1" *--> "1" Patient : previous [if available]
    PatientContactDetails "1" *--> "*" PatientContactInfo : patientContactInfo
    PatientContactDetails "1" *--> "*" Phone : phones

    link Allergy "https://github.cerner.com/ibus-core/ibus-patient-client/blob/master/src/main/java/com/cerner/ibus/patient/model/Allergy.java"
    link Attributes "https://github.cerner.com/ibus-core/ibus-patient-client/blob/master/src/main/java/com/cerner/ibus/patient/model/Attributes.java"
    link BirthDateTime "https://github.cerner.com/ibus-core/ibus-patient-client/blob/master/src/main/java/com/cerner/ibus/patient/model/BirthDateTime.java"
    link FamilyContactInfo "https://github.cerner.com/ibus-core/ibus-patient-client/blob/master/src/main/java/com/cerner/ibus/patient/model/FamilyContactInfo.java"
    link Patient "https://github.cerner.com/ibus-core/ibus-patient-client/blob/master/src/main/java/com/cerner/ibus/patient/model/Patient.java"
    link PatientChangeEvent "https://github.cerner.com/ibus-core/ibus-patient-client/blob/master/src/main/java/com/cerner/ibus/patient/model/PatientChangeEvent.java"
    link PatientContactDetails "https://github.cerner.com/ibus-core/ibus-patient-client/blob/master/src/main/java/com/cerner/ibus/patient/model/PatientContactDetails.java"
    link PatientContactInfo "https://github.cerner.com/ibus-core/ibus-patient-client/blob/master/src/main/java/com/cerner/ibus/patient/model/PatientContactInfo.java"
    link PatientIdentifier "https://github.cerner.com/ibus-core/ibus-patient-client/blob/master/src/main/java/com/cerner/ibus/patient/model/PatientIdentifier.java"
    link Phone "https://github.cerner.com/ibus-core/ibus-patient-client/blob/master/src/main/java/com/cerner/ibus/patient/model/Phone.java"
    link RegisteredFacilityInfo "https://github.cerner.com/ibus-core/ibus-patient-client/blob/master/src/main/java/com/cerner/ibus/patient/model/RegisteredFacilityInfo.java"

  ```

[![](https://mermaid.ink/img/pako:eNrNWntv2joU_ypRtD_arS2l76JpEoV0RStQAd203V4hkxjwboi5eVRjVfns9zhPO7EDpbtjqCqJz8M_H59zfGzzpJvUwnpNN23keU2CJi6aPTgafMIWrW7b2J0snqI29tnv-y5xJhqxim1z5BPs-C0JySLe3EYLjnBLPH8ZUZeai5HpE-p4RUkPP2KX-LxojGrnKiC2hd3djPRugqH7nV0tEhYJdwk8Bb0ZYVRQewlEoPPYRa5-jFamxKRz1h6j5gg-jXhlQlPkTRswSUAjjs8R8L8Bsr2d7ug7Nv1dbUSpjZHDMczQ_GoBg21QMFcIfRkbbrn7RmujeTyCvWSWlxo_FpcG68qH5khoy_xseAoNKiNGHWeT9br-Uz2bwchm_XUwVukponh-cIRI9IE4CnzsccH4brCYY-sTXqSBdGX0B0Oj0-gMesNWc_jJ-PqmlL3VG9wMm_WBMRy02sbwSwte73pGo9VvdTsrxe_qg5bRGQz7_dW89at-9_YeOsr3yQQ1meQtZXL3d83BEMaj7KCBbOxYyI1Z4W_QzjHvZ9bb2U3Ny754E18R1582kY8HZIb5lNdyfJgn7GoLjFw-Q02p62sz6vjTQqslJLurhY-1KQ3cfNuMOIAq3-phkzpWDgED4CCHFlPkT-pgIekKI5GkyX1zis1_PiObWPAvwDuNqUsdek2wbe11wB2XHQ3_8MGsntYJZiPs5tz5KxgCMlIMS6S1mT1YKmN2yGXYKLsWCTdgGpYaF7wtQmWhfaSkfmgkKakDZlLB-xYaS5ZqfXpLTWQzu7EcnzwXOUKrxhzsWa6D50reBU7W0Ca2TcIlhW5lrQjDgA-CazQj9qIBcwgJq-WMqfb6xX9MXA_mhB9-QoI-85RcYWCjMG9Oydwb0Diba3n2uynM6lKbsy--hiiM5lfXDNfJ0BT0W1RK7kmHV1phhENNi5Bo4H9UkVGweX6dLDKsqjtWqgxtUeQqr0WkWjeoSn4ROnmlsh7IXLEQq1ozckvCc0Ysy8Zrh25McaC1H4zH5EchTpMxwj8yJrCuAKLk2VOtYNqIf-O4PsIKBaviJPzi2pm5YP2COdBQsvJz5CTMXpgLVsV6OzXWZsmgk5pNwZCZLYn_9wWDfhBFxEpgV6xxRNbImMDzMWdORuQLKC0z7x-VeGJb5KMvaV6VZBTivN-uSCichvI0knnS6_pP9WwGg3PYF-JQOf5mONK4eJ01EjWbgeCi73UwMkUvRRL7dBbkaiCFuC_38w1Vlvv-KqWKjF_EJyYpNUKBrxydwFoKUOBcxjUxv5hG6ZBbS9-_x04ww25YuX3gEu5951On-6WTNbTrt0b2dm2I793BjdGTdBgjbEyRM8HGY24hT0pgM3BdzOfMlDJ38SOhAb-cRrrYltlMn4qSXI-KtbERdQrpOhbJlTBxzyp6BoOtIhIk74hXtyzMVuBiyideD8_oo4L6G3dM4nRl41jHR-rNJucwd-wYJHvvGe3uZ-49OV-p394avY9fh42beuejhB4f-MiFG932VasjIdx3lKSbVlMqILZz_q5w4ahsbWIfEdt7Wm_TyIc1X_cmzFzbuttAKRyFi6_a8RWRpXuxIuY_eetWtqWRGqxsEcxxrrW1UXaSXx5LnYvZ-SWelZwseL6LoWYgoqfE0qZ44ZBcRfjCcVB6_EbmEg00cHxXeeERuaj2l4UhW5ug1vqbZ6VsBC6hrhSHL2bvuBXPwH5Kpy85_Fjl8f3MUqUnE9eBbfeh-GGckQzkchd7nmo_BfztwPbJ3A5lvHWEGorLlRBndHIno30jc5XCaKJU0S6ErPxAJp6n4iEeEOO1TqbaYPP1B9wTrZ8HlGcbErYNMsB6RzChRf8PiEzxBujkySmrdyW5CfjIxBFOLEoj-5Gd0RebqXCYU-hYEe31uHOFV5Y4bHRVIKd1CWSP2vZ8OT8LLGwllnfCy4x1rqeTAzDQL4B7YW4OgShmIrpZ2egyuh3BUiWtTTLSdrJOIZrDokgawCFlZcwm8ivCtIcnwIBdbF0jk9hgLEUdQd0JmPpnWMe3XnbtwVyhLfcf2FIa4zHD_Igl55pydAo36goIN7zHGGRYVcuVBPL27q1EL8qZgPMHuSWlDqZgXZZZ21uvrw0uFX45cPkKvD7mMICSI4a3-_sf4oMRraYZ2VY3ZeHOEiLubJuclyheOT7obx_0SOxBr8JjGNYg9wAgkr90m5deChak8ktiXoNw95CpqYpqxLuIWv42QjLggopEdy07tpHufpRj4K1Tk-6EVfo4JG85SybGe3Bs4vyT_AQImKa-P_dqlcqE-NNgdGBiF4qFA5POKmQUePsmdXH0FIPYN232VRnZdFSZIeZMFc814ZE4le_oEVWYbKQmFKzEgpUZhLxdiXs-YKyAL8GT3jdsA1LaeYwqBiU6wu_HJfSfGCyxmCyKfjfAAgbRflmE_W5gcc9SOGLgbgkZB0IOMh_W28Ip4CiDuiUXLIKQguTWhK1hzDDkIIYpeguwWL8iFHl5sAVsciAxWH1Ph2oCVFl6TQ9r-Afdn2JYnHVY8HULj1Fg-2xQz8CKAqhFF46p13w3wHt6MLcgpcY_ftZrY6g4oXWOHL32pP_Qa_vHl9WTg8Pji-rR0fnR4eXJ2Z6-gObTk9OD6unl5fn5xeXx6eVJ9XlP_0kpqDg5uDg5hE_19Oj0AqjVUN23kMb3aVjEp27apU0R1FOsV7ZzgKGwIQNgkzpjMmHtgWtDc2Z7zz9IJgCs5xFrimCFeLw8q5wdnV2go2N8dn6MTo-PLXNUvbwYH51Ux9b5YfUI6c-AFof9t-OfgLOv5_8Ankcdcw?type=png)](https://mermaid.live/edit#pako:eNrNWntv2joU_ypRtD_arS2l76JpEoV0RStQAd203V4hkxjwboi5eVRjVfns9zhPO7EDpbtjqCqJz8M_H59zfGzzpJvUwnpNN23keU2CJi6aPTgafMIWrW7b2J0snqI29tnv-y5xJhqxim1z5BPs-C0JySLe3EYLjnBLPH8ZUZeai5HpE-p4RUkPP2KX-LxojGrnKiC2hd3djPRugqH7nV0tEhYJdwk8Bb0ZYVRQewlEoPPYRa5-jFamxKRz1h6j5gg-jXhlQlPkTRswSUAjjs8R8L8Bsr2d7ug7Nv1dbUSpjZHDMczQ_GoBg21QMFcIfRkbbrn7RmujeTyCvWSWlxo_FpcG68qH5khoy_xseAoNKiNGHWeT9br-Uz2bwchm_XUwVukponh-cIRI9IE4CnzsccH4brCYY-sTXqSBdGX0B0Oj0-gMesNWc_jJ-PqmlL3VG9wMm_WBMRy02sbwSwte73pGo9VvdTsrxe_qg5bRGQz7_dW89at-9_YeOsr3yQQ1meQtZXL3d83BEMaj7KCBbOxYyI1Z4W_QzjHvZ9bb2U3Ny754E18R1582kY8HZIb5lNdyfJgn7GoLjFw-Q02p62sz6vjTQqslJLurhY-1KQ3cfNuMOIAq3-phkzpWDgED4CCHFlPkT-pgIekKI5GkyX1zis1_PiObWPAvwDuNqUsdek2wbe11wB2XHQ3_8MGsntYJZiPs5tz5KxgCMlIMS6S1mT1YKmN2yGXYKLsWCTdgGpYaF7wtQmWhfaSkfmgkKakDZlLB-xYaS5ZqfXpLTWQzu7EcnzwXOUKrxhzsWa6D50reBU7W0Ca2TcIlhW5lrQjDgA-CazQj9qIBcwgJq-WMqfb6xX9MXA_mhB9-QoI-85RcYWCjMG9Oydwb0Diba3n2uynM6lKbsy--hiiM5lfXDNfJ0BT0W1RK7kmHV1phhENNi5Bo4H9UkVGweX6dLDKsqjtWqgxtUeQqr0WkWjeoSn4ROnmlsh7IXLEQq1ozckvCc0Ysy8Zrh25McaC1H4zH5EchTpMxwj8yJrCuAKLk2VOtYNqIf-O4PsIKBaviJPzi2pm5YP2COdBQsvJz5CTMXpgLVsV6OzXWZsmgk5pNwZCZLYn_9wWDfhBFxEpgV6xxRNbImMDzMWdORuQLKC0z7x-VeGJb5KMvaV6VZBTivN-uSCichvI0knnS6_pP9WwGg3PYF-JQOf5mONK4eJ01EjWbgeCi73UwMkUvRRL7dBbkaiCFuC_38w1Vlvv-KqWKjF_EJyYpNUKBrxydwFoKUOBcxjUxv5hG6ZBbS9-_x04ww25YuX3gEu5951On-6WTNbTrt0b2dm2I793BjdGTdBgjbEyRM8HGY24hT0pgM3BdzOfMlDJ38SOhAb-cRrrYltlMn4qSXI-KtbERdQrpOhbJlTBxzyp6BoOtIhIk74hXtyzMVuBiyideD8_oo4L6G3dM4nRl41jHR-rNJucwd-wYJHvvGe3uZ-49OV-p394avY9fh42beuejhB4f-MiFG932VasjIdx3lKSbVlMqILZz_q5w4ahsbWIfEdt7Wm_TyIc1X_cmzFzbuttAKRyFi6_a8RWRpXuxIuY_eetWtqWRGqxsEcxxrrW1UXaSXx5LnYvZ-SWelZwseL6LoWYgoqfE0qZ44ZBcRfjCcVB6_EbmEg00cHxXeeERuaj2l4UhW5ug1vqbZ6VsBC6hrhSHL2bvuBXPwH5Kpy85_Fjl8f3MUqUnE9eBbfeh-GGckQzkchd7nmo_BfztwPbJ3A5lvHWEGorLlRBndHIno30jc5XCaKJU0S6ErPxAJp6n4iEeEOO1TqbaYPP1B9wTrZ8HlGcbErYNMsB6RzChRf8PiEzxBujkySmrdyW5CfjIxBFOLEoj-5Gd0RebqXCYU-hYEe31uHOFV5Y4bHRVIKd1CWSP2vZ8OT8LLGwllnfCy4x1rqeTAzDQL4B7YW4OgShmIrpZ2egyuh3BUiWtTTLSdrJOIZrDokgawCFlZcwm8ivCtIcnwIBdbF0jk9hgLEUdQd0JmPpnWMe3XnbtwVyhLfcf2FIa4zHD_Igl55pydAo36goIN7zHGGRYVcuVBPL27q1EL8qZgPMHuSWlDqZgXZZZ21uvrw0uFX45cPkKvD7mMICSI4a3-_sf4oMRraYZ2VY3ZeHOEiLubJuclyheOT7obx_0SOxBr8JjGNYg9wAgkr90m5deChak8ktiXoNw95CpqYpqxLuIWv42QjLggopEdy07tpHufpRj4K1Tk-6EVfo4JG85SybGe3Bs4vyT_AQImKa-P_dqlcqE-NNgdGBiF4qFA5POKmQUePsmdXH0FIPYN232VRnZdFSZIeZMFc814ZE4le_oEVWYbKQmFKzEgpUZhLxdiXs-YKyAL8GT3jdsA1LaeYwqBiU6wu_HJfSfGCyxmCyKfjfAAgbRflmE_W5gcc9SOGLgbgkZB0IOMh_W28Ip4CiDuiUXLIKQguTWhK1hzDDkIIYpeguwWL8iFHl5sAVsciAxWH1Ph2oCVFl6TQ9r-Afdn2JYnHVY8HULj1Fg-2xQz8CKAqhFF46p13w3wHt6MLcgpcY_ftZrY6g4oXWOHL32pP_Qa_vHl9WTg8Pji-rR0fnR4eXJ2Z6-gObTk9OD6unl5fn5xeXx6eVJ9XlP_0kpqDg5uDg5hE_19Oj0AqjVUN23kMb3aVjEp27apU0R1FOsV7ZzgKGwIQNgkzpjMmHtgWtDc2Z7zz9IJgCs5xFrimCFeLw8q5wdnV2go2N8dn6MTo-PLXNUvbwYH51Ux9b5YfUI6c-AFof9t-OfgLOv5_8Ankcdcw)

## Client APIs

- [getPatients](./../../src/main/java/com/cerner/ibus/patient/client/PatientClient.java#L28): Retrieves the patient information based on the qualifier.
- [getPatientChangeSubscription](./../../src/main/java/com/cerner/ibus/patient/client/PatientClient.java#L41) - Gets a message subscription to listen to patient change events.
- [savePatients](./../../src/main/java/com/cerner/ibus/patient/client/PatientClient.java#L51): Adds or updates patient data. (For CareAware use only)
- [removePatients](./../../src/main/java/com/cerner/ibus/patient/client/PatientClient.java#L65): Deletes patient for a given set patient Ids. (For CareAware use only)

## Event types supported by the patient client
- ADD
- UPDATE
- REMOVE
- PATIENT HIDE/UNHIDE
- PATIENT COMBINE/UNCOMBINE
- PATIENT ALLERGY CHANGE
- PATIENT ENCNTR MOVE
- UNKNOWN
