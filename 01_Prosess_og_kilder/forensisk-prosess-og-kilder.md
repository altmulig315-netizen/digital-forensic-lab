# Forensisk prosess og kilder

*Digital forensic lab · Høyskolen Kristiania*

Gjennomgang av forelesningsbildene «Prosessen» og «Forensics report», med de profesjonelle standardene og veiledningene som beskriver riktig startprosedyre.

---

## Lysbilde 1: Prosessen, fase for fase

Modellen på bildet er en vanlig femfasemodell. Den er sekvensiell, men dokumentasjon er i praksis noe du gjør hele veien, ikke et eget steg etter analysen.

### 1. Identifisering

*Bildet: utgangspunkt for etterforskning · identifisere ressurser og involverte enheter*

Her avklarer du **hva** du skal svare på og **hvor** bevisene kan finnes, før du rører noe.

- Mandat: hva er spørsmålet, hvem bestilte oppdraget, og hvilken hjemmel har du (samtykke, beslag, intern undersøkelse)?
- Kartlegg enheter: PC-er, telefoner, minnepinner, skylagring, ruter, logger. Ta bilder av åstedet slik det er.
- Vurder hva som er flyktig. RAM, nettverkstilkoblinger og kjørende prosesser forsvinner når maskinen slås av, så rekkefølgen betyr noe.

