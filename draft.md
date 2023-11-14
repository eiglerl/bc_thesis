# Teorie her  

Teorie her se zabývá formálním pohledem na hry a hráče modelované strategiemi. Jako hlavní průkopník je považován John von Neumann. Společně s ekonomem Oskarem Morgensternem vydali v roce 1940 knihu Theory of Games and Economic Behavior. Jedním z hlavních pilířů moderních úspěchů teorie her je věta o existenci equilibrií v hrách dvou hráčů s nulových součtem dokázaná Johnem von Neumannem. Rozepisovat víc?

Popsat normal-form game, utility, hra s úplnou/neúplnou informací, zero-sum? 

## Terminologie (většina terminologie ze skript https://kam.mff.cuni.cz/~balko/ath2324/main.pdf)

Hra v normální formě je trojice $(P, A, u)$, kde 
* $P$ je konečná množina $n$ hráčů,
* $A_i$ je množina akcí hráče $i \in P$,
* $A = A_1 \times ... \times A_n$ je profil akcí,
* $u_i: A_i \to \mathbb{R}$ je funkce odměn (utility/payoff function) pro hráče $i \in P$,
* $u = (u_i, ..., u_n)$.

Strategie hráče $i$ je $s_i$, takové že hráč $i$ zahraje akci $a \in A_i$ s pravděpodobností $s_i(a)$, množina všech strategií hráče $i$ je $S_i$.
Čistá stragie je strategie, kde hráč $i \in P$ vybere akci $a \in A_i$ s pravděpodobností 1, neboli $s_i(b) = 1$ pro $a=b$, jinak $0$.
Smíšená strategie je strategie, kde $s_i$ je pravděpodobnostní distribuce hráče $i$ přes akce z $A_i$.  

Profil strategií všech hráčů je $s = (s_1, ..., s_n)$, pak značíme $s_{-i}$ profil strategií všech hráčů kromě $i$-tého.

## Zero-sum 

Hra s nulovým součtem je hra dvou hráčů, kde pro každou dvojici akcí $a=(a_1, a_2) \in (A_1, A_2)$ platí $u_1(a) = u_2(a)$. Neboli zisk jednoho hráče je ztráta druhého.  

## Best response

Nejlepší odpověď hráče $i$ na profil strategií $s_{-i}$ je smíšená strategie $s_{i}^{*}$ taková, že $\forall s_{i}' \in S_{i}: u_i(s_{i}^{*}, s_{-i}) \geq u_i(s_{i}', s_{-i})$.

## Nash Equilibrium

Pro hru v normálním tvaru $G = (P, A, u)$ $n$ hráčů, Nashovo equilibrium v $G$ je profil strategií $s$ takový, že $\forall i \in P: s_i$ je nejlepší odpověd na $s_{-i}$. Slovně řečeno, žádný racionální hráč (sám o sobě) nechce změnit strategii - ve smyslu, že si jinou strategií nemůže pomoct, pokud ostatní budou stále hrát tu svojí. Podle Nashovo věty má každá hra v normální formě Nashovo equilibrium.  

## Minimax/Maximin

### Minimax

Definice minimaxu je: $\overline{u_i} = min_{s_{-i}}max_{s_{i}} u_i(s_i, s_{-i})$. Vlastně říká, minimální hodnotu, kterou můžou protihráči hráče $i$ donutit dostat, když neznají jeho strategii.

### Maximin

Definice maximinu: $\underline{u_i} = max_{s_{i}}min_{s_{-i}}u_i(s_i, s_{-i})$. Oproti tomu maximin říká maximální hodnotu zisku, kterou hráč $i$ může zaručit, pokud nezná strategie ostatních hráčů.

Jedna z nejdůležitějších vět teorie her. Pro každou hru s nulovým součtem platí: 

$max_{s_{i}}min_{s_{-i}}u_i(s_i, s_{-i}) = min_{s_{-i}}max_{s_{i}} u_i(s_i, s_{-i})$

Tato věta v nějakém smyslu vlastně řeší hry s nulovým součtem. Vychází z ní také, že Nashova equilibria v hrách s nulovým součtem se dají dobře počítat. Také existuje hodnota $v = max_{s_{i}}min_{s_{-i}}u_i(s_i, s_{-i})$, tzv. hodnota hry $G$.


## Alfabeta prořezávání

Hry s nulovým součtem se dají například reprezentovat stromem hry (game tree). Hráči se střídají po vrstvách stromu. Každý vrchol má tolik potomků, kolik daný hráč má akcí. Listy jsou ohodnocené ziskem pro daného hráče (zero-sum => ztráta pro druhého hráče). Pro vyhodnocení je potřeba projít každý vrchol ve stromě a rozhodnout se pro daného hráče, jaká akce bude nejlepší. Jelikož jde o hru s nulovým součtem, jeden hráč minimalizuje a druhý maximalizuje. Pomocí alfa-beta prořezávání se některé podstromy dají vynechat, když nemůžou vrátit lepší výsledek než jiný podstrom. 

Potřeba lépe pochopit a vysvětlit.

Hlavně obrázek.

## ML, NN?

Strojové učení je podoblast umělé inteligence. Zaměřuje se na algoritmy a techniky "učení" - ve smyslu vylepšování schopnosti predikování/uzpůsobování se prostředí.  

# AI

