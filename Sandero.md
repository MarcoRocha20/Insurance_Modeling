# **Trabalho Final - Tarifação**
Author

Marco Rocha - Debora Rocha 
## **Sandero**
• Análise exploratória dos dados. • Ajuste um modelo para a frequência e severidade de sinistros em função das variáveis: sexo, idade do condutor e estado

[](#cb1-1)*# Autores: Debora Rocha e Marco Rocha* 

[](#cb1-2)*# Carregando Pacotes ------------------------------------------------------*

[](#cb1-3)library(tidyverse)

[](#cb1-4)library(readxl)

[](#cb1-5)library(fitdistrplus)

[](#cb1-6)library(MASS)

[](#cb1-7)require(pscl)

[](#cb1-8)require (hnp)

[](#cb1-9)require(boot)

[](#cb1-10)*# Lendo os dados*

[](#cb1-11)dados <- read\_excel("E:/7° Semestre 2023-01/Tarifação Seguros/Trabalho Final/Insurance\_Modeling/Dados R.xlsx")

[](#cb1-12)*# 121 observações, 15 variáveis*

[](#cb1-13)dados <- dados[-121,]

Agora é preciso agrupar os dados por Região e por tipos de sinistro.

[](#cb2-1)*# Agrupando os dados por sub\_regiões e por tipo de sinistro ---------------*

[](#cb2-2)dados$Freq\_Total <- dados$Freq\_Incencio\_Roubo + dados$Freq\_Colisao + dados$Freq\_Outras

<a name="cb2-3"></a>[](#cb2-3)

[](#cb2-4)dados$Indeni\_Total <- dados$Indeni\_Colisao + dados$Indeni\_Incencio\_Roubo + dados$Indeni\_Outras

<a name="cb2-5"></a>[](#cb2-5)

[](#cb2-6)dados$Regiao = substr(dados$Regiao, start=1, stop=2)

<a name="cb2-7"></a>[](#cb2-7)

[](#cb2-8)dados$Freq\_Media <- dados$Freq\_Total / dados$Expostos

[](#cb2-9)dados$Indeni\_Media <- dados$Indeni\_Total / dados$Expostos
## **Análise Exploratória**
### **Sexo**
[](#cb3-1)*# Análise Explortória -----------------------------------------------------*

<a name="cb3-2"></a>[](#cb3-2)

[](#cb3-3)attach(dados)

<a name="cb3-4"></a>[](#cb3-4)

[](#cb3-5)*# Distribuição das variavies de interrese* 

[](#cb3-6)ggplot(dados, aes(x=Freq\_Media)) + geom\_histogram(bins = 25, col='blue')+

[](#cb3-7)  ggtitle("Distribuição da Frequência média de sinistros")

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)

[](#cb4-1)ggplot(dados, aes(x=Indeni\_Media)) + geom\_histogram(bins = 50, col='blue')+

[](#cb4-2)   ggtitle("Distribuição da Indenização média por sinistro")

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)

[](#cb5-1)*# Distribuição das variavies de interrese por sexo* 

<a name="cb5-2"></a>[](#cb5-2)

[](#cb5-3)ggplot(dados, aes(x=Freq\_Media, color=Sexo)) + geom\_histogram()+ facet\_wrap(~Sexo)+

[](#cb5-4)  ggtitle("Frequência média de sinistros por Sexo")

`stat\_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)

[](#cb7-1)ggplot(dados, aes(x=Indeni\_Media, color=Sexo)) + geom\_histogram()+ facet\_wrap(~Sexo)+

[](#cb7-2)  ggtitle("Indenização média de sinistros por Sexo")

`stat\_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)

[](#cb9-1)ggplot(dados, aes(y=Freq\_Media, color=Sexo)) + geom\_boxplot()+ facet\_wrap(~Sexo)+

[](#cb9-2)  ggtitle("Frequência média de sinistros por Sexo")

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)

[](#cb10-1)ggplot(dados, aes(y=Indeni\_Media, color=Sexo)) + geom\_boxplot()+ facet\_wrap(~Sexo)+

[](#cb10-2)  ggtitle("Indenização média de sinistros por Sexo")

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)
### **Idade**
[](#cb11-1)ggplot(dados, aes(x=Freq\_Media)) + geom\_histogram(color='blue')+ facet\_wrap(~Idade)+

[](#cb11-2)  ggtitle("Frequência média de sinistros por Idade")

`stat\_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)

[](#cb13-1)ggplot(dados, aes(x=Indeni\_Media)) + geom\_histogram(color='blue')+ facet\_wrap(~Idade)+

[](#cb13-2)  ggtitle("Indenização média de sinistros por Idade")

`stat\_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)

[](#cb15-1)ggplot(dados, aes(y=Freq\_Media, color=Idade)) + geom\_boxplot()+ 

[](#cb15-2)  ggtitle("Frequência média de sinistros por Idade")

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)

[](#cb16-1)ggplot(dados, aes(y=Indeni\_Media, color=Idade)) + geom\_boxplot()+ 

[](#cb16-2)  ggtitle("Indenização média de sinistros por Idade")

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)

[](#cb17-1)ggplot(dados, aes(y=Freq\_Total, color=Idade)) + geom\_boxplot()+ 

[](#cb17-2)  ggtitle("Frequência total de sinistros por Idade")

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)

[](#cb18-1)ggplot(dados, aes(y=Indeni\_Total, color=Idade)) + geom\_boxplot()+ 

[](#cb18-2)  ggtitle("Indenização total de sinistros por Idade")

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)
### **Estado**
[](#cb19-1)ggplot(dados, aes(x=Freq\_Media)) + geom\_histogram(color='blue')+ facet\_wrap(~Regiao)+

[](#cb19-2)  ggtitle("Frequência média de sinistros por Região")

`stat\_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)

[](#cb21-1)ggplot(dados, aes(x=Indeni\_Media)) + geom\_histogram(color='blue')+ facet\_wrap(~Regiao)+

[](#cb21-2)  ggtitle("Indenização média de sinistros por Região")

`stat\_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)

[](#cb23-1)dados2 <- dados[dados$Indeni\_Media<3000,]

<a name="cb23-2"></a>[](#cb23-2)

[](#cb23-3)ggplot(dados2, aes(x=Indeni\_Media)) + geom\_histogram(color='blue')+ facet\_wrap(~Regiao)+

[](#cb23-4)  ggtitle("Indenização média de sinistros por Região")

`stat\_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)
### **Relação número de sinistro e valor de indenizações**
[](#cb25-1)ggplot(dados, aes(y= Indeni\_Total, x = Freq\_Total)) + geom\_point()+ 

[](#cb25-2)  ggtitle("Frequência total e indenização total")

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)

[](#cb26-1)ggplot(dados, aes(y= Indeni\_Total, x = Freq\_Total)) + geom\_smooth()+ geom\_point()+

[](#cb26-2)  ggtitle("Frequência total e indenização total")

`geom\_smooth()` using method = 'loess' and formula = 'y ~ x'

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)

[](#cb28-1)dados1 <- dados[dados$Freq\_Total<4500,]

<a name="cb28-2"></a>[](#cb28-2)

[](#cb28-3)ggplot(dados1, aes(y= Indeni\_Total, x = Freq\_Total)) + geom\_smooth()+ geom\_point()+

[](#cb28-4)  ggtitle("Frequência total e indenização total")

`geom\_smooth()` using method = 'loess' and formula = 'y ~ x'

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)
### **Total de expostos**
[](#cb30-1)*# total de expostos homens* 

<a name="cb30-2"></a>[](#cb30-2)

[](#cb30-3)ggplot(dados, aes(x = Sexo)) + geom\_bar()+ 

[](#cb30-4)  ggtitle("Expostos por sexo")

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)

Fazer uma tabela de expostos por faixa etária por estado e por sexo

[](#cb31-1)soma\_sexo\_F <- dados %>%

[](#cb31-2)  filter(Sexo == "Feminino") %>%

[](#cb31-3)  summarize(soma = sum(Expostos))

<a name="cb31-4"></a>[](#cb31-4)

<a name="cb31-5"></a>[](#cb31-5)

[](#cb31-6)soma\_sexo\_M <- dados %>%

[](#cb31-7)  filter(Sexo == "Masculino") %>%

[](#cb31-8)  summarize(soma = sum(Expostos))

<a name="cb31-9"></a>[](#cb31-9)

[](#cb31-10)valores <- c(as.numeric(soma\_sexo\_F),as.numeric(soma\_sexo\_M))

[](#cb31-11)barplot(valores)

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)

[](#cb32-1)soma\_MG <- dados %>%

[](#cb32-2)  filter(Regiao == "MG") %>%

[](#cb32-3)  summarize(soma = sum(Expostos))

<a name="cb32-4"></a>[](#cb32-4)

[](#cb32-5)soma\_ES <- dados %>%

[](#cb32-6)  filter(Regiao == "ES") %>%

[](#cb32-7)  summarize(soma = sum(Expostos))

<a name="cb32-8"></a>[](#cb32-8)

[](#cb32-9)soma\_RJ <- dados %>%

[](#cb32-10)  filter(Regiao == "RJ") %>%

[](#cb32-11)  summarize(soma = sum(Expostos))

<a name="cb32-12"></a>[](#cb32-12)

<a name="cb32-13"></a>[](#cb32-13)

[](#cb32-14)soma\_SP <- dados %>%

[](#cb32-15)  filter(Regiao == "SP") %>%

[](#cb32-16)  summarize(soma = sum(Expostos))

<a name="cb32-17"></a>[](#cb32-17)

<a name="cb32-18"></a>[](#cb32-18)

[](#cb32-19)soma\_18\_25 <- dados %>%

[](#cb32-20)  filter(Idade == "Entre 18 e 25 anos") %>%

[](#cb32-21)  summarize(soma = sum(Expostos))

<a name="cb32-22"></a>[](#cb32-22)

[](#cb32-23)soma\_26\_35 <- dados %>%

[](#cb32-24)  filter(Idade == "Entre 26 e 35 anos") %>%

[](#cb32-25)  summarize(soma = sum(Expostos))

<a name="cb32-26"></a>[](#cb32-26)

<a name="cb32-27"></a>[](#cb32-27)

[](#cb32-28)soma\_36\_45 <- dados %>%

[](#cb32-29)  filter(Idade == "Entre 36 e 45 anos") %>%

[](#cb32-30)  summarize(soma = sum(Expostos))

<a name="cb32-31"></a>[](#cb32-31)

<a name="cb32-32"></a>[](#cb32-32)

[](#cb32-33)soma\_46\_55 <- dados %>%

[](#cb32-34)  filter(Idade == "Entre 46 e 55 anos") %>%

[](#cb32-35)  summarize(soma = sum(Expostos))

<a name="cb32-36"></a>[](#cb32-36)

[](#cb32-37)soma\_55\_mais <- dados %>%

[](#cb32-38)  filter(Idade == "Maior que 55 anos") %>%

[](#cb32-39)  summarize(soma = sum(Expostos))

<a name="cb32-40"></a>[](#cb32-40)

[](#cb32-41)expostos\_idade <- cbind("Entre 18 e 25 anos" = soma\_18\_25,

[](#cb32-42)                        "Entre 26 e 35 anos" = soma\_26\_35,

[](#cb32-43)                        "Entre 36 e 45 anos" = soma\_36\_45,

[](#cb32-44)                        "Entre 46 e 55 anos" = soma\_46\_55,

[](#cb32-45)                        "Maior que 55 anos" = soma\_55\_mais)
## **Modelando a Distribuição da Indenização**
[](#cb33-1)*## estimador máxima verossimilhança*

[](#cb33-2)fgamEMV = fitdist(dados$Indeni\_Media, "gamma", method="mle")

[](#cb33-3)fgamEMV

Fitting of the distribution ' gamma ' by maximum likelihood 

Parameters:

`         `estimate   Std. Error

shape 3.961055213 0.4122702683

rate  0.004983358 0.0005295789

[](#cb35-1)plot(fgamEMV)

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)

[](#cb36-1)fpoisEMV = fitdist(round(dados$Indeni\_Media), "pois", method="mle")

[](#cb36-2)fpoisEMV

Fitting of the distribution ' pois ' by maximum likelihood 

Parameters:

`       `estimate Std. Error

lambda    794.9   2.573745

[](#cb38-1)plot(fpoisEMV)

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)

[](#cb39-1)fnbinomEMV= fitdist(round(dados$Indeni\_Media), "nbinom", method="mle")

[](#cb39-2)fnbinomEMV

Fitting of the distribution ' nbinom ' by maximum likelihood 

Parameters:

`       `estimate Std. Error

size   3.985998    0.49730

mu   794.974610   36.44329

[](#cb41-1)plot(fnbinomEMV)

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)
## **Modelando a distribuição da Frequência**
[](#cb42-1)*## estimador máxima verossimilhança*

[](#cb42-2)fgamEMV = fitdist(dados$Freq\_Media, "gamma", method="mle")

[](#cb42-3)fgamEMV

Fitting of the distribution ' gamma ' by maximum likelihood 

Parameters:

`       `estimate Std. Error

shape  8.202499   1.038115

rate  21.539838   2.811225

[](#cb44-1)plot(fgamEMV)

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)

[](#cb45-1)fpoisEMV = fitdist((dados$Freq\_Total), "pois", method="mle")

[](#cb45-2)fpoisEMV

Fitting of the distribution ' pois ' by maximum likelihood 

Parameters:

`       `estimate Std. Error

lambda 511.4583   2.064502

[](#cb47-1)plot(fpoisEMV)

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)

[](#cb48-1)fnbinomEMV= fitdist((dados$Freq\_Total), "nbinom", method="mle")

[](#cb48-2)fnbinomEMV

Fitting of the distribution ' nbinom ' by maximum likelihood 

Parameters:

`        `estimate  Std. Error

size   0.5634169  0.06110501

mu   511.3822643 62.21811575

[](#cb50-1)plot(fnbinomEMV)

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)
## **Modelos MLG**
[](#cb51-1)modelSg = glm(dados$Indeni\_Media ~ dados$Regiao + dados$Sexo + dados$Idade, family= Gamma)

[](#cb51-2)summary(modelSg)

Call:

glm(formula = dados$Indeni\_Media ~ dados$Regiao + dados$Sexo + 

`    `dados$Idade, family = Gamma)

Coefficients:

`                                `Estimate Std. Error t value Pr(>|t|)    

(Intercept)                    9.290e-04  1.663e-04   5.588 1.66e-07 \*\*\*

dados$RegiaoMG                 9.366e-05  1.600e-04   0.585  0.55943    

dados$RegiaoRJ                 3.853e-05  1.740e-04   0.221  0.82515    

dados$RegiaoSP                 3.360e-04  1.644e-04   2.044  0.04332 \*  

dados$SexoMasculino           -3.274e-04  9.898e-05  -3.308  0.00127 \*\* 

dados$IdadeEntre 26 e 35 anos  2.238e-04  1.242e-04   1.802  0.07428 .  

dados$IdadeEntre 36 e 45 anos  3.963e-04  1.372e-04   2.889  0.00465 \*\* 

dados$IdadeEntre 46 e 55 anos  6.285e-04  1.553e-04   4.046 9.64e-05 \*\*\*

dados$IdadeMaior que 55 anos   8.938e-04  1.766e-04   5.060 1.67e-06 \*\*\*

\---

Signif. codes:  0 '\*\*\*' 0.001 '\*\*' 0.01 '\*' 0.05 '.' 0.1 ' ' 1

(Dispersion parameter for Gamma family taken to be 0.1868491)

`    `Null deviance: 31.532  on 119  degrees of freedom

Residual deviance: 20.657  on 111  degrees of freedom

AIC: 1724.1

Number of Fisher Scoring iterations: 6

[](#cb53-1)plot(hnp(modelSg, sim=100, type.resid="deviance", how.many.out=TRUE, paint.out=TRUE),main="Resíduos Severidade de Sinistros Observados \n vs. \n Distribuição Gama com Função Log")

Gamma model 

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)

Total points: 120 

Points out of envelope: 80 ( 66.67 %) 

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)

Total points: 120 

Points out of envelope: 80 ( 66.67 %) 

[](#cb57-1)modelSgi = glm(dados$Indeni\_Media ~ dados$Regiao + dados$Sexo + dados$Idade, family= Gamma(link = identity))

[](#cb57-2)summary(modelSgi)

Call:

glm(formula = dados$Indeni\_Media ~ dados$Regiao + dados$Sexo + 

`    `dados$Idade, family = Gamma(link = identity))

Coefficients:

`                              `Estimate Std. Error t value Pr(>|t|)    

(Intercept)                    1030.27     145.05   7.103 1.24e-10 \*\*\*

dados$RegiaoMG                   38.40     119.37   0.322 0.748282    

dados$RegiaoRJ                   85.36     134.95   0.633 0.528348    

dados$RegiaoSP                 -102.21     112.80  -0.906 0.366864    

dados$SexoMasculino             169.04      60.25   2.805 0.005935 \*\* 

dados$IdadeEntre 26 e 35 anos  -220.51     128.57  -1.715 0.089132 .  

dados$IdadeEntre 36 e 45 anos  -324.26     122.65  -2.644 0.009387 \*\* 

dados$IdadeEntre 46 e 55 anos  -450.88     116.14  -3.882 0.000176 \*\*\*

dados$IdadeMaior que 55 anos   -539.66     112.14  -4.812 4.74e-06 \*\*\*

\---

Signif. codes:  0 '\*\*\*' 0.001 '\*\*' 0.01 '\*' 0.05 '.' 0.1 ' ' 1

(Dispersion parameter for Gamma family taken to be 0.2085772)

`    `Null deviance: 31.532  on 119  degrees of freedom

Residual deviance: 21.053  on 111  degrees of freedom

AIC: 1726.4

Number of Fisher Scoring iterations: 11

[](#cb59-1)plot(hnp(modelSgi, sim=100, type.resid="deviance", how.many.out=TRUE, paint.out=TRUE),main="Resíduos Severidade de Sinistros Observados \n vs. \n Distribuição Gama com Função Identidade")

Gamma model 

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)

Total points: 120 

Points out of envelope: 77 ( 64.17 %) 

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)

Total points: 120 

Points out of envelope: 77 ( 64.17 %) 

[](#cb63-1)modelLN = glm(log(dados$Indeni\_Media) ~ dados$Regiao + dados$Sexo + dados$Idade, family= gaussian(link=log))

[](#cb63-2)summary(modelLN)

Call:

glm(formula = log(dados$Indeni\_Media) ~ dados$Regiao + dados$Sexo + 

`    `dados$Idade, family = gaussian(link = log))

Coefficients:

`                               `Estimate Std. Error t value Pr(>|t|)    

(Intercept)                    1.888511   0.025612  73.735  < 2e-16 \*\*\*

dados$RegiaoMG                -0.009231   0.024173  -0.382 0.703297    

dados$RegiaoRJ                 0.024207   0.026222   0.923 0.357924    

dados$RegiaoSP                -0.016688   0.023707  -0.704 0.482950    

dados$SexoMasculino            0.042965   0.012543   3.425 0.000862 \*\*\*

dados$IdadeEntre 26 e 35 anos  0.003221   0.019295   0.167 0.867708    

dados$IdadeEntre 36 e 45 anos -0.014881   0.019471  -0.764 0.446354    

dados$IdadeEntre 46 e 55 anos -0.048153   0.019808  -2.431 0.016661 \*  

dados$IdadeMaior que 55 anos  -0.068974   0.020028  -3.444 0.000810 \*\*\*

\---

Signif. codes:  0 '\*\*\*' 0.001 '\*\*' 0.01 '\*' 0.05 '.' 0.1 ' ' 1

(Dispersion parameter for gaussian family taken to be 0.2022275)

`    `Null deviance: 29.955  on 119  degrees of freedom

Residual deviance: 22.447  on 111  degrees of freedom

AIC: 159.39

Number of Fisher Scoring iterations: 5

[](#cb65-1)plot(hnp(modelLN, sim=100, type.resid="deviance", how.many.out=TRUE, paint.out=TRUE),main="Resíduos Severidade de Sinistros Observados \n vs. \n Distribuição LogNormal")

Gaussian model (glm object) 

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)

Total points: 120 

Points out of envelope: 96 ( 80 %) 

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)

Total points: 120 

Points out of envelope: 96 ( 80 %) 

[](#cb69-1)*# Gráficos de Diagnósticos para GLM, do pacote "boot"*

<a name="cb69-2"></a>[](#cb69-2)

[](#cb69-3)glm.diag.plots(modelSg, glmdiag = glm.diag(modelSg), subset = NULL,iden = FALSE, labels = NULL, ret = FALSE) *#"Diagnósticos para o Modelo de Severidade de Sinistros \n utilizando a Distribuição Gama"*

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)

[](#cb70-1)glm.diag.plots(modelSgi, glmdiag = glm.diag(modelSgi), subset = NULL,iden = FALSE, labels = NULL, ret = FALSE) *#"Diagnósticos para o Modelo de Severidade de Sinistros \n utilizando a Distribuição Gama"*

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)

[](#cb71-1)glm.diag.plots(modelLN, glmdiag = glm.diag(modelLN), subset = NULL,iden = FALSE, labels = NULL, ret = FALSE) *#"Diagnósticos para o Modelo de Severidade de Sinistros \n utilizando a Distribuição Gama"*

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)

[](#cb72-1)modelbinneg = glm.nb(dados$Indeni\_Media ~ dados$Regiao + dados$Sexo + dados$Idade)

<a name="cb72-2"></a>[](#cb72-2)

[](#cb72-3)dados$Severidade <- dados$Indeni\_Total / dados$Freq\_Total

<a name="cb72-4"></a>[](#cb72-4)

[](#cb72-5)modelbinneg = glm.nb(dados$Severidade ~ dados$Regiao + dados$Sexo + dados$Idade)

<a name="cb72-6"></a>[](#cb72-6)

<a name="cb72-7"></a>[](#cb72-7)

[](#cb72-8)summary(modelbinneg)

Call:

glm.nb(formula = dados$Severidade ~ dados$Regiao + dados$Sexo + 

`    `dados$Idade, init.theta = 5.075790123, link = log)

Coefficients:

`                               `Estimate Std. Error z value Pr(>|z|)    

(Intercept)                    8.234665   0.167230  49.241  < 2e-16 \*\*\*

dados$RegiaoMG                 0.198364   0.157094   1.263 0.206695    

dados$RegiaoRJ                -0.003475   0.172095  -0.020 0.983889    

dados$RegiaoSP                -0.471975   0.153943  -3.066 0.002170 \*\* 

dados$SexoMasculino            0.301962   0.081143   3.721 0.000198 \*\*\*

dados$IdadeEntre 26 e 35 anos -0.516153   0.128252  -4.025 5.71e-05 \*\*\*

dados$IdadeEntre 36 e 45 anos -0.669781   0.128264  -5.222 1.77e-07 \*\*\*

dados$IdadeEntre 46 e 55 anos -0.743495   0.128271  -5.796 6.78e-09 \*\*\*

dados$IdadeMaior que 55 anos  -0.961627   0.128294  -7.496 6.60e-14 \*\*\*

\---

Signif. codes:  0 '\*\*\*' 0.001 '\*\*' 0.01 '\*' 0.05 '.' 0.1 ' ' 1

(Dispersion parameter for Negative Binomial(5.0758) family taken to be 1)

`    `Null deviance: 256.16  on 119  degrees of freedom

Residual deviance: 123.83  on 111  degrees of freedom

AIC: 1991.6

Number of Fisher Scoring iterations: 1

`              `Theta:  5.076 

`          `Std. Err.:  0.636 

` `2 x log-likelihood:  -1971.608 

[](#cb74-1)plot(hnp(modelbinneg, sim=100, type.resid="deviance", how.many.out=TRUE, paint.out=TRUE),main="Resíduos Severidade de Sinistros Observados \n vs. \n Distribuição Binomial Negativa")

Negative binomial model (using MASS package) 

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)

Total points: 120 

Points out of envelope: 88 ( 73.33 %) 

![](Aspose.Words.5955c65b-cb01-4055-bef6-19207a7012d7.001.png)

Total points: 120 

Points out of envelope: 88 ( 73.33 %) 
