# Análise Exploratória de Dados do Spotify

## 1. Sobre o projeto

Este projeto tem como objetivo explorar dados de músicas disponíveis no Spotify e em outras plataformas de streaming, buscando identificar características associadas ao volume de reproduções (*streams*).

A proposta é utilizar técnicas de Análise Exploratória de Dados (EDA), estatística descritiva e testes estatísticos para investigar padrões de popularidade musical e responder a perguntas relevantes para o negócio.

Além da análise técnica, o projeto busca transformar os resultados em informações que possam apoiar decisões relacionadas à distribuição de músicas, presença em playlists e estratégias de divulgação no mercado musical.

## 2. Objetivos de negócio

A análise foi estruturada a partir das seguintes perguntas:

1. Músicas presentes em mais playlists do Spotify apresentam maior volume de streams?
2. A presença de uma música em diferentes plataformas de streaming está associada ao seu volume de reproduções?
3. Características das músicas, como quantidade de artistas, gênero musical e país, apresentam relação com o volume de streams?
4. O momento de lançamento da música (ano e mês) influencia o volume de streams acumulado?

## 3. Tecnologias e ferramentas

As ferramentas utilizadas no desenvolvimento do projeto incluem:

- **Python:** linguagem de programação utilizada nas análises.
- **Pandas:** manipulação e tratamento dos dados.
- **NumPy:** operações numéricas.
- **Matplotlib e Seaborn:** visualização de dados.
- **SciPy:** aplicação de testes estatísticos.
- **Scikit-posthocs:** testes estatísticos de comparações múltiplas (Dunn).
- **Databricks:** ambiente utilizado para armazenamento e exploração dos arquivos.

## 4. Etapas do projeto

### 4.1. Preparação e exploração dos dados

Inicialmente, foram carregados os arquivos CSV no ambiente Databricks, utilizando Pandas para manipulação dos dados.

As atividades de preparação incluem:

- Inspeção da estrutura dos conjuntos de dados;
- Verificação dos tipos de variáveis;
- Identificação de valores ausentes;
- Verificação de registros duplicados;
- Análise das quantidades de registros;
- Conversão de tipos de dados;
- Preparação das variáveis para as análises estatísticas.

### 4.2. Análise da relação entre playlists e streams

**Pergunta de negócio:** Músicas presentes em mais playlists do Spotify apresentam maior volume de streams?

Para investigar essa relação, foram utilizadas as correlações de Pearson e Spearman entre as variáveis `in_spotify_playlists` e `streams`.

**Resultados encontrados:**

| Métrica | Resultado |
|---|---:|
| Correlação de Pearson | 0.79 |
| Correlação de Spearman | 0.83 |

**Interpretação:**

Os resultados indicam uma forte associação positiva entre a quantidade de playlists do Spotify e o volume de streams.

Isso sugere que músicas presentes em mais playlists tendem a apresentar maiores volumes de reproduções.

A correlação de Spearman apresentou valor superior ao de Pearson, reforçando a consistência da associação na ordenação dos dados.

É importante destacar que correlação não significa causalidade. A inclusão em playlists pode contribuir para aumentar as reproduções, mas músicas que já apresentam maior popularidade também podem ter mais oportunidades de inclusão em playlists.

### 4.2. Análise da relação entre charts e streams

**Pergunta de negócio:** Músicas que entram nos charts (rankings) do Spotify têm mais streams que as que não entram?

Para investigar essa relação, foram utilizadas as correlações de Pearson e Spearman entre as variáveis - `in_apple_charts`, `in_deezer_charts`, `in_shazam_charts`,  `in_spotfy_charts`,  e `streams`.

**Resultados encontrados:**

| Métrica | Correlação de Pearson | Correlação de Spearman|
|---|---|---:|
| `in_apple_charts` | 0.32| 0.34 |
| `in_deezer_charts` |0.23| 0.25 |
| `in_shazam_charts` |0.02| 0.22 |
| `in_spotfy_charts`| 0.24|0.27|

**Interpretação:**