V roce 1997 poprvé dosáhla umělá inteligence DeepBlue II [https://www.sciencedirect.com/science/article/pii/S0004370201001291] výhry proti velmistrovi a světovému šampionovi v šachách, Garry Kasparov. O rok dříve prohrál DeepBlue I proti stejnému oponentovi. DeepBlue II byl postavený na velkém paralelismu. Každou vteřinu ohodnocoval a zkoumal miliony stavů. Oproti DeepBlue I měl také komplexnější ohodnovací funkci pro stavy hry.

V minulosti byly programy na hraní her jako jsou šachy, go či shogi, stavěné na prohledávání herního stromu, případně s pomocí alfabeta prořezávání, a chytrých heuristik. Pro ohodnocování stavu využívaly funkce připravené a promyšlené mistry a vlastnosti dané domény. 

## Bakalářka 

### FIT Michal Sova

Do řešení podobného problému - umělé inteligence ve hře Scotland Yard, se pouštěl i (Bc.?) Michal Sova ve své bakalářské práci [https://www.fit.vut.cz/study/thesis/23706/]. Využíval metod strojového učení.  

Pro testování navrhl zjednodušenou verzi hry. Úprava hry spočívala v omezení počtu deketivů z původních pěti na pouze dva. Jelikož by Mr.X byl poté ve velké výhodě, zmenšila se mapa na mřížku 5x5 (kde každý vrchol je propojen se všemi sousedy). Z dopravdních prostředků zůstal pouze jeden a Mr. X přichází o své speciální tahy. Délka hry je zkrácená na 15 tahů z 22. Mr. X se ukáže jednou za tři kola, původně byl viděl přibližně jednou za pět kol.  

Na navržené verzi hry byly porovnány dva různé postupy pro umělou inteligenci ve hře - Alfa-beta prořezávání a Monte Carlo tree search. Výsledky ukázaly, že procento výher u algoritmu Monte Carlo je nižší než u algoritmu Alfa-beta. Rozšíření hry pro algoritmus Alfa-beta nebylo úspěšné kvůli nedostatku vlastních zdrojů.  

### MUNI Matej Rišnovský

Ve své bakalářské práci [https://is.muni.cz/th/or4dk/Implementacia_AI_do_hry_CatchThePhantom.pdf] (Bc.?) Matej Rišnovský implementoval hru Scotland Yard ve vývojovém prostředí Unity a zkoumal problémy návrhu umělé inteligence z diplomové práce Mária Kudolániho [https://is.muni.cz/th/duubn/final.pdf]. 

Za cíl měla práce vytvořit racionální umělou inteligenci, která bude hrát proti hráči, případně s ním. Do hry byly implementované 3 obtížnosti, které do rozhodování s nižší obtížností zavádělí vyšší chybovost.


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

Growing-tree CFR je varianta CFR, která postupně zvětšuje prohlédvaný strom. Začíná s prvotním stromem L obsahující aktuální stav a jeho potomky.  
V každé iteraci probíhají dva kroky:  

* regret aktualizace - CFR
* fáze expanze - přidání nových vrcholů do stromu (podle simulování her), při simulování  pomocí strategie se prochází strom, dokud se nenarazí na ještě nenavštívený stav, ten se  přidá do stromu, počty návštěv vrcholů na cestě (trajektorii) se navýší, expanduje se k akcí (kde k je minimální velikost supportu)  

Na listových vrcholech se na hodnoty hry dotazuje neuronové sítě.

### Trénování

Data pro trénování neuronové sítě se sbírají při self-play (z trajektorie i při prohledávání stromu akcí ve stavu). V trajektorii se procházené dotazy na neuronovou síť ukládají a solver je prozkoumá podrobněji, případně i rekurzivně přidá další dotazy na vyřešení. Z dotazů a jejich řešení se aktualizuje síť. Řešení dotazů je vlastně řešení "podher" - pomocí GT-CFR (díky tomu rekurzivně vytváří další dotazy - pouze s malou pravděpodobností 0.1 nebo 0.2). Zlepšení sítě se propaguje zespod - nejdříve díky "podhrám" těsně nad listy.

### Výsledky?

# Fantom staré Prahy

## Pravidla

## Informace kolem? (vznik, existují AI)

# Moje hra (jak moc popisovat?)

## Unity a C#

Svou implementaci hry "Fantom staré Prahy" (upravená verze hry "Scotland Yard) jsem vyvíjel v herním engine Unity. Zdrojové kódy jsou napsané ve staticky typovaném programovacím jazyce C#.  Před spuštěním hry je možné zvolit, zda za Fantoma, respektive detektivy, bude hrát předpřipravné AI či člověk. Přidání AI je snadné - stačí do složky se skripty přidal C# skript obsahující třídu implementující správný interface (viz AIBase.cs). Hra je implementovaná s využitím paralelního zpracování (UI vlákno + pomocné). 

## Grafické rozhraní (fotky, popis?)?

## Generování mapy

# Praktičtější zaměření bakalářky

Zkoumání map, lepší generování?
AI?
Program pro simulování?





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


alphago:
https://arxiv.org/abs/1812.06855
https://ieeexplore.ieee.org/abstract/document/7499782
https://dl.acm.org/doi/abs/10.1145/3206157.3206174

alphazero:
https://link.springer.com/chapter/10.1007/978-981-15-4095-0_15
https://www.pnas.org/doi/abs/10.1073/pnas.2206625119


