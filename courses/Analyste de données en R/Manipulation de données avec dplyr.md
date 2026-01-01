# Manipulation de données avec dplyr

## Objectifs
Maitriser les fonctions principales de dplyr pour manipuler les données

## Structure générale d’une requête dplyr
  donnees(le dataframe) %>%
  fonction1() %>%
  fonction2() %>%
  fonction3()

## Verbes ou fonctions clés de dplyr
- ### Select() : pour sélectionner des colonnes
  df %>% select(nom, age, sexe)
  df %>% select(-age) pour exclure un paramètre du dataframe par exemple
  counties_selected <- counties %>% select(state, county, population, unemployment) exemple pour la création d'une nouvelle table
- ### Filter() : pour filtrer des lignes
  df %>% filter(age > 18) ou df %>% filter(age > 18, sexe == "F") pour les conditions multiples par exemple
- ### arrange() : pour trier les données
  df %>% arrange(age)
  df %>% arrange(desc(age)) selon l'ordre
- ### mutate() : pour créer ou modifier des colonnes
  df %>% mutate(age_mois = age * 12)
- ### summarise() : pour calculer des statistiques
  df %>% summarise(moyenne_age = mean(age, na.rm = TRUE))
- ### group_by() : pour regrouper les données
  df %>%
  group_by(sexe) %>%
  summarise(moyenne_age = mean(age, na.rm = TRUE))

## Exemple d'une structure de combinaison de fonction
  df %>%
  filter(age >= 18) %>%
  group_by(sexe) %>%
  summarise(
    effectif = n(),
    age_moyen = mean(age, na.rm = TRUE)
  ) %>%
  arrange(desc(age_moyen))
  
## Points clés à retenir
- Une fonction par ligne pour la lisibilité
- Utiliser na.rm = TRUE pour éviter les erreurs
- Toujours faire group_by() avant summarise()
- Préférer |> (R ≥ 4.1) au %>% si possible

## Comparaison avec SQL
| SQL      | dplyr        |
| -------- | ------------ |
| SELECT   | `select()`   |
| WHERE    | `filter()`   |
| ORDER BY | `arrange()`  |
| GROUP BY | `group_by()` |
| COUNT()  | `n()`        |
| AVG()    | `mean()`     | 

## Source
- DataCamp - ISHEERO
