---
layout: post
published: false
title: Sonarqube - wprowadzenie do statycznej analizy kodu
tags:
  - craftsmanship
---
Pamiętam jak kilka lat temu z uporem maniaka integrowałem biblioteki statycznej analizy kodu do każdego pom.xml, który wpadł w moje ręce. Do dzisiaj wiele osób za to mnie szczerze nienawidzi. Modyfikacja pomów, konfiguracja komitowana do repozytorium i długie instrukcje na wiki związane z integracją IDE. Patrząc z perspektywy czasu przyznaję, że był to dość pracochłonne przedsięwzięcie. Na szczęście pojawiło się narzędzie, które nie tylko uprościło proces statycznej analizy kodu, ale także znacznie tę analizę upowszechniło.

##Konfiguracja
SonarQube, bo o nim mowa, powstał jako narzędzie do integracji raportów z różnych bibliotek i wizualizacji wyników. Twórcy byli rozczarowani tempem zmian w popularnych bibliotekach statycznej analizy kodu, dlatego zaczęli na własną rękę przygotowywać zestaw reguł, które ich zdaniem powinien spełniać dobry kod. W wyniku tego procesu dostaliśmy kompleksowe narzędzie do zbierania analiz i raportowania jakościowych zmian projektu w czasie. 

W erze przedokerowej, takie wprowadzenie zajęłobyby pewnie kilka ekranów poleceń i czyności konfiguracyjnych. Ja pokażę, że cały proces konfiguracji i pierwszego użycia można zamknąć w 4 poleceniach, z których jedno to zmiana bieżącego katalogu.

Sciągnięcie i uruchomienie serwera w domyślnej konfiguracji osiągniemy wydając polecenie:
```bash
docker run -d --name sonarqube -p 9000:9000 -p 9092:9092 sonarqube
```

Następnie potrzebujemy projekt, który poddamy analizie. Dla celów pokazowych weźmy szkielet aplikacji, który każdy z nas niejednokrotnie użył:
```bash
mvn archetype:generate 
	-DgroupId=com.mycompany.app 
    -DartifactId=my-app 
    -DarchetypeArtifactId=maven-archetype-quickstart 
    -DinteractiveMode=false
```

Na koniec pozostaje nam zmienić katalog i uruchomić analizę:
```bash
cd my-app
mvn sonar:sonar
```

Po zakończeniu przechodzimy na stronę _http://localhost:9000_ i powinnismy zobaczyć gotowy raport. Tym, co nas początku najbardziej nas interesuje są _smrodki_ czyli Code Smells:



##Praktyka
##Podsumowanie
Zachęcam każdego, aby uruchomił lokalnie SonarQube i przeskanował swoje projekty (o ile jeszcze tego nie robi). Wiedza, jaka płynie z takiej operacji jest nie do przecenienia.
