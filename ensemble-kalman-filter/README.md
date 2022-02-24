# Data assimilation med ensemble Kalman filter

## ensemble Kalman filter oppgave

I nabolandet til vår helt er orsaka til flukten i oppgave 1 og fly-observasjonane i oppgave 2: Putin.
Putin er openbart veldig full, og difor uberegneleg og irrasjonell.
I tillegg køyrer han bil, og ropar ut sin distanse frå fengsel og rettmessig straff kvart einaste sekund.
Data på dette har vi i fila `drunk_belief.csv`.

1. Last inn data i `drunk_belief.csv`.

Grunna store mengder vodka har vår vesle krigshissar fått det føre seg at han kvart sekund skal auke farten til bilen
ved likninga `v = np.sqrt(v**2 + p**2)`.
Han også er nemleg glad i Pytagoras, sjølv om han elles er historielaus.
Dette fører dog til problem for vår helt: oppdatert state er svært ikkje-lineær i tidlegare states!

Vår helt gjer som han normalt gjer når noko er vanskeleg: Han tenkjer og byrjar rekne og kode litt.
Det slår han at Ensemble Kalman filteret er svaret på alle hans problem!

2. Implementer `run_dynamics` som oppdaterer avstand og hastigheit som gitt ovanfor.

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
    - Putin er ikkje ved sine fulle fem, og anta difor hans posisjonsavlesning følgjer ei Gaussisk fordeling som er unbiased med varians: `var_y = 10 * posisjon`
4. Plot prior/posterior estimat for posisjon og fart mot tid. Plot samstundes Putins datapunkt, samt den sanne state funne i `true_car_state.csv`

