#GIT Ein Crashkurs
##1 Einleitung:
GIT = ein Versionssystem, zur Verwaltung von Textdateien
###1.1 Idee:
Verschiedene Benutzer besitzen jeweils ein eigens lokales Repository sowie dessen History.
Repositories können dann zusammengeführt werden.
###1.2 github.com
Webplattform auf der Repositories einfach „gelagert“ werden können.
###1.3 Installation:
```apt install git git-gui```
##2 Anlegen eines Repositories:
###2.1 Lokal am Rechner:
Im gewünschten Verzeichnis (mit oder ohne Inhalt):
```git init```
###2.2 auf github.com:
Durchklicken und README.md & Lizenz & .gitignore anlegen
##3 github – Repository auf lokalen Rechner holen:
```git clone https://github.com/<eigener Name auf github>/Repository – Name>```
Das lokale Repository ist automatisch mit dem remote – Repository auf github.com verbunden.
Siehe Datei .git/config und einige mehr:
[remote "origin"]
	url = http://github.com/edvapp/networkbox

##4 Lokales und remote Repository verbinden:
Dieser Punkt kann für geklonte Repositories entfallen. Daher empfiehlt sich, zuerst das Repository auf github.com anzulegen, zu klonen und dann erst die Änderungen wieder zurückzuschreiben.
Siehe:
https://help.github.com/articles/adding-an-existing-project-to-github-using-the-command-line/#platform-linux
###4.1 Remote Repository bekannt machen:
```git remote add origin https://github.com/<eigener Name auf github>/Repository – Name>```
###4.2 Remote Repository verifizieren:
```git remote -v```
###4.3 Daten von remote ins lokale Repository holen:
```git pull origin master```

##5 Lokale Änderung commiten:
Im git – Repository = lokales Verzeichnis:
###5.1 Änderungen erzeugen
```
echo „Hello World“ > myGit1.txt
echo „Hallo Welt“ > myGit2.txt
```
###5.2 Status betrachten:
```git status```
###5.3 Änderung zum Commit vormerken:
```
git add myGit1.txt
git status
```
###5.4 Commit durchführen:
```git commit -m „Commit Numer 1“```
###5.5 Commit – History  betrachten:
```git log --oneline --decorate --graph --all```
###5.6 Langen Befehl als alias speichern:
```
git config --global alias.hist 'log --oneline --decorate --graph –all'
```
oder

In Datei "homeverzeichnis"/.gitconfig
die Zeile:
```
[alias]
	hist = log --oneline --decorate --graph --all
```
einfügen
###5.7 Commit – History betrachten:
```git hist```

###5.8 Änderungen/Differenzen betrachten:
```
git status
echo „schon wieder eine Welt“ > myGit1.txt
git add myGit1.txt
git diff
```
zeigt die Differenzen zwischen dem augenblicklichen Stand und dem letzten Commit.
```
git commit -m „Commit Numer 2“
```

###5.9 Änderung rückgängig machen:
```
git status
git add .
git commit -m „Commit Numer 3“
git hist
git reset HEAD~1
git hist
```
Bemerkung:
```
git reset HEAD~2 setzt den HEAD – Pointer um 2 Commits zurück.
```
###5.10 Von GIT überwachte Dateien aus GIT entfernen:
Die Datei myGit2.txt wird nicht mehr gebraucht und soll aus der Überwachung entfernt werden.
```
git rm myGit2.txt
git status
git commit -m „Commit Nummer 4“
```
##6 Commits zurück nach origin = github.com pushen:
###6.1 Sich selbst für/bei git „bekannt machen“:
```
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```
###6.2 ERSTE Commits nach remote pushen:
```
git push origin master
```
evt. ```git push -u origin master Achtung -u nur hier nötig.```
###6.3 12. ALLE SPÄTEREN Commits nach remote pushen:
```
git status
echo „Hello noch ein Planet“ >> myGit2.txt
git status
git commit -m „Commit Numer 4 oder 3? ;-)“
git push
```
###6.4 Zurückgesetzten Commit mit Gewalt nach remote pushen:
```
git status
git reset HEAD~1
git status
git push -f
```

##7 Mit dem Fork Workflow an Projekten beitragen
###7.1 „Forken“
https://www.atlassian.com/git/tutorials/comparing-workflows/forking-workflow 
Eine serverseitige Kopie Clonen: entspricht dem Forken auf Github.com
###7.2 Eine Verbindung zum Projekt Maintainer Repo schaffen
```git remote add upstream https://github.org/maintainer/repo```
###7.3 Code aktuell halten
Den eigenen Code mit dem des Maintainers immer wieder mal aktualisieren:
```
git pull upstream master
```
###7.4 Arbeiten wie sonst mit git
###7.5 Zusammenführen von Code: Pull Request
Um überprüfte Änderungen begutachten und einpflegen zu lassen: Pull Request über die Seite github.org erstellen.

##8 Nützliche Links
Von Innsbrucker Informatik Intitut an der Uni, die Herangehensweise bei ihren Projekten mit einem anschaulichem Bild:
https://iis.uibk.ac.at/collab/git

git mit Hilfe und ohne Installtion für SchülerInnen ausprobieren (achtung Englisch)
https://try.github.io

Sehr umfangreiche Anleitung (von dort hab ich auch ein paar Bilder zum Erklären beim Worshop vorgezeigt):
https://www.atlassian.com/git/tutorials/what-is-version-control

Ein grafischer Spickzettel für Git (beschränkt sich auf das lokale Arbeiten)
https://marklodato.github.io/visual-git-guide/index-de.html