Na análise dos charts, as correlações são positivas, mas variam de muito fracas a fracas.  Isso sugere que músicas que entram no charts do Spotfy apresentam uma associação linear ou monotônica fraca com o streams, conforme a métrica utilizada.  

### 4.3. Análise da presença em múltiplas plataformas

**Pergunta de negócio:** A presença de uma música em diferentes plataformas de streaming está associada a um maior volume de streams no Spotify?

Foram consideradas três plataformas:

- Spotify;
- Apple Music;
- Deezer.

A análise foi realizada considerando a presença das músicas em playlists dessas plataformas e a quantidade total de plataformas nas quais cada música estava presente.

**Distribuição das músicas por quantidade de plataformas:**

| Quantidade de plataformas | Músicas |
|---|---:|
| 1 plataforma | 4 |
| 2 plataformas | 31 |
| 3 plataformas | 807 |
| **Total** | **842** |

Aproximadamente 95.84% das músicas estavam presentes nas três plataformas.

**Correlação de Spearman com os streams do Spotify:**

| Plataforma | Correlação |
|---|---:|
| Spotify | 0.8291 |
| Deezer | 0.7577 |
| Apple Music | 0.6723 |

**Interpretação:**

A quantidade de playlists nas três plataformas apresentou associação positiva com o volume de streams no Spotify, sendo a associação mais forte observada para as playlists do próprio Spotify.

Entretanto, a quantidade total de plataformas apresentou correlação muito fraca com os streams (Spearman = 0.0757).

Esse resultado pode ser explicado pela baixa variação entre os grupos, já que a grande maioria das músicas estava presente nas três plataformas.

Portanto, a simples presença em mais plataformas não foi suficiente para diferenciar o volume de streams nesta amostra.

### 4.4. Análise das características das músicas

**Pergunta de negócio:** Características como quantidade de artistas, gênero musical e país apresentam relação com o volume de streams?

Foram consideradas as seguintes variáveis:

- `artist_count`: quantidade de artistas envolvidos na música;
- `gênero_musical`: gênero musical;
- `main_country`: país principal;
- `streams`: volume de reproduções no Spotify.

Para as variáveis categóricas, foram calculadas estatísticas descritivas, incluindo quantidade de músicas, média, mediana e desvio padrão dos streams.

#### 4.4.1 Análise por número de artistas

A análise da relação entre a quantidade de artistas participantes de uma música e seu volume de streams apresentou uma correlação de Spearman de 0.13577, indicando uma associação positiva muito fraca entre as variáveis.

Embora a análise descritiva por meio do boxplot tenha indicado medianas de streams menores nos grupos com maior quantidade de artistas, a correlação observada não demonstra uma associação monotônica expressiva.

Para reduzir a influência de grupos com pouquíssimas observações, foi realizada uma análise considerando músicas com até cinco artistas. Essa decisão permite avaliar o comportamento dos grupos com maior representatividade na amostra, mas deve ser considerada uma análise complementar.

Os resultados sugerem que a quantidade de artistas, isoladamente, não apresenta uma associação relevante com o volume acumulado de streams. 

#### 4.4.2 Análise por gênero musical

Após investigar as diferenças na distribuição de streams entre os gêneros musicais, foi realizada uma análise complementar para identificar as músicas com maior volume de reproduções dentro de cada categoria.

O objetivo foi compreender se os gêneros que apresentam diferenças no comportamento dos streams também possuem músicas que se destacam individualmente, contribuindo para identificar oportunidades de curadoria musical.

Os resultados demonstraram que músicas com volumes expressivos de streams estão distribuídas entre diferentes gêneros. Entre os principais destaques estão Blinding Lights, do The Weeknd (Synth-pop), com aproximadamente 3,70 bilhões de streams; Shape of You, de Ed Sheeran (Pop), com 3,56 bilhões; Sunflower, de Post Malone e Swae Lee (Hip-hop), com 2,81 bilhões; e One Dance, de Drake, WizKid e Kyla (Afrobeats), com 2,71 bilhões.

Também foram identificadas faixas de grande alcance em gêneros como Indie pop, Indie rock, EDM, R&B, Pop rock, Reggaeton e K-pop.

