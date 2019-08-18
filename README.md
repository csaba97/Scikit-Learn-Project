# Scikit-Learn-Project to predict the grades of students in Romania at the Baccalaureate knowing their grades from the exam in 8th grade

# Installing the tool

1. Make sure Python is installed on the computer(check it with python –version). If it is
not, install it from the official Python website
2. Make sure pip is installed on the computer. Pip comes pre-installed with new Python
releases.
3. To install the tool as a standalone version, just type `pip install scikit-learn` in the
terminal
4. These tools: numpy, pandas, matplotlib, seaborn need to be installed to process
data, to plot functions and to use mathematical functions so for every tool just type
`pip install {name of the tool}`
5. Also it is highly recommended to install Jupyter Notebook which is a code editor in
which separate pieces of code can be executed, commented, plots can be made etc. To
install it, type: `pip install jupyter` in the terminal

# Data
The data from the 2012’s Baccalaureate is used. This data is taken from an Open sourced
source: Rolisoft : Bacalaureat-data. https://github.com/RoliSoft/Bacalaureat-Data.

# How to use it

The Jupyter notebooks are heavily commented so the execution flow can be understood from there...

# Some insights:

##  Predicting the target value romana final

Romana final is the grade for the final Baccalaureate grade in Romanian language. It is a
continuous value ranging from 0 to 10. So, this is a regression problem. Some information
about the target value:
![image](https://user-images.githubusercontent.com/37183688/63228963-9f9bf780-c203-11e9-97d9-7e5aadd2ddd8.png)

This was a tough experiment because a lot of feature engineering needed to be done, namely:
1. Removing highly correlated columns, because there are 42 columns in total with many
categorical features and we must speed up the algorithms somehow. Besides this, some
algorithms don’t work well with highly correlated features such as Linear Regression.
Several features were excluded because of correlation such as ’..nota’ and ’..contestatie’
for every type of grade because the ’...final’ column contains the final grade which is of
our interest. Yes, some observations could have been made regarding who goes to dispute
the grade(contestare), but because the columns contain sparse data I excluded them to
speed up the algorithm. We can see that ’media teze nationale’ and ’media la admitere’
are highly correlated(because one is used in the calculation of the other one). Also, ’nota
la limba romana’ and ’optional8 nota’ and ’nota la matematica’ are highly correlated
with both the ’media la admitere’ and ’media teze nationale’ These are obvious because
some of the columns are just the average of other columns, so these will be removed. But
there is a neat trick here: we won’t include the ’limba materna8 nota’ feature because it
has many empty values, but instead we include both the ’media teze nationale’ and the 
grades for other subjects because in this way ’media teze nationale’ will contain in itself
the value for ’limba materna8 nota’.  

![image](https://user-images.githubusercontent.com/37183688/63228989-d4a84a00-c203-11e9-91ca-3987d72eaed5.png)  
 
 
 2. Transforming categorical features. Random Forest can work well with Label Encoded
features and it is also quicker. One hot encoded features were used initially with Random
Forest to see the feature importance for every subcategory. In this way, we got some
interesting results such as Harghita county in itself is a very good predictor for the final
target value. Nume feature was replaced with firstnames, and students can contain multiple firstnames so they were one-hot encoded to allow multiple firstnames for a single
person. Also, ’limba moderna nota’ was a categorical feature but was replaced with a
single number which is the average of the grades got at the exam with A1 = 1 and B2
= 4. For those who have taken another language exam, their grades were replaced with
the maximum grade of 4.0.  
  
![image](https://user-images.githubusercontent.com/37183688/63228994-e689ed00-c203-11e9-86e9-4d850aa0f55a.png)  
 
 
 After running a Random Forest Regressor we got an accuracy of 70%. Cross validation
showed a score of 67% which is still a high value. Several other algorithms were tried. Only
one was with success(GradientBoostingRegressor) with an accuracy score of 72%.


 


