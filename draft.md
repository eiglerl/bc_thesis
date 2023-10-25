# Teorie her  

Teorie her se zabývá formálním pohledem na hry a hráče modelované strategiemi. Jako hlavní průkopník je považován John von Neumann. Společně s ekonomem Oskarem Morgensternem vydali v roce 1940 knihu Theory of Games and Economic Behavior. Jedním z hlavních pilířů moderních úspěchů teorie her je věta o existenci equilibrií v hrách dvou hráčů s nulových součtem dokázaná Johnem von Neumannem.

Popsat normal-form game, utility, hra s úplnou/neúplnou informací, zero-sum? 

## Alfabeta prořezávání

## Minimax/Maximin  

## Nash Equilibrium

## ML, NN?

# AI

V roce 1997 poprvé dosáhla umělá inteligence DeepBlue II [https://www.sciencedirect.com/science/article/pii/S0004370201001291] výhry proti velmistrovi a světovému šampionovi v šachách, Garry Kasparov. O rok dříve prohrál DeepBlue I proti stejnému oponentovi. DeepBlue II byl postavený na velkém paralelismu. Každou vteřinu ohodnocoval a zkoumal miliony stavů. Oproti DeepBlue I měl také komplexnější ohodnovací funkci pro stavy hry.

V minulosti byly programy na hraní her jako jsou šachy, go či shogi, stavěné na prohledávání herního stromu, případně s pomocí alfabeta prořezávání, a chytrých heuristik. Pro ohodnocování stavu využívaly funkce připravené a promyšlené mistry a vlastnosti dané domény. 

## Player of Games

### Intro

Dělat AI obecnější. Původně AI zaměřené na jednu hru s použitím specifik z domény dané hry, AlphaZero přišlo s možností hraní několika her s plnou informací. Hlavní myšlenka algoritmu Player of Games je zobecnění i pro hry s neúplnou informací. Využívá metod self-play a prohledávání stromu hry. Při učení se snaží dostat k Nash. ekvilibriu.

### Terminologie?

### Neuronová síť

Místo ohodnocovací funkce využívá Player of Games neuronovou síť. Na vstupu síť dostane public state a beliefs, na které odpoví counterfactual hodnoty a strategie hráče na tahu pro každý private state daného hráče. Je použita feed-forward network a residual network.

### CFR

Hrát moc předvídatelně je problém - protivník může jednoduše odhadnout private state a hrát best response strategii. Při hraní worst-case optimal strategií se tomuto problému vyhneme. Counter-factual regret minimalizace (CFR) konverguje k Nash ekvilibriu - aproximace optimální strategie. CFR je self-play algoritmus. Strategie po iteraci T, získané jako průměrná dosavadní strategie, k $\epsilon$-Nash ekvilibriu konverguje rychlostí O($\sqrt{T}$).

#### Regret matching

V iteraci T ve stavu s si hráč vypočítá regret pro každou nezahranou akci a: r(s, a) = v(s, a) - suma přes akce b v(s, b)*pr(s, b), kde v(s, a) je hodnota akce a ve stavu s (counter-factual value). Přes všechny iterace t = 0, ..., T si ukládá vypočítané regrety do R(s, a). V další iteraci bude zvolená strategie ve stavu s jako: pr(s, a) = R(s, a) / suma přes akce b R(s, b), kde záporné členy jsou nahrezeny 0, případně pr uniformní strategií.

#### Regret matching+

Místo ukládání součtů regretů do R je zvolený trochu jiný přístup: $Q^t(s, a) = max(0, Q^{t-1}(s, a) + r^t(s, a))$ a $pr(s, a) = Q^t(s, a)/suma přes b Q^t(s, b)$

#### GT-CFR

Growing-tree CFR je varianta CFR, která postupně zvětšuje prohlédvaný strom. Začíná s prvotním stromem L obsahující aktuální stav a jeho potomky. V každé iteraci probíhají dva kroky:
    regret aktualizace - CFR
    fáze expanze - přidání nových vrcholů do stromu (podle simulování her), při simulování pomocí strategie se prochází strom, dokud se nenarazí na ještě nenavštívený stav, ten se přidá do stromu, počty návštěv vrcholů na cestě (trajektorii) se navýší, expanduje se k akcí (kde k je minimální velikost supportu)
Na listových vrcholech se na hodnoty hry dotazuje neuronové sítě.

### Trénování

Data pro trénování neuronové sítě se sbírají při self-play (z trajektorie i při prohledávání stromu akcí ve stavu). V trajektorii se procházené dotazy na neuronovou síť ukládají a solver je prozkoumá podrobněji, případně i rekurzivně přidá další dotazy na vyřešení. Z dotazů a jejich řešení se aktualizuje síť. Řešení dotazů je vlastně řešení "podher" - pomocí GT-CFR (díky tomu rekurzivně vytváří další dotazy - pouze s malou pravděpodobností (0.1 nebo 0.2)). Zlepšení sítě se propaguje zespod - nejdříve díky "podhrám" těsně nad listy.

### Výsledky?









https://www.fit.vut.cz/study/thesis/23706/
https://is.muni.cz/th/or4dk/Implementacia_AI_do_hry_CatchThePhantom.pdf

zajímavé články/knihy

https://books.google.cz/books?hl=cs&lr=&id=yeVbAAAAQBAJ&oi=fnd&pg=PP2&dq=game+theory&ots=Yo9-NARDii&sig=SHrWI5F2wvVG4cFgV5fYh8_H5ME&redir_esc=y#v=onepage&q=game%20theory&f=false
https://books.google.cz/books?hl=cs&lr=&id=3KnuDwAAQBAJ&oi=fnd&pg=PT11&dq=game+theory&ots=mANfC2ua1R&sig=IEeHhjijlnC3YQ5mAXtGZ64OkJs&redir_esc=y#v=onepage&q=game%20theory&f=false
https://d1wqtxts1xzle7.cloudfront.net/32188651/An_Introduction_to_Game_Theory.pdf?1383077017=&response-content-disposition=inline%3B+filename%3DAn_Introduction_to_Game_Theory.pdf&Expires=1697980632&Signature=gMrJvxUf8ROLVn33hLtTevqLUtcNUahL2gEjq97dOeJ67hLWDSvL70rggj1tom0ErjEHyloQyUG8ih~E3esWHPrfEdwJfayu1NX-yUGPHWdBGWeiUgSSeoHdeIdeBmwahEDa~kSna-7GdLTbjdF2xbH-1Xg8PIbuBbhZvP6TLXNovtDAdmrhf3-pn0dGQVJY3xDePsi3HJ-AZDP8EhLJ56WZe09YU7Fwfsetv~91JeFJ4IwScBpGajfEBC4n~lq7Wz6y6NeyV3npWDlIjjiA3fRdbS24swK1qm7Ou88tjS1KrRO26O-zm-WXb9Mh4ltWwflU84sqU9ZGTnGHig~OHg__&Key-Pair-Id=APKAJLOHF5GGSLRBV4ZA
https://books.google.cz/books?hl=cs&lr=&id=o6UlEAAAQBAJ&oi=fnd&pg=PR14&dq=game+theory&ots=HkGXHtMrhg&sig=Q-BSVHn6iHKidOUkmqGIUl8ivfI&redir_esc=y#v=onepage&q=game%20theory&f=false
https://arxiv.org/pdf/2111.05884.pdf

https://www.cs.cmu.edu/~sandholm/cs15-892F13/algorithmic-game-theory.pdf
https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=7471613


deepblue:
https://books.google.cz/books?hl=cs&lr=&id=zV0W4729UqkC&oi=fnd&pg=PR9&dq=game+theory+deep+blue&ots=yqPzO4JQja&sig=2gPCNVxqbW7qN3wISXosetzy2HE&redir_esc=y#v=onepage&q=game%20theory%20deep%20blue&f=false
https://www.sciencedirect.com/science/article/pii/S0004370201001291
https://books.google.cz/books?hl=cs&lr=&id=IiXjBwAAQBAJ&oi=fnd&pg=PA2&dq=game+theory+deep+blue&ots=_M4uTzlGIz&sig=xT5hqETpOSmhjrh0zczc__jXifM&redir_esc=y#v=onepage&q=game%20theory%20deep%20blue&f=false
https://dl.acm.org/doi/pdf/10.1145/233977.234001
https://en.chessbase.com/post/25-years-ago-deep-blue-beats-kasparov

alphago:
https://arxiv.org/abs/1812.06855
https://ieeexplore.ieee.org/abstract/document/7499782
https://dl.acm.org/doi/abs/10.1145/3206157.3206174

alphazero:
https://link.springer.com/chapter/10.1007/978-981-15-4095-0_15
https://www.pnas.org/doi/abs/10.1073/pnas.2206625119


