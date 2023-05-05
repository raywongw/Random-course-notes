


## Tutorial 4

Consider the following three tables in a Cookbook database.

Ingredient (<ins>iID</ins>, iname, madeIn)
Dish (<ins>dID</ins>, dname, cuisine, vegetarian, introduction)
Recipe (<ins>dID</ins>, <ins>iID</ins>, usageDec)


- Since a dish can use multiple ingredients, the relation Recipe matches up Ingredient(identified by `iID`) with Dish (identified by `dID`) and stores the usage of the ingredient in the cooking progress.



### Q1. List the `iID`, `iname`, `usageDec` of the ingredient(s) in the recipe of the dish with dID as 2
- In descending order of `iID`

```MySQL
SELECT DISTINCT I.iID, I.iname, R.usageDec FROM Ingredient I, Recipe R
WHERE I.iID = R.iID AND R.dID = 2
ORDER BY iID DESC;
```


### Q2. List the `dID`, `dname` of all Korean cuisine vegetarian dish(es) without using “peanut” in its recipe. 
- Case insensitive matching, in descending order of `dID`, remove duplicates.


```MySQL
SELECT DISTINCT D.dID, D.dname FROM dish D
WHERE D.cuisine = 'Korean' AND D.vegetarian = TRUE AND D.dID NOT IN 
	(SELECT R.dID FROM Recipe R, Ingredient I
	 WHERE R.iID = I.iID AND I.iname LIKE "peanut")
ORDER by dID DESC;
```


### Q3. List the `iID`, `iname` of the ingredient(s) in the recipe of the Chinese cuisine dish(es) with “crab” appear in the introduction.
- Case insensitive matching, in descending order of `iID`, remove duplicates.
```MySQL
SELECT DISTINCT iID, iname FROM Ingredient I
WHERE iID IN (SELECT iID FROM Recipe R, Dish D
			  WHERE D.dID = R.dID AND D.introduction LIKE '%crab%' AND D.cuisine = 'Chinese')
ORDER BY iID DESC
```

| iID | iname  |
| --- | ------ |
| 4   | Onion  |
| 2   | Peanut |
| 1   | King Crab Legs       |

### Q4. List the `dID`, `dname` of the dish(es) that uses the ingredient “king crab legs”(iname) from “Alaska” (madeIn) in its recipe.
- Case insensitive matching, in descending order of dID, remove duplicates.

No JOIN Attempt:
```MySQL
SELECT DISTINCT dID, dname FROM Dish D
WHERE dID IN (SELECT R.dID FROM Recipe R
			  WHERE R.iID IN (SELECT iID FROM Ingredient I
							  WHERE iname = 'king crab legs' AND madeIN LIKE '%Alaska%'))
ORDER BY dID DESC
```


| dID | dname            |
| --- | ---------------- |
| 5   | Garlic Crab Legs |
| 3   | Crab Salad       |



### Q5. List the `iID`, `iname` of the ingredient(s) that are not in the recipe of any Chinese cuisine dishes.
- In descending order of `iID`, remove duplicates.
```MySQL
SELECT iID, iname FROM Ingredient I
WHERE iID NOT IN (SELECT DISTINCT iID FROM Recipe R
			   WHERE R.dID IN (SELECT dID FROM Dish D
							   WHERE D.cuisine = "Chinese"))
ORDER BY iID DESC

/*0.0011 sec*/
```

| iID | iname          |
| --- | -------------- |
| 10  | King Crab Legs |
| 9   | Shrimp         |


### Q6. List the `dID`, `dname` of the dish(s) that use all 3 ingredients `(“Ginger”, “Onion” and “Garlic”)` in its recipe.
- In descending order of `dID`, remove duplicates.
```MySQL
SELECT DISTINCT dID, dname FROM Dish D
WHERE D.dID IN (SELECT dID FROM Recipe R
			    WHERE R.iID IN (SELECT iID FROM Ingredient I
							    WHERE iname IN ('Ginger', 'Onion', 'Garlic')))
ORDER BY dID DESC

/*0.0012 sec*/
```

| dID | Dname                  |
| --- | ---------------------- |
| 7   | Fired Shrimp           | 
| 5   | Garlic Crab Legs       |
| 1   | Red Braised Pork Belly |


### Q7. List the `iID`, `iname` of the common ingredient(s) among the dishes `(“Garlic Crab Legs”, “Crab Salad”, and “Fried Shrimp”)`
- In descending order of `iID`, remove duplicates.
```MySQL
SELECT iID, iname FROM Ingredients I
WHERE 
```

| iID | iname |
| --- | ----- |
| 4   | Onion |


### Q8. List the `dID`, `numOfIngredients` of dish(es) with 3 to 5 ingredients in its recipe.
- `numOfIngredients` is the number of ingredients used in the recipe of the dish.
- In descending order of `dID`.
```MySQL

```

| dID | numOfIngredients |
| --- | ---------------- |
| 7   | 4                |
| 5   | 4                |
| 4   | 3                |
| 3   | 3                |
| 1   | 4                |


### Q9. Find the `dishCount` for the ingredient called `“Geoduck”`.
- dishCount is the number of dish(es) that use “Geoduck” in its recipe.
- You can assume that there is at least one dish that use “Geoduck” in its recipe in the cookbook.
```MySQL

```

| dishCount |
| --------- |
| 1          |


### Q10. For all ingredients madeIn “Japan”, list the iID, numOfKoreanDishes.
- `numOfKoreanDishes` is the number of Korean cuisine dishes using that ingredient in its
recipe (can be 0).
- in descending order of iID.

```MySQL

```

| iID | numOfKoreanDishes |
| --- | ----------------- |
| 8   | 1                 |
| 4   | 0                  |


### Q11. List the `iID`, `iname` of the top 3 most popular ingredients among all Chinese cuisine dishes. 
- In case of a tie, resolve by listing the ingredients with smaller iID first.
```MySQL

```

| iID | iname  |
| --- | ------ |
| 2   | Peanut |
| 4   | Onion  |
| 5   | Garlic | 