A análise evidencia que o gênero musical está associado a diferenças na distribuição de streams, mas que o desempenho individual das músicas também desempenha um papel importante na identificação de sucessos. Desse modo, está descrito, a seguir, as músicas que possuem maior quantidade de streams quando analisadas do ponto de vista da mediana dos gêneros mais significativos e temos disponível também, a tabela 'Top5GenerosMusicais' com as as cinco músicas que apresentam maior quantidade de streams em seu respectivo grupo musical.


<img width="846" height="606" alt="image" src="https://github.com/user-attachments/assets/e865f9df-6940-4c7a-acdd-5ceea46e9157" />


##### Análise dos gêneros musicais mais significativos (com mais de 20 músicas) que possuem maior quantidade mediana de streams

- Pop: o bigode superior termina em ~2,55 bi, e há outliers em ~2,7, ~2,9 (dois pontos quase sobrepostos) e ~3,57 bi. Confirma a assimetria positiva: a mediana é ~0,39 bi, mas o gênero contém as músicas mais ouvidas da base. A distância entre a mediana e o topo mostra o quanto poucos hits concentram os streams. Nesse caso, o gênero musical por si só já é suficiente para gerar alta quantidade de streams. Segue as músicas com maiores quantidades de streams:

- STAY (with Justin Bieber) - Justin Bieber, The Kid Laroi Someone You Loved - Lewis Capaldi Shape of You - Ed Sheeran Circles - Post Malone Dance Monkey - Tones and I Hip-hop: tem um único outlier isolado em 2,8 bi, muito acima do bigode (1,05 bi). Esse ponto sozinho é o maior destaque do gênero e provavelmente é uma música específica de enorme sucesso. Trata-se do sucesso What It Is. Minha sugestão, nesse caso, é sempre que possível incluir essa música nas playlists. Sua presença irá aumentar a quantidade de streams.

- R&B: outliers em ~1,95, ~2,08 e ~2,56 bi. O gênero tem mais “hits” do que o primeiro gráfico sugeria. As músicas que geram mais stream são:

- Starboy - The Weeknd - Daft Punk The Hills - The Weeknd All of Me - John Legend. Minha sugestão, nesse caso, é sempre que possível incluir essas músicas nas playlists. Sua presença irá aumentar a quantidade de streams. Indie pop: apenas dois outliers (~1,8 e ~2,56 bi). É o gênero com a melhor mediana e poucos casos extremos, ou seja, o desempenho é mais sustentado, não dependente de poucos hits. As músicas que apresentam maior quantidade de streams são:

- Another Love - Tom Odell Heat Waves - Glass Animals

- Heavy metal: é o mais surpreendente. Tem a menor mediana (~0,15 bi), mas muitos outliers (cerca de 8 pontos, entre ~1,35 e ~1,95 bi). Isso sugere que a maioria das músicas tem baixo alcance, mas há um grupo de clássicos muito fortes que são:

- No Role Modelz, J. Cole. Can't Hold Us (feat. Ray Dalton) - Ray Dalton, Ryan Lewis, Macklemore Without Me - Eminem The Real Slim Shady -Eminem Lose Yourself - Soundtrack Version - Eminem Gangsta's Paradise - Coolio, L.V. INDUSTRY BABY (feat. Jack Harlow) Jack Harlow, Lil Nas X Till I Collapse Eminem, Nate Dogg HUMBLE. Kendrick Lamar

Obs: Aqui temos uma questão com relação a base de dados. As músicas:

No Role Modelz — J. Cole Can't Hold Us — Macklemore, Ryan Lewis e Ray Dalton Without Me — Eminem The Real Slim Shady — Eminem Lose Yourself — Eminem Gangsta's Paradise — Coolio e L.V. HUMBLE. — Kendrick Lamar são predominantemente associadas ao Hip-hop/Rap, não ao Heavy metal - Isso gera uma limitação da classificação. 

- Reggaeton: vários outliers agrupados entre ~1,25 e ~1,45 bi e um em ~1,75 bi. Isso indica um conjunto de músicas de sucesso, não um caso isolado. Segue as músicas com maiores streams:

