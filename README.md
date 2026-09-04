# **ECE2112: Programming Assessment 3**
**Submitted by: Jazmine Mikaela L. Rafols | 2ECE-D**   
**Submitted on: September 4, 2026**

## **Objectives of the Experiment**
> At the end of Programming Assessment 3, the student should be able to load a `CSV` dataset into a Pandas DataFrame, select rows and columns using positional and label-based indexing, filter records using boolean conditions on a DataFrame column, and extract a well-defined subset of data without altering the source data for each problem given. The source data `cars.csv` shall be used throughout experiment 3.

## A. Reproducible Normalization Problem
> **Instructions:** Load `cars` to display the shape and the complete list of column names of `cars`. Then, using positional slicing, create the subset `cars_6_to_10` containing rows 6 through 10 of the dataset, where the first row is row `1`. The subset `cars_6_to_10` should only display the columns `Model`, `mpg`, `cyl`, `hp`, and `gear`, in that order. When retrieving rows 6 to 10, the row selection must use `iloc`, while the column selection must use column labels.

To load `cars.csv` as a Pandas DataFrame, the python library `Pandas` must be first initialized to begin with data structures,
```python
import pandas as pd
```
After initialization, this will allow the use of data structures and its following data analysis tools.

### Solution to the Problem

Now, `cars.csv` can be displayed through using `pd.read_csv` and labeled as `cars`. The following should display a shape of 32 rows and 12 columns containing the following characteristics: `Model`, `mpg`, `cyl`, `disp`, `hp`, `drat`, `wt`, `qsec`, `vs`, `am`, `gear`, and `carb`.

Then under the subset `cars_6_to_10`, use positional slicing to contain only the sixth to tenth row of the dataset, considering that the first row is row `1`. However, it should be noted that the row selection must only use `iloc` when retrieving. The syntax should be as follows:
```python
cars_6_to_10 = cars.iloc[6:11]
cars_6_to_10
```
`cars.iloc` utilizes the index [`6`] as it refers to row 6 and inclusive of the data frame, the index [`11`] refers to what row the range will end at and is exclusive of the given index; which explains why [`11`] is used to indicate that the rows will end on row 10. The colon operator `:` is the positional slicing separator to get the portion of the sequence needed. The returned subset should start with the `Model` name `Duster 360` and end at `Merc 280C`.

Although, it is required that `cars_6_to_10` should only return the columns `Model`, `mpg`, `cyl`, `hp`, and `gear` when displayed. To isolate those selected columns, `loc` can be used,
```python
cars_6_to_10.loc[:, ['Model','mpg','cyl','hp','gear']]
```
The empty spaces before and after the `:` means that it will take the whole table of the assigned columns, which are the requested columns aforementioned. Additionally, because of `cars.iloc[6:11]`, it only took the elements of those five columns. It should display a similar table from earlier but with only the isolated columns `Model`, `mpg`, `cyl`, `hp`, and `gear`:

| | Model | mpg | cyl | hp | gear |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **6** | Duster 360 | 14.3 | 8 | 245 | 3 |
| **7** | Merc 240D | 24.4 | 4 | 62 | 4 |
| **8** | Merc 230 | 22.8 | 4 | 95 | 4 |
| **9** | Merc 280 | 19.2 | 6 | 123 | 4 |
| **10** | Merc 280C | 17.8 | 6 | 123 | 4 |

## B. Model Lookup
> **Instructions:** Use Boolean indexing on the column `Model` to display the complete row for `Toyota Corolla`, then for `Pontiac Firebird`, display only the columns `Model`, `mpg`, `hp`, and `wt`. Store these two results in `toyota` and `pontiac`, respectively. Do not use a hard-coded row number to locate their models.

Similarly to problem A, the following will use `loc` to locate the two models: `Toyota Corolla`, and `Pontiac Firebird`, however, instead of row numbers, it will use Boolean indexing and the exact name of the model.

