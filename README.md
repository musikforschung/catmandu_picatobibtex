<details>

<summary>us English version (click here)</summary>

# Catmandu_PICAtoBibTex

Transformation of bibliographic data from PICA+ format to BibTeX format for RILM

The German editorial office of the Répertoire International de Littérature Musiicale (RILM) is located at the Staatliches Institut für Musikforschung (SIM). As such, the SIM transmits all entries of the [Bibliographie des Musikschrifttums](https://www.musikbibliographie.de/) (BMS online) published in Germany to the central editorial office of [RILM Abstracts of Music Literature](https://www.rilm.org/abstracts/) on a quarterly basis. The bibliographic data of the BMS online are in PICAplus format and has to be transformed into BibTeX format for further processing in the RILM central editorial office. For this purpose, the SIM uses the command line tool Catmandu. Further information on Catmandu is available here https://librecat.org/Catmandu. 

# Files description

* [BibTeX_bms.pm](https://github.com/musikforschung/Catmandu_PICAtoBibTeX/blob/main/BibTeX_bms.pm) contains some RILM-specific tags that are not supported in the original Catmandu [BibTeX module](https://github.com/LibreCat/Catmandu-BibTeX/tree/main/lib/Catmandu/Exporter): abstractor, author_afterword, author_collaborator, author_commentator, author_compiled, author_foreword, author_illustrator, author_introduction, author_supervisor, author_translator, country, crossref, eventdate, eventtitle, honoured, language_original, reviewed-item.
* [countrycode.fix](https://github.com/musikforschung/Catmandu_PICAtoBibTeX/blob/main/countrycode.fix) selects the country codes and IDs of all journals and collections. The loader codes are written to a csv file and transferred to the essays contained in the journals or collections in a later step.
* [festschrift_proceeding.fix](https://github.com/musikforschung/Catmandu_PICAtoBibTeX/blob/main/festschrift_proceeding.fix) selects the IDs of all conference and festschriften and assigns the RILM-tag to them. The selected RILM-tags and IDs are written to a csv file and in a later step transferred to the articles contained in the conference and festschrift proceedings.
* [note.csv](https://github.com/musikforschung/Catmandu_PICAtoBibTeX/blob/main/note.csv) contains the illustration details of the PICA field 034M and the corresponding RILM tag.
* [picafix.fix](https://github.com/musikforschung/Catmandu_PICAtoBibTeX/blob/main/picafix.fix) contains the script for transforming the necessary PICA+ data into the BibTeX format.
* [replace.fix](https://github.com/musikforschung/Catmandu_PICAtoBibTeX/blob/main/replace.fix) is needed for cleaning up the transformed data.

# Required Catmandu modules

* [Catmandu::PICA](https://metacpan.org/dist/Catmandu-PICA)
* [Catmandu::BibTeX](https://metacpan.org/pod/Catmandu::BibTeX)

# Use of the files

1. Validation of the PICA+ data. For example with [Catmandu::Validator::PICA](https://metacpan.org/pod/Catmandu::Validator::PICA).
2. Using the command "catmandu convert PICA --type plain to CSV --fix festschrift_proceeding.fix < dmpbms.pp > festschrift_proceeding_ppn.csv | catmandu convert PICA --type plain to CSV --fix countrycode.fix < dmpbms.pp > countrycodelist.csv" in the command line, create a list of all IDs of proceedings, festschrifts and journals with the corresponding RILM-tags respectively country codes for the included essays.
3. With the command "catmandu convert PICA --type plain to BibTeX --fix picafix.fix --fix replace.fix < dmpbms.pp > dmpbms.btx" in the command line the actual transformation and cleaning of the data is executed.
4. Some BibTeX fields need a RILM specific naming. For this a postprocessing with an editor is necessary. The following fields and contents have to be renamed:
* "@er{" -> "@book{"
* "@dd{" -> "@dissertation{"
* "@dm{" -> "@thesis{"
* "type = {book}" -> "type = {bm}"
* "type = {journal}" -> "type = {bp}"
* "type = {article}" -> "type = {ap}"
* "type = {collection}" -> "type = {bc}"
* "@be{" -> "@collection{"
* "type = {incollection}" -> "type = {ac}"
* "@ae{" -> "@incollection{"
* "@as{" -> "@incollection{"
* "type = {video}" -> "type = {mp}"
* "type = {audio}" -> "type = {mr}"
* "type = {proceedings}" -> "type = {bs}"

# Authors

* [BibTeX_bms.pm](https://github.com/musikforschung/Catmandu_PICAtoBibTeX/blob/main/BibTeX_bms.pm):
Nicolas Steenlant, nicolas.steenlant at ugent.be; edited by René Wallor

* files included in [Fix_bms](https://github.com/musikforschung/Catmandu_PICAtoBibTeX/blob/main/Fix_bms):
René Wallor, wallor at sim.spk-berlin.de

# Contributors

* [picafix.fix](https://github.com/musikforschung/Catmandu_PICAtoBibTeX/blob/main/picafix.fix):
Johann Rolschewski, jorol at cpan.org

# License an copyright

* [BibTeX_bms.pm](https://github.com/musikforschung/Catmandu_PICAtoBibTeX/blob/main/BibTeX_bms.pm):
Copyright (c) 2021 by Nicolas Steenlant

* files in [Fix_bms](https://github.com/musikforschung/Catmandu_PICAtoBibTeX/blob/main/Fix_bms):
Copyright (c) 2022 Stiftung Preußischer Kulturbesitz - Staatliches Institut für Musikforschung

This program is free software; you can redistribute it and/or modify it under the terms of either: the GNU General Public License as published by the Free Software Foundation; or the Artistic License.

See http://dev.perl.org/licenses/ for more information. 


</details>

---

<details open>

<summary>DE Deutsche Version</summary>


# Catmandu_PICAtoBibTex

Transformation bibliographischer Daten aus dem Format PICA+ in das Format BibTeX für RILM

Am Staatlichen Institut für Musikforschung (SIM) befindet sich die deutsche Redaktion des Répertoire International de Littérature Musiicale (RILM). Als diese übermittelt das SIM vierteljährlich alle in Deutschland erscheinenden Einträge der [Bibliographie des Musikschrifttums](https://www.musikbibliographie.de/) (BMS online) an die Zentralredaktion von [RILM Abstracts of Music Literature](https://www.rilm.org/abstracts/). Die bibliographischen Daten aus BMS online liegen im PICAplus-Format vor und müssen für die Weiterverarbeitung in der RILM-Zentralredaktion in das Format BibTeX transformiert werden. Dafür nutzt das SIM das Kommandozeilentool Catmandu. Weitere Informationen zu Catmandu gibt hier https://librecat.org/Catmandu. 

# Beschreibung der Dateien

* [BibTeX_bms.pm](https://github.com/musikforschung/Catmandu_PICAtoBibTeX/blob/main/BibTeX_bms.pm) enthält einige RILM-spezifische tags, die im ursprünglichen Catmandu [BibTeX Modul](https://github.com/LibreCat/Catmandu-BibTeX/tree/main/lib/Catmandu/Exporter) nicht unterstützt werden: abstractor, author_afterword, author_collaborator, author_commentator, author_compiled, author_foreword, author_illustrator, author_introduction, author_supervisor, author_translator, country, crossref, eventdate, eventtitle, honoured, language_original, reviewed-item.
* [countrycode.fix](https://github.com/musikforschung/Catmandu_PICAtoBibTeX/blob/main/countrycode.fix) selektiert die Ländercodes und IDs aller Zeitschriften und Sammelbände. Die Ländercodes werden in eine csv-Datei geschrieben und in einem späteren Schritt auf die in den Zeitschriften und Sammelbänden enthaltenen Aufsätze übertragen.
* [festschrift_proceeding.fix](https://github.com/musikforschung/Catmandu_PICAtoBibTeX/blob/main/festschrift_proceeding.fix) selektiert die IDs aller Konferenz- und Festschriften und ordnet ihnen den entsprechenden RILM-tag zu. Die selektierten RILM-tags und IDs werden in eine csv-Datei geschrieben und in einem späteren Schritt auf die in den Konferenz- und Festschriften enthaltenen Aufsätzen übertragen.
* [note.csv](https://github.com/musikforschung/Catmandu_PICAtoBibTeX/blob/main/note.csv) enthält die Illustrationsangaben des PICA-Feldes 034M und den entsprechenden RILM-tag.
* [picafix.fix](https://github.com/musikforschung/Catmandu_PICAtoBibTeX/blob/main/picafix.fix) enthält das Script für die Transformation der notwendigen PICA+ Daten in das Format BibTeX.
* [replace.fix](https://github.com/musikforschung/Catmandu_PICAtoBibTeX/blob/main/replace.fix) wird für die Bereinigung der transformierten Daten benötigt.

#  benötigte Catmandu-Module

* [Catmandu::PICA](https://metacpan.org/dist/Catmandu-PICA)
* [Catmandu::BibTeX](https://metacpan.org/pod/Catmandu::BibTeX)

# Verwendung der Dateien

1. Validation der PICA+ Daten. Zum Beispiel mit [Catmandu::Validator::PICA](https://metacpan.org/pod/Catmandu::Validator::PICA).
2. Mit dem Befehl "catmandu convert PICA --type plain to CSV --fix festschrift_proceeding.fix < dmpbms.pp > festschrift_proceeding_ppn.csv | catmandu convert PICA --type plain to CSV --fix countrycode.fix < dmpbms.pp > countrycodelist.csv" in der Kommandozeile eine Liste aller IDs der Zeitschriften sowie der Konferenz- und Festschriften mit den dazugehörigen Ländercodes bzw. RILM-tags für die enthaltenen Aufsätze erstellen.
3. Mit dem Befehl "catmandu convert PICA --type plain to BibTeX --fix picafix.fix --fix replace.fix < dmpbms.pp > dmpbms.btx" in der Kommandozeile wird die eigentliche Transformation und Bereinigung der Daten ausgeführt.
4. Einige BibTeX-Felder benötigen eine RILM-spezifische Benennung. Dafür ist eine Nachbearbeitung mit einem Editor notwendig. Folgende Felder und Inhalte müssen umbenannt werden:
* "@er{" -> "@book{"
* "@dd{" -> "@dissertation{"
* "@dm{" -> "@thesis{"
* "type = {book}" -> "type = {bm}"
* "type = {journal}" -> "type = {bp}"
* "type = {article}" -> "type = {ap}"
* "type = {collection}" -> "type = {bc}"
* "@be{" -> "@collection{"
* "type = {incollection}" -> "type = {ac}"
* "@ae{" -> "@incollection{"
* "@as{" -> "@incollection{"
* "type = {video}" -> "type = {mp}"
* "type = {audio}" -> "type = {mr}"
* "type = {proceedings}" -> "type = {bs}"

# Autoren

* [BibTeX_bms.pm](https://github.com/musikforschung/Catmandu_PICAtoBibTeX/blob/main/BibTeX_bms.pm):
Nicolas Steenlant, nicolas.steenlant at ugent.be; bearbeitet von René Wallor

* Skripte in [Fix_bms](https://github.com/musikforschung/Catmandu_PICAtoBibTeX/blob/main/Fix_bms):
René Wallor, wallor at sim.spk-berlin.de

# Mitwirkende

* [picafix.fix](https://github.com/musikforschung/Catmandu_PICAtoBibTeX/blob/main/picafix.fix):
Johann Rolschewski, jorol at cpan.org

# Lizenz und Copyright

* [BibTeX_bms.pm](https://github.com/musikforschung/Catmandu_PICAtoBibTeX/blob/main/BibTeX_bms.pm):
Copyright (c) 2021 by Nicolas Steenlant

* Skripte in [Fix_bms](https://github.com/musikforschung/Catmandu_PICAtoBibTeX/blob/main/Fix_bms):
Copyright (c) 2022 Stiftung Preußischer Kulturbesitz - Staatliches Institut für Musikforschung

This program is free software; you can redistribute it and/or modify it under the terms of either: the GNU General Public License as published by the Free Software Foundation; or the Artistic License.

See http://dev.perl.org/licenses/ for more information.

</details>

---