- Me Porto Bonito - Chencho Corleone, Bad Bunny Danza Kuduro - Don Omar, Lucenzo Yonaguni - Bad Bunny Pepas - Farruko Dakiti - Bad Bunny, Jhay Cortez Callaita Bad Bunny, Tainy K-pop: outliers em ~0,87, ~1,07, ~1,14 e ~1,7 bi, bem acima da caixa (que termina em ~0,32 bi). Caixa estreita com vários hits distantes. Segue as músicas com maiores streams:

- Boy With Luv (feat. Halsey) - Halsey, BTS MONEY - Lisa Butter - BTS Dynamite - BTS

- Latin trap: a caixa é a mais compacta, com dois outliers (~0,54 e ~1,36 bi). É o gênero mais homogêneo. As músicas com maiores streams são:

- Quevedo: Bzrp Music Sessions, Vol. 52 - Bizarrap, Quevedo La Jumpa - Arcangel, Bad Bunny


### 4.4 Análise por país

Para comparar os streams entre países, aplicou-se o teste de Kruskal-Wallis, não paramétrico e adequado à forte assimetria da variável. Como esse teste apenas indica se existe diferença em algum ponto, utilizou-se em seguida o teste post hoc de Dunn com correção de Holm, que identifica quais pares de países diferem. O país refere-se à origem da música, e os rótulos inconsistentes (USA, MX e PR) foram unificados antes da análise. Como o Kruskal-Wallis compara distribuições, os resultados são descritos como tendência a streams maiores ou menores, e não como diferença de medianas.

A análise foi feita em três recortes.

- Todos os países (Figura 1).
Neste recorte, a mediana de streams varia de aproximadamente 0,05 a 1 bilhão, sem padrão regional evidente. Os valores mais extremos, como os da Noruega e da Irlanda, vêm de países com apenas 1 ou 2 músicas na base. Como medianas e testes baseados em amostras tão pequenas são instáveis e pouco poderosos, este recorte tem caráter apenas descritivo, e os testes estatísticos não foram aplicados a ele. Esses países foram excluídos nos recortes seguintes.

<img width="987" height="442" alt="image" src="https://github.com/user-attachments/assets/33eca80c-19da-4734-8594-ee2f7502194c" />

- Países com mais de 10 músicas (Figura 2).
O teste de Kruskal-Wallis (k = 10 países; n = 759 músicas) indicou diferença significativa na distribuição de streams (H = 65,34; p < 0,001), com tamanho de efeito médio (η² = 0,075). Isso significa que o país de origem da música está associado a cerca de 7,5% da variação nos postos de streams, e que a maior parte da variabilidade vem de outros fatores. O teste de Dunn com correção de Holm mostrou que as músicas do Reino Unido tendem a ter mais streams do que as da Coreia do Sul, Brasil, México, Argentina e Estados Unidos (esta última diferença, com p = 0,028, não se manteve no recorte seguinte). Porto Rico difere de Coreia do Sul, Brasil e México, e a Austrália difere de Brasil e Coreia do Sul. A Coreia do Sul também difere dos Estados Unidos. Os demais pares não apresentaram diferença significativa. O destaque da Austrália deve ser lido com cautela, pois ela tem apenas 14 músicas e não difere dos países de posição intermediária.

<img width="984" height="458" alt="image" src="https://github.com/user-attachments/assets/cdf50719-61fc-4345-b436-04aaca53dad7" />


- Países com mais de 5 músicas (Figura 3).
Este recorte, que inclui 15 países (n = 796 músicas), serviu como análise de sensibilidade. O teste de Kruskal-Wallis permaneceu significativo (H = 76,06; p < 0,001), com tamanho de efeito semelhante ao anterior (η² = 0,079). No teste de Dunn, mantiveram-se significativas as diferenças entre o Reino Unido e Coreia do Sul, Brasil, México e Argentina, entre Porto Rico e Coreia do Sul e Brasil, entre a Austrália e Brasil e Coreia do Sul, e entre a Coreia do Sul e os Estados Unidos. As diferenças entre Reino Unido e Estados Unidos e entre Porto Rico e México, significativas com mais de 10 músicas, deixaram de sê-lo, e devem ser interpretadas como evidência frágil. Surgiu ainda uma diferença entre Índia e Reino Unido, que merece cautela por se basear em apenas 9 músicas indianas. Conclui-se que o padrão principal é robusto ao corte de amostra mínima adotado.

