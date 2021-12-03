<details>

<summary>us English version (click here)</summary>

# Catmandu_PICAtoBibTex

Transformation of bibliographic data from PICA+ format to BibTeX format for RILM

The German editorial office of the Répertoire International de Littérature Musiicale (RILM) is located at the State Institute for Music Research (SIM). As such, the SIM transmits all entries of the [Bibliographie des Musikschrifttums](https://www.musikbibliographie.de/) (BMS) appearing in Germany to the central editorial office of [RILM Abstracts of Music Literature](https://www.rilm.org/abstracts/) on a quarterly basis. The bibliographic data of the BMS are in PICAplus format and must be transformed into BibTeX format for further processing in the RILM central editorial office. For this purpose, the SIM uses the command line tool Catmandu. Further information on Catmandu is available here https://librecat.org/Catmandu. 

* [festschrift_proceeding.fix](Catmandu_PICAtoBibTex/festschrift_proceeding.fix) selects the IDs of all conference and festschriften and assigns the RILM-tag to them. The selected RILM-tags and IDs are written to a csv file and in a later step transferred to the articles contained in the conference and festschrift proceedings.
* The script [countrycode_collection.fix](Catmandu_PICAtoBibTeX/countrycode_collection.fix) selects the country codes and IDs of all anthologies. The loader codes are written to a csv file and transferred to the essays contained in the anthologies in a later step.
* [countrycode_journal.fix](Catmandu_PICAtoBibTeX/countrycode_journal.fix) selects the country codes and IDs of all journals. The loader codes are written to a csv file and in a later step transferred to the articles contained in the journals.
* [BibTeX.pm](Catmandu_PICAtoBibTeX/BibTeX.pm) contains some RILM specific fields in BibTeX which are not supported in the original module.
* [note.csv](Catmandu_PICAtoBibTeX/note.csv) contains the illustration details of the PICA field 034M and the corresponding RILM tag.
* [picafix.fix](Catmandu_PICAtoBibTeX/picafix.fix) contains the script for transforming the necessary PICA+ data into the BibTeX format.
* [replace.fix](Catmandu_PICAtoBibTeX/replace.fix) is needed for cleaning up the transformed data.

# required Catmandu modules

* [Catmandu::PICA](https://metacpan.org/dist/Catmandu-PICA)
* [Catmandu::BibTeX](https://metacpan.org/pod/Catmandu::BibTeX)

# Use of the files

1. installation of Catmandu and the required modules.
2. download all files into the home directory.
3. replace the file [BibTeX.pm](Catmandu_PICAtoBibTeX/BibTeX.pm) under the path "/home/kim/perl5/perlbrew/perls/perl-5.30.3/lib/site_perl/5.30.3/Catmandu/Exporter/BibTeX.pm" with the file contained here.
3. place the file with the PICA+ data (dmpbms.pp) also in the home directory.
4. validation of the PICA+ data. For example with [Catmandu::Validator::PICA](https://metacpan.org/pod/Catmandu::Validator::PICA).
5. using the command "catmandu convert PICA --type plain to CSV --fix festschrift_proceeding < dmpbms.pp > festschrift_proceeding_ppn.csv" in the command line, create a list with all IDs of the conference and festschrifts and the corresponding RILM-tags for the included essays. Insert "$ less festschrift_proceeding_ppn.csv" into the header. 
6. use the command "catmandu convert PICA --type plain to CSV --fix countrycode_collection.fix < dmpbms.pp > countrycodelist.csv" in the command line to create a list with all IDs and the corresponding country codes of the anthologies. Insert "$ less countrycodelist.csv" in the header. 
Use the command "catmandu convert PICA --type plain to CSV --fix countrycode_journal.fix < dmpbms.pp > countrycodelist_journal.txt" in the command line to create a list with all IDs and the corresponding country codes of the journals. Paste the contents of the list into the "countrycodelist.csv" file. 8.
8. with the command "catmandu convert PICA --type plain to BibTeX --fix picafix.fix --fix replace.fix < dmpbms.pp > dmpbms.btx" in the command line the actual transformation and cleaning of the data is executed.
9. some BibTeX fields need a RILM specific naming. For this a postprocessing with an editor is necessary. The following fields and contents have to be renamed:
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

# Licenses

The file [BibTeX.pm](Catmandu_PICAtoBibTex/BibTeX.pm) is licensed with perl_5. All other files are [CCO](https://creativecommons.org/share-your-work/public-domain/cc0/).


</details>

---

<details open>

<summary>DE Deutsche Version</summary>


# Catmandu_PICAtoBibTex

Transformation bibliographischer Daten aus dem Format PICA+ in das Format BibTeX für RILM

Am Staatlichen Institut für Musikforschung (SIM) befindet sich die deutsche Redaktion des Répertoire International de Littérature Musiicale (RILM). Als diese übermittelt das SIM vierteljährlich alle in Deutschland erscheinenden Einträge der [Bibliographie des Musikschrifttums](www.musikbibliographie.de/) (BMS) an die Zentralredaktion von [RILM Abstracts of Music Literature](https://www.rilm.org/abstracts/). Die bibliographischen Daten der BMS liegen im PICAplus-Format vor und müssen für die Weiterverarbeitung in der RILM-Zentralredaktion in das Format BibTeX transformiert werden. Dafür nutzt das SIM das Kommandozeilentool Catmandu. Weitere Informationen zu Catmandu gibt hier https://librecat.org/Catmandu. 

# Beschreibung der Dateien

* [festschrift_proceeding.fix](Catmandu_PICAtoBibTex/festschrift_proceeding.fix) selektiert die IDs aller Konferenz- und Festschriften und ordnet ihnen den RILM-tag zu. Die selektierten RILM-tags und IDs werden in eine csv-Datei geschrieben und in einem späteren Schritt auf die in den Konferenz- und Festschriften enthaltenen Aufsätzen übertragen.
* Das Script [countrycode_collection.fix](Catmandu_PICAtoBibTeX/countrycode_collection.fix) selektiert die Ländercodes und IDs aller Sammelbände. Die Lädercodes werden in eine csv-Datei geschrieben und in einem späteren Schritt auf die in den Sammelbänden enthaltenen Aufsätze übertragen.
* [countrycode_journal.fix](Catmandu_PICAtoBibTex/countrycode_journal.fix) selektiert die Ländercodes und IDs aller Zeitschriften. Die Lädercodes werden in eine csv-Datei geschrieben und in einem späteren Schritt auf die in den Zeitschriften enthaltenen Aufsätze übertragen.
* [BibTeX.pm](Catmandu_PICAtoBibTex/BibTeX.pm) enthält einige RILM-spezifische Felder in BibTeX, die im ursprünglichen Modul nicht unterstützt werden.
* [note.csv](Catmandu_PICAtoBibTex/note.csv) enthält die Illustrationsangaben des PICA-Feldes 034M und den entsprechenden RILM-tag.
* [picafix.fix](Catmandu_PICAtoBibTeX/picafix.fix) enthält das Script für die Transformation der notwendigen PICA+ Daten in das Format BibTeX.
* [replace.fix](Catmandu_PICAtoBibTeX/replace.fix) wird für die Bereinigung der transformierten Daten benötigt.

#  benötigte Catmandu-Module

* [Catmandu::PICA](https://metacpan.org/dist/Catmandu-PICA)
* [Catmandu::BibTeX](https://metacpan.org/pod/Catmandu::BibTeX)

# Verwendung der Dateien

1. Installation von Catmandu und der benötigten Module.
2. Download aller Dateien in das Home-Verzeichnis.
3. Die Datei [BibTeX.pm](Catmandu_PICAtoBibTeX/BibTeX.pm) unter dem Pfad "/home/kim/perl5/perlbrew/perls/perl-5.30.3/lib/site_perl/5.30.3/Catmandu/Exporter/BibTeX.pm" mit der hier enthaltenen Datei ersetzen.
3. Die Datei mit den PICA+ Daten (dmpbms.pp) ebenfalls im Home-Verzeichnis ablegen.
4. Validation der PICA+ Daten. Zum Beispiel mit [Catmandu::Validator::PICA](https://metacpan.org/pod/Catmandu::Validator::PICA).
5. Mit dem Befehl "catmandu convert PICA --type plain to CSV --fix festschrift_proceeding < dmpbms.pp > festschrift_proceeding_ppn.csv" in der Kommandozeile eine Liste mit allen IDs der Konferenz- und Festschriften erstellen und den dazugehörigen RILM-tags für die enthaltenen Aufsätze. In den header "$ less festschrift_proceeding_ppn.csv" einfügen. 
6. Mit dem Befehl "catmandu convert PICA --type plain to CSV --fix countrycode_collection.fix < dmpbms.pp > countrycodelist.csv" in der Kommandozeile eine Liste mit allen IDs und den dazugehörigen Ländercodes der Sammelbände erstellen. In den header "$ less countrycodelist.csv" einfügen. 
7. Mit dem Befehl "catmandu convert PICA --type plain to CSV --fix countrycode_journal.fix < dmpbms.pp > countrycodelist_journal.txt" in der Kommandozeile eine Liste mit allen IDs und den dazugehörigen Ländercodes der Zeitschriften erstellen. Den Inhalt der Liste in die Datei "countrycodelist.csv" einfügen.
8. Mit dem Befehl "catmandu convert PICA --type plain to BibTeX --fix picafix.fix --fix replace.fix < dmpbms.pp > dmpbms.btx" in der Kommandozeile wird die eigentliche Transformation und Bereinigung der Daten ausgeführt.
9. Einige BibTeX-Felder benötigen eine RILM-spezifische Benennung. Dafür ist eine Nachbearbeitung mit einem Editor notwendig. Folgende Felder und Inhalte müssen umbenannt werden:
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

# Lizenzen

Die Datei [BibTeX.pm](Catmandu_PICAtoBibTex/BibTeX.pm) ist mit perl_5 lizensiert. Alle anderen Dateien sind [CCO](https://creativecommons.org/share-your-work/public-domain/cc0/).

</details>

---