Kilder: [ISO/IEC 27037](https://www.iso.org/standard/44381.html) (identifisering), [RFC 3227](https://www.rfc-editor.org/rfc/rfc3227) (rekkefølge etter flyktighet), [NIST SP 800-86](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-86.pdf) kap. 3.1

### 2. Preservering

*Bildet: isolere, sikre og preservere data involvert · chain of custody*

Målet er at beviset ikke endres, og at du kan bevise at det ikke er endret.

- Isoler: koble fra nettverk, flymodus eller Faraday-pose for telefoner, slik at ingen kan fjernslette eller endre.
- Les disken gjennom en write blocker (for eksempel Tableau-broen fra labben), aldri gjennom en vanlig dock.
- Lag et bit-for-bit image (E01 eller raw/dd), beregn hash av kilde og image, og sjekk at de er like.
- Chain of custody: et skjema som viser hvem som har hatt beviset, når, hvor og hvorfor, fra beslag til retten.

Kilder: [ACPO prinsipp 1 og 2](https://training-on-eppo.era.int/EPPO/kiosk/pdf/ACPO_Good_Practice_Guide.pdf), [SWGDE Computer Forensic Acquisitions](https://www.swgde.org/wp-content/uploads/2024/03/2023-06-15-SWGDE-Best-Practices-for-Computer-Forensic-Acquisitions-17-F-002-2.0.pdf), [NIST CFTT](https://www.nist.gov/itl/ssd/software-quality-group/computer-forensics-tool-testing-program-cftt) (testrapporter for write blockere)

### 3. Analyse

*Bildet: verktøy og teknikker · prosessere data (play books) · analysere resultater*

Du jobber alltid på kopien, aldri på originalen.

- Verktøy og teknikker: Autopsy, FTK, X-Ways, Volatility, Plaso. Verktøyene skal være validerte, og du noterer versjonsnummer.
- Playbooks er faste oppskrifter for vanlige oppgaver (tidslinje, filgjenoppretting, nettleserhistorikk), slik at to analytikere gjør det likt.
- Analyser resultatene opp mot hypoteser. Let også etter spor som taler **mot** hypotesen din.

Kilder: [ISO/IEC 27041](https://www.iso.org/standard/44405.html) (validering av metoder), [ISO/IEC 27042](https://www.iso.org/standard/44406.html) (analyse og tolkning), [ENFSI BPM-FIT](https://unodc.org/e4j/data/_university_uni_/best_practice_manual_for_the_forensic_examination_of_digital_technology.html?lng=en)

### 4. Dokumentasjon

*Bildet: isolere, sikre og preservere data involvert*

Hva dokumentasjon innebærer:

- Fortløpende notater («bench notes»): hva du gjorde, når, med hvilket verktøy og versjon, og hva resultatet ble.
- Hashverdier, serienumre, bilder av utstyret og chain of custody-skjemaet.
- Nok detaljer til at en annen analytiker kan gjenta arbeidet og få samme resultat (etterprøvbarhet).

Kilder: [ACPO prinsipp 3](https://training-on-eppo.era.int/EPPO/kiosk/pdf/ACPO_Good_Practice_Guide.pdf) (audit trail), [ISO/IEC 27043](https://www.iso.org/standard/44407.html) (prosessmodell der dokumentasjon går parallelt med alle faser)

### 5. Presentasjon

*Bildet: produsere rapport som er forståelig for stakeholdere*

Mottakeren er ofte jurist, leder eller dommer, ikke tekniker. Funnene skal være forståelige uten å miste presisjon, og du skal kunne forsvare dem i et avhør. Lysbilde 2 handler om nettopp denne rapporten.

Kilder: [Forensic Focus: Writing DFIR Reports](https://www.forensicfocus.com/articles/writing-dfir-reports-a-primer/), [UK Forensic Science Regulator Code of Practice](https://www.gov.uk/government/publications/statutory-code-of-practice-for-forensic-science-activities)

---

## Lysbilde 2: Forensics report

Hovedpoenget er at rapporten skrives for andre, men også for deg selv om et halvt år, når du har glemt detaljene og noen stiller spørsmål ved funnene.

| Krav på lysbildet | Hva det betyr | Seksjon i Brunty-malen |
|---|---|---|
| Hva er hensikten med oppdraget | Spørsmålet du skal besvare, hvem som bestilte, og eventuelle søkeord eller hypoteser. | Objectives |
| Hvem og når | Analytiker, oppdragsgiver, dato og klokkeslett for beslag, imaging og analyse. | Title page, Overview |
| Hva som er gjort | Hvert steg, med verktøy og versjon, slik at det kan gjentas. | Forensic Analysis (Steps Taken) |
| Hvilke funn som ble gjort | Funnene forklart for en lekperson og knyttet til målene. | Relevant Findings |
| Konklusjon | Kort svar på spørsmålet, uten å påstå mer enn funnene bærer. | Conclusion |
| Referanser til hardware og arkivsak | Bevisnummer, merke, modell, serienummer, hashverdier og saksnummer. | Evidence, Exhibits |

Eksempel på en bevisreferanse i rapporten:

```
Bevis 01 · Seagate ST1000DM010 · S/N Z9A1XXXX · image sak-2026-014_bevis01.E01 · SHA-256 kilde = image ✓
```

### Collection → Examination → Analysis → Reporting

Pilene nederst på lysbildet er de fire fasene fra NIST SP 800-86. De beskriver samme arbeid som femfasemodellen, bare delt annerledes:

| NIST SP 800-86 | Femfasemodellen | Innhold |
|---|---|---|
| Collection | Identifisering + Preservering | Finne, sikre og avbilde data med integritet bevart. |
| Examination | Analyse (prosessere data) | Hente ut og filtrere relevante data fra imaget, for eksempel filgjenoppretting og parsing. |
| Analysis | Analyse (analysere resultater) | Tolke dataene og trekke slutninger opp mot spørsmålet. |
| Reporting | Dokumentasjon + Presentasjon | Rapporten og forklaringen til mottakeren. |

---

## Startprosedyre: riktig rekkefølge når du starter

Dette er en sammenstilling av ACPO, ISO/IEC 27037, SWGDE og NIST, tilpasset en disk i labben. Rekkefølgen er poenget.

1. **Avklar mandat og hjemmel.** Skriv ned spørsmålet og hvem som har gitt deg tillatelse.
2. **Start notatene.** Dato, klokkeslett, saksnummer. Alt etter dette skrives ned fortløpende.
3. **Fotografer og registrer.** Enheten slik du fant den, merke, modell, serienummer, tilkoblede kabler.
4. **Vurder om maskinen er på.** Er den på, sikre flyktige data først (RAM-dump) etter RFC 3227. Er den av, la den være av.
5. **Isoler og merk beviset.** Koble fra nettverk, legg i beviskonvolutt, start chain of custody-skjemaet.
6. **Test write blockeren.** Bekreft at den faktisk blokkerer skriving før bevisdisken kobles til.
7. **Lag image.** Bit-for-bit, helst E01 med metadata, via write blocker til en ren måldisk.
8. **Verifiser hash.** Kilde og image skal ha lik MD5/SHA-256. Skriv begge inn i notatene.
9. **Legg originalen tilbake i sikker lagring** og jobb kun på en arbeidskopi av imaget.

**ACPO sine fire prinsipper i én setning hver**

- Ikke endre data som kan bli bevis.
- Må du røre originaldata, skal du være kompetent til det og kunne forklare konsekvensene.
- Før en logg over alt som gjøres, slik at en uavhengig tredjepart kan gjenta det.
- Den som leder etterforskningen har ansvar for at loven og prinsippene følges.

---

## Kilderegister: profesjonell dokumentasjon

| Kilde | Hva den er | Faser | Tilgang |
|---|---|---|---|
| [NIST SP 800-86](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-86.pdf) (2006) | Guide to Integrating Forensic Techniques into Incident Response. Kilden til Collection/Examination/Analysis/Reporting. | Alle | Gratis |
| [NIST SP 800-61 rev. 3](https://csrc.nist.gov/pubs/sp/800/61/r3/final) (2025) | Hendelseshåndtering. Nyttig når forensikk er en del av en sikkerhetshendelse. | Identifisering | Gratis |
| [RFC 3227](https://www.rfc-editor.org/rfc/rfc3227) | Guidelines for Evidence Collection and Archiving. Kort og klassisk om rekkefølge etter flyktighet. | Identifisering, Preservering | Gratis |
| [ISO/IEC 27037](https://www.iso.org/standard/44381.html) | Identifisering, innsamling, anskaffelse og bevaring av digitale bevis. | Identifisering, Preservering | Betalt |
| [ISO/IEC 27041](https://www.iso.org/standard/44405.html) | Sikre at undersøkelsesmetodene er egnet og validert. | Analyse | Betalt |
| [ISO/IEC 27042](https://www.iso.org/standard/44406.html) | Analyse og tolkning av digitale bevis. | Analyse, Presentasjon | Betalt |
| [ISO/IEC 27043](https://www.iso.org/standard/44407.html) | Overordnet prosessmodell for hendelsesetterforskning. | Alle | Betalt |
| [ACPO Good Practice Guide v5](https://training-on-eppo.era.int/EPPO/kiosk/pdf/ACPO_Good_Practice_Guide.pdf) (2012) | Britisk politiveileder med de fire prinsippene som siteres overalt. | Preservering, Dokumentasjon | Gratis |
| [FSR Code of Practice](https://www.gov.uk/government/publications/statutory-code-of-practice-for-forensic-science-activities) | Britisk lovpålagt kvalitetskrav for forensiske aktiviteter, inkludert digitale. | Analyse, Presentasjon | Gratis |
| [SWGDE](https://www.swgde.org/documents/published-complete-listing/) | Amerikanske best practices. Start med [Computer Forensic Acquisitions](https://www.swgde.org/wp-content/uploads/2024/03/2023-06-15-SWGDE-Best-Practices-for-Computer-Forensic-Acquisitions-17-F-002-2.0.pdf). | Preservering | Gratis |
| [NIST CFTT](https://www.nist.gov/itl/ssd/software-quality-group/computer-forensics-tool-testing-program-cftt) | Uavhengige testrapporter for write blockere og imaging-verktøy, blant annet Tableau. | Preservering | Gratis |
| [ENFSI BPM-FIT](https://unodc.org/e4j/data/_university_uni_/best_practice_manual_for_the_forensic_examination_of_digital_technology.html?lng=en) (2015) | Europeisk beste praksis for undersøkelse av digital teknologi. | Alle | Via ENFSI |
| [Writing DFIR Reports: A Primer](https://www.forensicfocus.com/articles/writing-dfir-reports-a-primer/) | Josh Brunty, Forensic Focus 2021. Lenken fra lysbildet, med en ferdig rapportmal. | Dokumentasjon, Presentasjon | Gratis |
| [Årnes (red.): Digital Forensics](https://www.wiley-vch.de/en/areas-interest/natural-sciences/digital-forensics-978-1-119-26238-1) (Wiley 2017) | Lærebok skrevet av norske fagfolk fra NTNU- og politimiljøet. | Alle | Bok |
| [NSMs grunnprinsipper for IKT-sikkerhet v2.1](https://nsm.no/getfile.php/1313975-1717589722/NSM/Filer/Dokumenter/Veiledere/NSMs%20Grunnprinsipper%20for%20IKT-sikkerhet%20v2.1.pdf) | Norsk. Kategori 4, «Håndtere og gjenopprette», dekker hendelseshåndtering. | Identifisering | Gratis |
| [Straffeprosessloven](https://lovdata.no/dokument/NL/lov/1981-05-22-25) | Norsk hjemmel for beslag (kap. 16) og tilgang til datasystemer (§ 199 a). | Identifisering | Gratis |

ISO-standardene kan kjøpes via Standard Norge. Sjekk om biblioteket på Kristiania har tilgang før du betaler.

---

*Laget 10. oktober 2026 for William, Digital forensic lab. Lenkene ble kontrollert samme dag. Lysbildeinnholdet er fra Høyskolen Kristiania.*