<img width="975" height="446" alt="image" src="https://github.com/user-attachments/assets/a78087a5-4b6c-4e0b-a460-b9a0f3fc126f" />

O país representa a origem da música, e os streams refletem audiência global. Assim, os resultados descrevem o alcance internacional das faixas de cada país, e não o comportamento dos ouvintes locais. A possível repetição de artistas entre as músicas pode violar a suposição de independência do teste. Desse modo, a análise mostra que o país de origem de uma música influencia, em parte, o quanto ela é ouvida no Spotify. Músicas do Reino Unido, de Porto Rico e da Austrália tendem a acumular mais streams, enquanto as da Coreia do Sul e do Brasil tendem a acumular menos. Os Estados Unidos e o Canadá ficam numa posição intermediária.

Esse efeito, porém, é moderado: o país explica apenas cerca de 8% da diferença entre as músicas. Os outros 92% dependem de fatores que esta análise não mediu. Por isso, o país sozinho não deve ser usado para prever o sucesso de uma música.

O que fazer com essa informação:

Usar o país como um critério entre vários, e não como o principal, ao avaliar investimento em artistas ou lançamentos. Tratar com cautela os países com poucas músicas na base (como a Austrália, com 14 faixas): os resultados são indícios, não certezas. Não concluir que músicas brasileiras ou sul-coreanas “têm pior desempenho”. Os números medem o alcance internacional das faixas, e muitos artistas desses países têm público forte e fiel em seus mercados locais. Aprofundar a análise antes de decisões de maior valor, incluindo idioma, gênero e ano de lançamento, por exemplo com um modelo de regressão sobre o logaritmo dos streams, para separar o efeito do país do efeito desses outros fatores.


### 4.5. Análise do momento de lançamento
**Pergunta de negócio:** O momento de lançamento (ano e mês) influencia o volume de streams acumulado?

A análise temporal revelou uma associação negativa forte entre a data completa de lançamento e o volume acumulado de streams, com coeficiente de Spearman de -0.6713. Esse resultado reforça a associação inicialmente identificada entre o ano de lançamento e os streams (-0,68).

A interpretação indica que músicas lançadas há mais tempo tendem a apresentar maiores volumes acumulados de reproduções. Uma possível explicação é o maior tempo de exposição nas plataformas de streaming, permitindo que essas músicas acumulem reproduções ao longo de um período mais extenso.

Alguns anos apresentam medianas muito elevadas, enquanto outros apresentam valores consideravelmente menores.

Alguns destaques visuais:

Décadas de 1940 a 1960: as medianas aparecem relativamente baixas e próximas, em comparação com vários anos posteriores.
Década de 1970: há um pico bastante expressivo, especialmente em torno de 1975.
Décadas de 1980 a 2010: encontramos oscilações importantes, com vários anos apresentando medianas acima de 1 bilhão de streams.
Anos mais recentes: observa-se uma redução das medianas, especialmente nos últimos anos representados. O gráfico não apresenta uma queda perfeitamente contínua. Existem anos recentes com medianas elevadas e anos anteriores com medianas menores.
Isso é importante porque mostra que a relação negativa encontrada por Spearman representa uma tendência geral, e não uma regra válida para todos os anos.

Na análise por mês, a correlação de Spearman foi de -0.03, indicando ausência de uma tendência monotônica relevante.

No entanto, janeiro apresenta uma mediana próxima de 627 milhões de streams, enquanto junho apresenta aproximadamente 170 milhões.

Isso sugere que pode haver diferenças entre os meses de lançamento.

Os resultados sugerem que o ano de lançamento apresenta uma associação mais expressiva com o volume acumulado de streams do que o mês e o dia considerados isoladamente. As diferenças observadas entre os meses também merecem investigação, especialmente para verificar possíveis padrões sazonais.

## 5. Conclusões e recomendações de negócio

