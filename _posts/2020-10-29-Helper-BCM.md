---
layout: post
title: Helper Brasil Conta Comigo
date: 2020-10-29
---

### What is Brasil Conta Comigo?

<center>
<div>
 <img src="https://raw.githubusercontent.com/ItamarRocha/ItamarRocha.github.io/master/images/apoiasus/BCM.jpeg" alt="logo_medway" style="width:550px">
</div>
</center>

[Brasil Conta Comigo](https://www.gov.br/pt-br/noticias/saude-e-vigilancia-sanitaria/2020/04/201co-brasil-conta-comigo201d-habilita-estudantes-da-saude-para-atuar-no-combate-ao-coronavirus) is a Governmental program that aims to increase the number of professionals in the fight against COVID-19. It intends to do so by recruiting students from the 5º and 6º years of Medical School along with last year students from the Nursing, physiotherapy, and farmaceutical school.
<hr>

### Problem Overview

The main spotted problem is the way the data is displayed. There is no filter. The places with vacancies are shown in a table at [ApoiaSUS](https://sgtes.unasus.gov.br/apoiasus/login/listadevagas.asp), followed by each profession slot number. Even though the data is grouped by states, there are more than 5570 cities in Brazil. With that said, finding a city near yours and that fulfills your profession type can be a difficult task. 
<hr>

### Tools Used

The project was done entirely in Python and deployed with Heroku. The libraries used in Python were:
* Pandas
* Numpy
* Streamlit
* Unidecode
* geopy
<hr>

### Preprocessing

The work consisted of Joining three tables, one table that contains the data in ApoiaSUS website, the [data with the IBGE code](https://github.com/romulokps/apoiasus/raw/master/populacaoBR2.csv) and the [data that stores the latitude and the longitude of each city](https://github.com/kelvins/Municipios-Brasileiros/raw/main/csv/municipios.csv), so we could use them to calculate an approximate distance.

We did the string preprocessing in each city and state name, removing accents and other characters that could lead to a more complex search system, and we lowered all the strings in the table that we use as search keys.

### Web App

The entire application was done using streamlit. We used it to generate the data with the filter sidebar, along with the map visualization. To adjust the data shown with the filter we used pandas dataframe .loc methods and to calculate the distance we used geopy.distance.

The code can be found at [the GitHub repository](https://github.com/romulokps/apoiasus).

### Results

The project is no longer working, since the govern has ended the program. You can see a preview of how it was by watching the video below.

[![](http://img.youtube.com/vi/IoWE-PGk1Q0/0.jpg)](http://www.youtube.com/watch?v=IoWE-PGk1Q0 "Helper ApoiaSus")

### Questions?

Thank you for your time!

You can reach me out on any social media at the end of the page.