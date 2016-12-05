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

Po zakończeniu przechodzimy na stronę _http://localhost:9000_ i powinnismy zobaczyć gotowy raport. Tym, co nz as początku najbardziej nas interesuje są _smrodki_ znalezione w kodzie czyli Code Smells:

![2016-12-05-sonarqube1.png]({{site.baseurl}}/img/2016-12-05-sonarqube1.png)

Ja możemy zobaczyć, w tak niewielkim fragmencie kodu, SonarQube namierzył aż trzy naruszenia! Nawigując po interfejsie mozemy przenazalizować okoliczności, w jakis zostało wprodzadzone każde naruszenie oraz zapoznać się z bardzo szczegółową dokumentacją. Każdy zdiagnozowany problem ma nie tylko opisaną przyczynę zakwalifikowania go jako Code Smell ale także przykłady i instrukcje, jak takie naruszenie można z kodu wyeliminować. I to właśnie tutaj ukryte są niezgłębione pokłady wiedzy na temat filozofii czystego kodu.

Należy w tym momencie zaznaczyć, że przedstawiona powyżej metoda jest odpowiednia do lokalnej metody analizy kodu. Jeśli zdecydujemy się wdrożyć w projekcie SonaQube jako narzędzie używane przez wielu programistów, warto poswięcić trochę czasu i skonfigurować przynajmniej takie elementy jak uwierzytelnianie, autoryzacja oraz dedykowana baza danych.

##Środowisko developerskie

Przeglądanie raportów i statystyk projektu pozostawmy jednak w gestii managerów. To, czego potrzebują programiści to integracji na poziomie środowiska IDE, możliwie jak nabliżej kodu. I tutaj z pomocą przychodzi nam plugin SonarLint, dostępny na wszystkie liczące się środowiska programistyczne. Wystraczy, że wskażemy mu serwer:

![2016-12-05-sonarqube2.png]({{site.baseurl}}/img/2016-12-05-sonarqube2.png)

Powiążemy bierzący projekt z projektem założonym na serwerze:

![2016-12-05-sonarqube3.png]({{site.baseurl}}/img/2016-12-05-sonarqube3.png)

Jeśli integracja przebiegnie poprawnie, wszystkie naruszenia na serwerze powinny zostać naniesione na plik otwarty w edytorze:

![2016-12-05-sonarqube4.png]({{site.baseurl}}/img/2016-12-05-sonarqube4.png)

##Podsumowanie
Zachęcam każdego, aby uruchomił lokalnie SonarQube i przeskanował swoje projekty (o ile jeszcze tego nie robi). Wiedza, jaka płynie z takiej operacji jest nie do przecenienia. Jeżeli zainteresuje was ten sposób analizy kody, warto zgłębić inne funkcjonalności jakie posiada SonarQube. Znajdziemy tam między innymi: 
* analizę pokrycia kodu testami
* wykrywanie copy'n'paste
* złożoność cyklomatyczną