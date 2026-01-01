# Manipulation de données avec dplyr

## Objectifs
Maitriser les fonctions principales de dplyr pour manipuler les données

## Structure générale d’une requête dplyr
  donnees(le dataframe) %>%
  fonction1() %>%
  fonction2() %>%
  fonction3()

## Verbes et fonctions clés de `dplyr`

| Fonction / Verbe | Description | Exemple |
|-----------------|------------|---------|
| `select()` | Sélectionner ou exclure des colonnes | `df %>% select(nom, age, sexe)` <br> `df %>% select(-age)` <br> `counties_selected <- counties %>% select(state, county, population, unemployment)` |
| `filter()` | Filtrer les lignes selon une condition | `df %>% filter(age > 18)` <br> `df %>% filter(age > 18, sexe == "F")` |
| `arrange()` | Trier les données | `df %>% arrange(age)` <br> `df %>% arrange(desc(age))` |
| `mutate()` | Créer ou modifier des colonnes | `df %>% mutate(age_mois = age * 12)` |
| `summarise()` / `summarize()` | Calculer des statistiques sur un vecteur ou un groupe | `df %>% summarise(moyenne_age = mean(age, na.rm = TRUE))` |
| `sum()` | Somme des valeurs | `sum(df$age)` → total des âges |
| `mean()` | Moyenne | `mean(df$age)` → âge moyen |
| `median()` | Médiane | `median(df$age)` → âge médian |
| `min()` | Valeur minimale | `min(df$age)` → âge minimum |
| `max()` | Valeur maximale | `max(df$age)` → âge maximum |
| `n()` | Nombre d’observations dans un groupe (`group_by`) | `df %>% group_by(sexe) %>% summarise(total = n())` |
| `group_by()` | Regrouper les données selon une ou plusieurs colonnes | `df %>% group_by(sexe) %>% summarise(moyenne_age = mean(age, na.rm = TRUE))` |
| `count()` | Compter les occurrences ou faire un comptage pondéré | `df %>% count(state)` <br> `df %>% count(state, sort = TRUE)` <br> `df %>% count(state, wt = population, sort = TRUE)` (`wt` = poids / comptage pondéré) |


 **Notes importantes :**  
- `wt` dans `count()` sert à **pondérer le comptage** (utile pour population, ventes, etc.).  
- Toujours utiliser `na.rm = TRUE` dans `mean()`, `sum()`, etc. pour **ignorer les valeurs manquantes**.  
- `group_by()` doit précéder `summarise()` pour calculer des statistiques **par groupe**.

## Exemple d'une structure de combinaison de fonction
  `df %>%
  filter(age >= 18) %>%
  group_by(sexe) %>%
  summarise(
    effectif = n(),
    age_moyen = mean(age, na.rm = TRUE)
  ) %>%
  arrange(desc(age_moyen))`

### Autres fonctions 
# `slice_max()` et `slice_min()` (dplyr)

| Fonction | Description | Exemple | 
|----------|-------------|---------|
| `slice_max(x, n = k)` | Sélectionne les `k` lignes avec les **valeurs les plus grandes** de la colonne `x` | `df %>% slice_max(population, n = 2)` | 
| `slice_min(x, n = k)` | Sélectionne les `k` lignes avec les **valeurs les plus petites** de la colonne `x` | `df %>% slice_min(population, n = 2)` | 
| `with_ties = TRUE/FALSE` | Conserver ou non les **lignes ex-aequo** | `df %>% slice_max(population, n = 1, with_ties = TRUE)` | 
| `by = ...` | Appliquer la sélection **par groupe** | `df %>% group_by(state) %>% slice_max(population, n = 1)` | 

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
