# Data assimilation med ensemble Kalman filter

## ensemble Kalman filter oppgave

I nabolandet til vår helt frå oppgåve 1 og 2 er køyrekulturen litt annleis.
Her har vi nemleg ein godt bedugga sjåfør bak rattet.
Sjåføren er i så godt slag at han kvart sekund ropar ut køyrelengda si, og som gode statistikarar har vi notert oss dette.

Data på distanse har vi i fila `drunk_belief.csv`.
Merk her at desse observasjonane er sjølvrapportering frå ein person som ikkje har sin beste augneblink, vi antek difor
at posisjonsavlesning og tilhøyrande rapportering følgjer ei Gaussisk fordeling som er unbiased med varians: `var_y = 10 * posisjon`.

1. Last inn data i `drunk_belief.csv`.

Grunna store mengder vodka har antihelt fått det føre seg at han kvart sekund skal auke farten til bilen
ved likninga `v = np.sqrt(v**2 + p**2)`.
Han også er nemleg glad i Pytagoras, sjølv om han elles er historielaus.
Dette fører dog til problem for oss: oppdatert state er svært ikkje-lineær i tidlegare states!

Difor må vi no gjere som vi elles gjer når livet er vanskeleg: Byrje å rekne og kode litt.
Det slår oss at Ensemble Kalman filteret er svaret på alle våre problem i å finne den sanne statusen til den berusa sjåføren!

2. Implementer ein funksjon `run_dynamics()` som oppdaterer avstand og hastigheit som gitt ovanfor.

3. Implementer ein variant av Ensemble Kalman Filteret
    - Note: Å nytte KalmanFilter som ein superklasse kan vere vanskeleg, men er gjort [her](https://github.com/Sonat-Consulting/kf-demo/blob/main/ensemble-kalman-filter/ensemble-kalman-filter.ipynb) for inspirasjon.
    - Det kan vere enklare å implementere ein funksjon eller berre loop som 
        1. Held/tek inn vår initielle prior (Gaussisk med mu og Sigma)
        2. Samplar ein initiell sapmle frå vår prior
        3. Iterativt tidspunkt, 
            - Estimer forventning som gjennomsnitt over sample
            - Estimer kovariansmatrise ved kovariansmatrise-estimat
            - Assimilerer datapunkt ved tid `t`
            - Oppdaterer sample som ein ny sample frå `MVNorm` med oppdatert `mu` og `Sigma`
            - Køyrer `run_dynamics()` for kvart element i sample
4. Plot prior/posterior estimat for posisjon og fart mot tid. Plot samstundes Putins datapunkt, samt den sanne state funne i `true_car_state.csv`
