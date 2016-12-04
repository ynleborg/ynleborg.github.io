---
layout: post
published: false
title: Sonarqube - wprowadzenie do statycznej analizy kodu
tags:
  - craftsmanship
---
Pamiętam jak kilka lat temu z uporem maniaka integrowałem biblioteki statycznej analizy kodu do każdego pom.xml, który wpadł w moje ręce. Do dzisiaj wiele osób za to mnie szczerze nienawidzi. Modyfikacja pomów, konfiguracja komitowana do repozytorium i długie instrukcje na wiki związane z integracją IDE. Patrząc z perspektywy czasu przyznaję, że nie był to dość pracochłonne przedsięwzięcie. Na szczęście pojawiło się narzędzie, które nie tylko uprościło proces statycznej analizy kody, ale także znacznie tę analizę upowszechniło.

##Konfiguracja
SonarQube, bo o nim mowa, powstał jako narzędzie do integracji raportów z różnych bibliotek i wizualizacji wyników. Twórcy byli rozczarowani tempem zmian w popularnych bibliotekach statycznej analizy kodu, dlatego zaczęli na własną rękę przygotowywać zestaw reguł, które ich zdaniem powinien spełniać dobry kod. W wyniku tego procesu dostaliśmy kompleksowe narzędzie do zbierania analiz i raportowania jakościowych zmian projektu w czasie. 

```bash
docker run eeee
```

##Praktyka
##Podsumowanie
Zachęcam każdego, aby uruchomił lokalnie SonarQube i przeskanował swoje projekty (o ile jeszcze tego nie robi). Wiedza, jaka płynie z takiej operacji jest nie do przecenienia. 