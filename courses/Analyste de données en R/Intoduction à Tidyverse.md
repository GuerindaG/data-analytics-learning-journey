# Tidyverse Cheat Sheet

`tidyverse` est un **ensemble de packages R cohérents** pour la manipulation, le nettoyage et la visualisation de données.  
Tous les packages partagent la philosophie “tidy data” : chaque colonne = variable, chaque ligne = observation.

---

## Packages principaux

| Package | Usage |
|---------|-------|
| `dplyr`  | Manipulation de données (filtrer, trier, résumer, regrouper) |
| `ggplot2` | Visualisation graphique |
| `tidyr`  | Restructuration et nettoyage de données (pivot, spread, gather) |
| `readr`  | Import/export de fichiers CSV, TSV, etc. |
| `purrr`  | Programmation fonctionnelle (map, reduce, etc.) |
| `tibble` | Version améliorée de `data.frame` |
| `stringr` | Manipulation de chaînes de caractères |
| `forcats` | Gestion des variables factor (catégorielles) |

---

## 1- dplyr : Manipulation de données

| Fonction | Description | Exemple |
|----------|------------|---------|
| `select()` | Sélectionner ou exclure des colonnes | `df %>% select(nom, age)` <br> `df %>% select(-age)` |
| `filter()` | Filtrer les lignes selon une condition | `df %>% filter(age > 18)` <br> `df %>% filter(age > 18, sexe == "F")` |
| `arrange()` | Trier les données | `df %>% arrange(age)` <br> `df %>% arrange(desc(age))` |
| `mutate()` | Créer ou modifier des colonnes | `df %>% mutate(age_mois = age * 12)` |
| `summarise()` | Calculer des statistiques | `df %>% summarise(age_moyen = mean(age, na.rm = TRUE))` |
| `group_by()` | Regrouper par variable | `df %>% group_by(sexe) %>% summarise(age_moyen = mean(age, na.rm = TRUE))` |
| `count()` | Compter occurrences ou pondérer | `df %>% count(state)` <br> `df %>% count(state, wt = population, sort = TRUE)` |
| `n()` | Nombre d’observations dans un groupe | `df %>% group_by(sexe) %>% summarise(total = n())` |
| `ngroup()` | Numéroter les groupes | `df %>% group_by(sexe) %>% mutate(id_groupe = ngroup())` |
| `slice_max()/slice_min()` | Top/bottom lignes selon une colonne | `df %>% slice_max(age, n = 2)` |

---

## 2- ggplot2 : Visualisation

| Fonction / Geom | Description | Exemple |
|-----------------|------------|---------|
| `geom_point()` | Nuage de points | `ggplot(df, aes(x = age, y = salaire)) + geom_point()` |
| `geom_line()` | Courbe / ligne | `ggplot(df, aes(x = date, y = ventes)) + geom_line()` |
| `geom_bar()` | Barres (compte automatique) | `ggplot(df, aes(x = sexe)) + geom_bar()` |
| `geom_col()` | Barres avec hauteur définie | `ggplot(df, aes(x = sexe, y = effectif)) + geom_col()` |
| `geom_boxplot()` | Boîte à moustaches | `ggplot(df, aes(x = sexe, y = salaire)) + geom_boxplot()` |
| `geom_histogram()` | Histogramme | `ggplot(df, aes(x = age)) + geom_histogram(binwidth = 5)` |
| `facet_wrap(~var)` | Graphique par catégorie | `ggplot(df, aes(x = age, y = salaire)) + geom_point() + facet_wrap(~sexe)` |
| `aes(color = var)` | Couleur selon une variable | `aes(color = sexe)` |
| `aes(fill = var)` | Remplissage selon une variable | `aes(fill = sexe)` |
| `geom_smooth(method = "lm")` | Ligne de tendance / régression | `geom_smooth(method = "lm")` |
| `theme_*()` | Thème graphique | `theme_minimal()`, `theme_classic()` |
| `labs(title, x, y)` | Titre et axes | `labs(title="Âge vs Salaire", x="Âge", y="Salaire")` |
| `scale_color_manual()` | Couleurs personnalisées pour color | `scale_color_manual(values=c("F"="red","M"="blue"))` |
| `scale_fill_manual()` | Couleurs personnalisées pour fill | `scale_fill_manual(values=c("F"="pink","M"="lightblue"))` |

---

## 3- tidyr : Restructuration de données

| Fonction | Description | Exemple |
|----------|------------|---------|
| `pivot_longer()` | Passer de large → long | `df %>% pivot_longer(cols = starts_with("jan"), names_to = "mois", values_to = "ventes")` |
| `pivot_wider()` | Passer de long → large | `df %>% pivot_wider(names_from = mois, values_from = ventes)` |
| `separate()` | Séparer une colonne en plusieurs | `df %>% separate(col = "date", into = c("jour","mois","annee"), sep = "-")` |
| `unite()` | Fusionner plusieurs colonnes | `df %>% unite("date_complete", jour, mois, annee, sep = "-")` |

---

## 4- readr : Import/export de fichiers

| Fonction | Description | Exemple |
|----------|------------|---------|
| `read_csv()` | Lire un CSV | `df <- read_csv("data.csv")` |
| `write_csv()` | Écrire un CSV | `write_csv(df, "data_export.csv")` |

---

## 5- purrr : Programmation fonctionnelle

| Fonction | Description | Exemple |
|----------|------------|---------|
| `map()` | Appliquer une fonction à chaque élément | `map(list(1,2,3), ~ .x^2)` |
| `map_df()` | Appliquer et combiner en data frame | `map_df(list(df1, df2), ~ .x)` |
| `map_dbl()` | Retourne un vecteur numérique | `map_dbl(list(1,2,3), ~ .x*2)` |
| `map_chr()` | Retourne un vecteur de caractères | `map_chr(list("a","b"), ~ paste0(.x,"_new"))` |

---

## POints clés

- Toujours utiliser **`%>%`** pour enchaîner les opérations  
- Préparer les données avec **dplyr** avant visualisation avec **ggplot2**  
- Utiliser **`na.rm = TRUE`** dans les fonctions de résumé pour éviter les `NA`  
- `tidyverse` encourage une syntaxe **propre, lisible et cohérente**

---
## Source
- Datacamp & Recherche

 Cette cheat sheet couvre les **packages essentiels du tidyverse** pour la manipulation et la visualisation de données en R.