### Solution to the Problem

Using Boolean indexing, locating a specific model can be done through the equivalence operator `==` and entering the desired model. Let `cars.loc` be stored in the subset `toyota`,
```python
toyota = cars.loc[(cars['Model']=='Toyota Corolla'),:]
```
`cars[`Model`]` is essentially saying that, to locate the desired car model, it must refer to the main data frame `cars` under the column `Model` and then followed by the specific name `Toyota Corolla`. Again, `:` means it will take the complete table of the row as is. Printing `toyota` should return the complete row of `Toyota Corolla` and its elements.

The same is done with the model `Pontiac Firebird`, although with certain limitations. `pontiac` should only display a portion of the total columns: `Model`, `mpg`, `hp`, and `wt`. So `pontiac = cars.loc` has an extended Boolean condition after the car model retrieval and replacing `toyota`’s colon operator, as demonstrated below:
```python
pontiac = cars.loc[(cars['Model']==''Pontiac Firebird'), ['Model','mpg','hp','wt']]
```
The subsets `toyota` and `pontiac` will return the following tables:

| | Model | mpg | cyl | disp | hp | drat | wt | qsec | vs | am | gear | carb |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **19** | Toyota<br>Corolla | 33.9 | 4 | 71.1 | 65 | 4.22 | 1.835 | 19.9 | 1 | 1 | 4 | 1 |

| | Model | mpg | hp | wt |
| :--- | :--- | :--- | :--- | :--- |
| **24** | Pontiac Firebird | 19.2 | 175 | 3.845 |

## C. Multi-Model Subsetting
> **Instructions:** Create a DataFrame named `selected_cars` containing only the records for three models: `Datsun 710`, `Lotus Europa`, and `Ferrari Dino`. For `selected_cars`, retain only the  `Model`, `mpg`, `cyl`, `hp`, and `gear`. Select the rows by their model values rather than by row numbers. Display `selected_cars` and its shape, in which the final DataFrame must contain exactly three rows and five columns.

This time, the problem asks for three selected models that are far apart from each other within the main data frame. Boolean indexing would suffice this condition although with the help of the OR operator `|` to retrieve the individual models from the main data frame.

### Solution to the Problem

Assigning the Boolean condition to `Datsun 710`, `Lotus Europa`, and `Ferrari Dino` then utilizing the OR operator will mean that the command will filter the main data frame under the column `Model` through finding a direct match name of at least one of the three given models.
```python
cars = cars.loc[(cars['Model']=='Datsun 710') | (cars['Model']=='Lotus Europa') | (cars['Model']=='Ferrari Dino')]
```
Once identified, the subset `selected_cars` will create a data frame of these three through `pd.DataFrame` and assigning the five required attributes: `Model`, `mpg`, `cyl`, `hp`, and `gear` as shown:
```python
selected_cars = pd.DataFrame(cars, columns =['Model','mpg', 'cyl', 'hp', 'gear'])
```
The final data frame should return a shape of `(3, 5)`, in which it can be displayed through using:
```python
print(selected_cars.shape)
```
Then, printing `selected_cars` will return the following values,

| | Model | mpg | cyl | hp | gear |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **2** | Datsun 710 | 22.8 | 4 | 93 | 4 |
| **27** | Lotus Europa | 30.4 | 4 | 113 | 5 |
| **29** | Ferrari Dino | 19.7 | 6 | 175 | 5 |

---
### **Thank you for Reading!**
To view the complete program for Programming Assessment 3, refer to this link: [Programming Assessment 3 by Jazmine Rafols](https://github.com/Jazmine-Rafols/RAFOLS_ECE2112-PA3/blob/3c2b3aac7a7acc309dfdabc68f18648e09bfc366/Program_Assessment-3.ipynb)
### File Version History  
**September 4, 2026** - Initial upload (draft) of README and PA3 on GitHub. \
**September 4, 2026** - Version 2: uploaded the complete discussions for all problems.
