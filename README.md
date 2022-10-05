---
title: "**Semana da Conscientização sobre sono**"
author: 
    - name: "**Sistema de Gestão da Qualidade. NGD. Núcleo de Gestão de Documentos**"
abstract: "**Como a qualidade do sono influencia em nossas atividades cotidianas**"
date: "Última atualização em `r format(Sys.time(), '%d / %m / %Y às %H:%M horas.')`"    
output: 
    learnr::tutorial:
         fig_caption: yes
         progressive: true
         allow_skip: true
runtime: shiny_prerendered
editor_options: 
  chunk_output_type: inline
---

[![SGQ - NGD](https://www.google.com/url?sa=i&url=https%3A%2F%2Fpneumosono.com.br%2Fblog%2F59-problemas-que-a-falta-de-sono-provoca-a-saude&psig=AOvVaw2QsvUtZpDoIH5ICi12kr72&ust=1665060508894000&source=images&cd=vfe&ved=0CAkQjRxqFwoTCPits4eQyfoCFQAAAAAdAAAAABAJ){.illustration style="top: 10px; right: 20px; position: absolute" width="130"}](https://youtu.be/8K9WvvPmfd0)

```{r setup, include=FALSE}

#install.packages("learnr")
library(learnr)
#install.packages("sortable")
library(sortable)


knitr::opts_chunk$set(echo = FALSE)

```

```{r pacotes, include=FALSE}
pacotes <- c("datasets",
             "forecast",
             "fpp2",
             "tseries",
             "patchwork", 
             "DataCombine", 
             "TTR",  
             "magrittr", 
             "rio", 
             "tidyverse", 
             "googlesheets4", 
             "googledrive",
             "lubridate",
             "pagedown",
             "rticles",
             "bookdown",
             "xaringan",
             "xaringanthemer",
             "thematic",
             "flexdashboard",
             "quarto",
             "bslib",
             "DT",
             "plotly",
             "DiagrammeR",
             "uuid", 
             "qrcode",
             "knitr",
             "tinytex",
             "usethis",
             "extrafont",
             "patchwork",
             "gganimate",
             "fable",
             "tsibble",
             "tsibbledata")
             
if(sum(as.numeric(!pacotes %in% installed.packages())) != 0){
  instalador <- pacotes[!pacotes %in% installed.packages()]
  for(i in 1:length(instalador)) {
    install.packages(instalador, dependencies = T)
    break()}
  sapply(pacotes, require, character = T) 
} else {
  sapply(pacotes, require, character = T) 
}
```

------------------------------------------------------------------------

|                                                                                                                                                                                          |
|------------------------------------------------------------------------|
| \ [*Se você desprezar seu sono, estará destruindo o reator da vida.*]{style="color:green"}                                                                                           |
| \ [Augusto Cury](https://m.facebook.com/usebebrasil/videos/o-que-a-qualidade-do-sono-pode-dizer-sobre-a-nossa-sa%C3%BAde-emocionalnesse-v%C3%ADdeo-o-/428668692122456/) 

------------------------------------------------------------------------



------------------------------------------------------------------------

## Saiba mais sobre como ter um sono reparador 

### [SONO](https://www.youtube.com/watch?v=zJGgrC4BDHE)

A quantidade e qualidade de sono diária influencia diretamente na sua saúde física, mental, intelectual, e emocional.

Mas então, quanto tempo diário de sono é preciso para ficarmos realmente bem?

```{=html}
<style>
div.blue1 { background-color:#e6f0ff; border-radius: 5px; padding: 20px;text-align: left;}
</style>
```
::: {.blue1 style="text-align: text-align: left"}


A necessidade básica de sono é individual, mas em média cada pessoa precisa dormir em torno de **oito horas** por dia.
Então podemos entender que quanto menos tempo dedicamos ao sono, mais prejuízos à saúde irão ocorrer.

- Você sabia que poucas horas de sono por dia podem causar redução da concentração, raciocínio, e poder de decisão?

- Distúrbios de humor podem ser frequentes como raiva, depressão e ansiedade, e você pode perceber-se mais nervoso, irritado e com confusão mental.

- Aprender torna-se muito mais difícil e a memória começa a falhar

- Ganho de peso, perda muscular, dor de cabeça também pode ocorrer

- Há maior risco de desenvolver hipertensão, diabetes e obesidade.


:::

Comprovadamente, o sono traz diversos benefícios “garantidores de saúde”, podemos citar alguns, como:

- Potencialização da capacidade de aprender, memorizar e tomar decisões;
- Melhora do autocontrole, redução de más sentimentos e maior criatividade;
- Reabastece o arsenal do nosso sistema imune, protegendo o corpo;
- Reforma o estado metabólico do corpo ajustando o equilíbrio de insulina e glicose circulante;
- Mantém o adequado funcionamento do sistema cardiovascular;
- Regula o apetite, contribuindo para o controle de peso corporal;
- Mantém um florescente microbioma no intestino, o que nos leva a ter mais saúde nutricional;
- Dentre muitos outros benefícios.



## Teste seus conhecimentos


```{r Quiz}
quiz (
  question("Para ter mais saúde, quantas horas devo dormir por dia?",
    answer("Quantas horas eu conseguir"),
    answer("Menos de 5 horas por dia"),
    answer("Cerca de 8 horas por dia", correct = TRUE),
    answer("Não preciso dormir"),
allow_retry = TRUE,
random_answer_order = TRUE
 ),

question_checkbox(
    "Podemos citar como sinais de sono não reparador",
  answer("Sonolência diurna", correct = TRUE),
  answer("Falta de atenção/ concentração", correct = TRUE),
  answer("Lapsos de memória", correct = TRUE),
  answer("Dificuldade de raciocínio", correct = TRUE),
  answer("Queda na imunidade", correct = TRUE),
  answer("Irritabilidade" , correct = TRUE ),
  answer("Alterações hormonais", correct = TRUE ),
  answer("Hipertensão" , correct = TRUE ),
  random_answer_order = TRUE,
  allow_retry = TRUE,
  try_again = "Be sure to select all toppings!"
 ),

question_checkbox(
    "Para ter mais qualidade de sono, é fundamental",
  answer("Realizar exercícios físicos e se alimentar próximo ao horário de dormir",),
  answer("Ir para a cama apenas quando estiver com sono", correct = TRUE),
  answer("Usar celular na cama"),
  answer("Manter o ambiente calmo, silencioso e escuro", correct = TRUE),
  answer("Tratar com carinho", correct = TRUE),
  random_answer_order = TRUE,
  allow_retry = TRUE,
  try_again = "Be sure to select all toppings!"
 ),


question_checkbox(
    "Todas as profissões exigem determinado nível de atenção e concentração para desempenhar ações **seguras**. Após descobrir todos os prejuízos que a privação de sono causam à concentração e raciocínio, dormir menos que 8 horas por dia:",
  answer("Aumenta as chances da ocorrência de acidentes e erros", correct = TRUE),
  answer("No caso de profissionais da saúde, coloca a segurança do profissional e do paciente em risco", correct = TRUE),
  answer("Melhora o desempenho profissional"),
  answer("Garante mais segurança e assertividade nas ações realizadas"),
  answer("Aumenta a ocorrência de doenças", correct = TRUE),
  answer("vPromove melhora geral da saúde do profissional"),
  random_answer_order = TRUE,
  allow_retry = TRUE,
  try_again = "Be sure to select all toppings!"
 )
)

```

:::

## Saiba mais sobre o sono

### Como ter mais qualidade de sono [clique aqui](https://www.youtube.com/watch?v=FwcjXaXCEWY)


### Sono, saúde e qualidade de vida [clique aqui](https://www.youtube.com/watch?v=7LjVRlPmqOQ)


### Segurança do paciente [clique aqui](https://www.youtube.com/watch?v=MiummDk8O5c)


### Sono, insônia e higiene do sono [clique aqui](https://www.youtube.com/watch?v=8RgPyNiN6Dw)



