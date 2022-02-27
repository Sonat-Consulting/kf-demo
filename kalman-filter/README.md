# Data assimilation med Kalman filter


## Kalman filter oppgave

Eit sindig menneske køyrer bil. 
Mennesket køyrer vekk frå fly og fulle menn i nabolandet. 
I slike tider kan ein ikkje vere varsam nok, og mannen held difor konstant hastigheit heile tida, samt køyrer i ei rett linje vekk frå uro og galskap.

1. Gitt all denne sindige køyringa: Set opp dynamikken, altså korleis endringa er frå tid `t-1` til tid `t` for bilen (state er `(posisjon, hastigheit)`).

Vi er interesserte i å vite posisjonen (gitt som distanse frå uro og galskap) samt hastigheiten til bilen ved alle tidspunkt.
Vi har nokre antagelsar med status ved tid 0, nemleg
```
posisjon = 3 (meter)
hastigheit = 4 (m/s)
```
Antagelsane er usikre, og difor legg vi uvisse rundt våre sentrale estimat, ved å nytte ei kovariansmatrise:
```
[50,0],
[0,50]
```
Vi er altså _ganske_ uvitande.
Heldigvis så vil mannen hjelpe oss. Han har ein halveges god GPS/distansemålar i bilen, som tillet han å rope ut eksakt kva den seier kvart einaste sekund.

2. Les inn avlest posisjonsdata i `observed_car_position.csv` til ditt favorittprogram

Diverre så blir distansemålaren forstyrra av framande makter, og må antakast å ha litt uvisse.
Vi legg difor ei Gaussisk fordeling på desse målingane. Vi antek at feilen i målingane er Gaussisk med
```
mean = 0
Sigma_y = 50
```

3. Set opp eit container objekt-struktur (og kall det for "KalmanFilter") som held matrisen `M` funne i punkt 1, samt forventning (vektor) og kovarians (square matrise) til ein prior, og variansen til avstandsmålingane `Sigma_y`.

4. Ved å nytte dynamikkane funne i 1, samt vyrde kunnskapar om Kalman-filteret (likning 1 og 2 i KF likningssettet) kan vi skrive ein `predict()` funksjon som oppdaterer vår prior frå tid `t-1` til tid `t`.

5. Ved å nytte dei resterande Kalman-filter likningane, skriv in `update()` funksjon som kan assimilere informasjonen som den sindige mannen skrik ut ved tid `t` (data skal vere lese inn etter punkt 2), gitt at all tidlegare informasjon er assimilert.

6. Iterer over datapunkta som er lest inn i steg 2, og iterativt kall `update()` og `predict()` funksjonane for å assimilere data samt bringe fordelingane framover i tid.

7. Mot tid på x-aksen, plot prior ved tid `t`, posterior ved tid `t`, avlest datapunkt ved tid `t`, samt den sanne state til bilen ved tid `t` (kan finnast i filen `true_car_position.csv`)

Dersom noko er uklart, skrik ut, eller sjå på [fasit](https://github.com/Sonat-Consulting/kf-demo/blob/main/kalman-filter/kalman-filter.ipynb)