A análise exploratória dos dados do Spotify permitiu identificar associações entre características das músicas, presença em plataformas e playlists, informações sobre artistas, gênero musical, país de origem e momento de lançamento com o volume acumulado de streams.

Entre os principais resultados, destaca-se a forte associação positiva entre a quantidade de playlists do Spotify e os streams (Spearman = 0.83). Esse resultado indica que músicas presentes em mais playlists tendem a apresentar maior volume de reproduções. Entretanto, não é possível afirmar que a inclusão em playlists, isoladamente, causa o aumento dos streams, pois a popularidade prévia também pode favorecer a entrada das músicas nesses espaços.

A análise dos charts revelou associações positivas, porém fracas, com os streams do Spotify. Já a presença em múltiplas plataformas apresentou pouca capacidade de diferenciar o volume de reproduções nesta amostra, principalmente porque aproximadamente 96% das músicas estavam presentes nas três plataformas analisadas.

Em relação às características das músicas, a quantidade de artistas apresentou associação positiva muito fraca com os streams (Spearman = 0.13577), sugerindo que essa variável, isoladamente, não é um indicador relevante de popularidade. Por outro lado, foram identificadas diferenças estatísticas entre gêneros musicais e países de origem. A investigação das músicas com maior volume de streams em cada gênero também mostrou que grandes sucessos estão distribuídos por diferentes estilos musicais, reforçando a importância de considerar tanto o comportamento geral dos gêneros quanto o desempenho individual das faixas.

A análise por país identificou diferenças entre as distribuições de streams, com tamanho de efeito moderado, mas mostrou que a origem da música não deve ser utilizada isoladamente para avaliar seu potencial de sucesso. Fatores como gênero, idioma, artista e período de lançamento também podem estar relacionados ao desempenho.

Por fim, a análise temporal apresentou uma associação negativa forte entre a data de lançamento e os streams acumulados (Spearman = -0.6713). Esse resultado sugere que músicas lançadas há mais tempo tendem a acumular mais reproduções, possivelmente devido ao maior período de exposição nas plataformas. A análise mensal também identificou diferenças entre as distribuições dos meses, embora não tenha sido observada uma tendência monotônica relevante ao longo do calendário.

### Recomendações para o negócio

Com base nos resultados, algumas iniciativas podem ser consideradas:

- **Curadoria de playlists:** avaliar a inclusão de músicas com histórico expressivo de streams, considerando também a aderência ao público e à proposta da playlist.
- **Diversificação musical:** explorar diferentes gêneros, uma vez que músicas de grande alcance foram identificadas em estilos variados.
- **Análise de artistas e faixas:** considerar o desempenho individual das músicas, evitando decisões baseadas exclusivamente no gênero ou na quantidade de artistas.
- **Estratégia de divulgação:** avaliar a presença em playlists e charts como indicadores complementares de visibilidade, sem interpretá-los como garantia de sucesso.
- **Planejamento de lançamentos:** investigar possíveis padrões sazonais e considerar o tempo de exposição ao comparar o desempenho de músicas lançadas em períodos diferentes.

### Limitações e próximos passos

Os resultados representam associações observadas em uma amostra específica e não demonstram relações de causa e efeito. A variável `streams` representa reproduções acumuladas no Spotify, não o desempenho global em todas as plataformas.

Também foram identificadas limitações relacionadas à distribuição desigual das observações entre gêneros, países e períodos de lançamento, além de possíveis inconsistências na classificação de alguns gêneros musicais.

Como evolução do projeto, recomenda-se desenvolver modelos de regressão para investigar a contribuição conjunta das variáveis sobre os streams, utilizando transformação logarítmica da variável resposta e controlando fatores como ano de lançamento, gênero, país e presença em playlists. Também seria interessante avaliar a importância das variáveis e comparar o desempenho dos modelos.

Conclui-se que a popularidade de uma música é um fenômeno multifatorial. A presença em playlists, o gênero, o país de origem e o momento de lançamento oferecem informações relevantes, mas nenhum desses fatores, isoladamente, é suficiente para explicar o volume acumulado de streams.
