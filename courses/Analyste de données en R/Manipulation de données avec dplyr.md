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
  df %>% select(-age) : pour exclure un paramètre du dataframe par exemple
  counties_selected <- counties %>% select(state, county, population, unemployment) : exemple pour la création d'une nouvelle table
- ### Filter() : pour filtrer des lignes
  df %>% filter(age > 18)
  df %>% filter(age > 18, sexe == "F") : pour les conditions multiples par exemple
- ### arrange() : pour trier les données
  df %>% arrange(age)
  df %>% arrange(desc(age)) selon l'ordre
- ### mutate() : pour créer ou modifier des colonnes
  df %>% mutate(age_mois = age * 12)
- ### summarise() : pour calculer des statistiques
  df %>% summarise(moyenne_age = mean(age, na.rm = TRUE))
  | Fonction   | Description                                  | Exemple                                            |
| ---------- | -------------------------------------------- | -------------------------------------------------- |
| `sum()`    | Somme des valeurs d’un vecteur               | `sum(df$age)` → total des âges                     |
| `mean()`   | Moyenne des valeurs                          | `mean(df$age)` → âge moyen                         |
| `median()` | Médiane (valeur centrale)                    | `median(df$age)` → âge médian                      |
| `min()`    | Valeur minimale                              | `min(df$age)` → âge minimum                        |
| `max()`    | Valeur maximale                              | `max(df$age)` → âge maximum                        |
| `n()`      | Nombre d’observations dans un groupe (dplyr) | `df %>% group_by(sexe) %>% summarise(total = n())` |
  
- ### group_by() : pour regrouper les données
  df %>%
  group_by(sexe) %>%
  summarise(moyenne_age = mean(age, na.rm = TRUE))
- ### Count() : pour compter
  df %>% count(state)
  df %>% count(state, sort = TRUE) : Count et sort
  df %>% count(state, wt = population, sort = TRUE) : wt dans count() permet de faire un comptage pondéré au lieu d’un comptage simple. Utile quand chaque ligne représente plusieurs unités (population, ventes, etc.) et pas juste 1.

## Exemple d'une structure de combinaison de fonction
  df %>%
  filter(age >= 18) %>%
  group_by(sexe) %>%
  summarise(
    effectif = n(),
    age_moyen = mean(age, na.rm = TRUE)
  ) %>%
  arrange(desc(age_moyen))

### Autres fonctions 
# `slice_max()` et `slice_min()` (dplyr)

| Fonction | Description | Exemple | Output |
|----------|-------------|---------|--------|
| `slice_max(x, n = k)` | Sélectionne les `k` lignes avec les **valeurs les plus grandes** de la colonne `x` | `df %>% slice_max(population, n = 2)` | CA (5000), NY (3000) |
| `slice_min(x, n = k)` | Sélectionne les `k` lignes avec les **valeurs les plus petites** de la colonne `x` | `df %>% slice_min(population, n = 2)` | TX (1000), CA (1000) |
| `with_ties = TRUE/FALSE` | Conserver ou non les **lignes ex-aequo** | `df %>% slice_max(population, n = 1, with_ties = TRUE)` | Toutes les lignes ayant la valeur max |
| `by = ...` | Appliquer la sélection **par groupe** | `df %>% group_by(state) %>% slice_max(population, n = 1)` | TX (2000), CA (5000), NY (3000) |

## Notes

- `slice_max()` et `slice_min()` sont très utiles pour trouver les **top/bottom records** dans un dataset ou un groupe.
- Par défaut, `with_ties = TRUE`, donc toutes les lignes égales à la valeur max/min sont conservées.
- Combinez avec `group_by()` pour faire un **top/bottom par catégorie**.

  
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
