Logical DAX Functions

Evaluates an expression and returns a specified value if the expression encounters an error; otherwise, it returns the value of the expression itself.

Step-1: Create a measure 

Generate_Error = "A"+1

Step-2: Now, add a Card visual to your Power BI page and drag the measure onto it.

it returns an error ‘can not convert Text to Number’, now we handle the error with some messages.

Step-3: Create other measure 

IFERROR_Measure = IFERROR("A"+1,"Wrong Input")

Step-4: After this drag measure into Card visual, it returns the given error message instead of conversion error.

If expression not return any error, it returns the value of expression

>>>>  IFERROR_Measure_2 = IFERROR(1+1,"Wrong Input")


============switch=====================

Evaluates an expression against a list of values and returns one of multiple possible result expressions. It comes under Logical Dax function category.

Step-1: Create one measure and write conditional statement 

Sales_Tag =
Var TotalSales= SUM(Orders[Sales])
Return
SWITCH(TRUE(),
TotalSales<50000, "Low",
TotalSales>50000 && TotalSales< 100000, "Medium",
TotalSales>100000, "High",
"Other"
)

Step-2: If condition has true, Switch will return the result in form of “Low”, “Medium” & “High”.

Step-3: You can change the font color white for Sales_Tag measure total, because here no need to display Text as in Total. Due to this.

Select table visual >  format bar > field Formatting, and follow the below properties:

Select Sales_Tag from dropdown
Choose font color white, by default it is selected but select again to apply this.
Turned off Apply to values
Turned on Apply to total

=================================
Get Month Name from Month number:
Create one calculated column, and write below SWICTH DAX formlua to get month name from month number.

Return Month Name =
SWITCH(Orders[MonthNumber],
1,"January",
2,"February",
3,"March",
4,"April",
5,"May",
6,"June",
7,"July",
8,"August",
9,"September",
10,"October",
11,"November",
12,"December",
"Invalid Month Number"
)

===========IF=================
IF DAX function is used to checks a condition, and returns one value when it’s TRUE, otherwise it returns a second value.

Step-1: Create a measure and write IF condition

IF Condition =
Var TotalSales = SUM(Orders[Sales])
Return
IF(TotalSales >= 100000, "Profit", "Loss")

Step-2 : Create another measure to implement a nested IF condition.

Nested_IF =
Var TotalSales= SUM(Orders[Sales])
Return
IF(TotalSales<50000, "Low",
IF(TotalSales>50000 && TotalSales< 100000, "Medium",
IF(TotalSales>100000, "High",
"Other"
)
)
)

Step-3: Drag both measures onto the table visual

============AND===================

Checks whether both arguments are TRUE, and returns TRUE if both arguments are TRUE. Otherwise returns false. 

Suppose you are interested to see the sales only where Category = “Furniture” and Sub Category =”Chairs”.

In order to achieve this you can use AND DAX function, it will check both conditions are true or not, if both conditions are TRUE then returns TRUE otherwise returns false.

 create one measure for AND Dax function-

SUM with AND =
CALCULATE(
SUM(‘Global-Superstore'[Sales]),
FILTER (‘Global-Superstore’,
AND (
‘Global-Superstore'[Category] = “Furniture”,
‘Global-Superstore'[Sub-Category]=“Chairs”
)
)
)

Now drag the measure to Table and in Card visual, it will return the sum only for whether both conditions are true.

===============================
Another way to write AND function-
Instead of AND you can use && sign, let’s have a look in below DAX code.

SUM with AND = CALCULATE(
SUM('Global-Superstore'[Sales]),
FILTER (
'Global-Superstore',
'Global-Superstore'[Category] = "Furniture" &&
'Global-Superstore'[Sub-Category]="Chairs"
) )
============================================
OR (||) DAX 

Checks whether one of the arguments is TRUE to return TRUE. The function returns FALSE if both arguments are FALSE. 

Within this dataset, we have categories, subcategories, and corresponding sales data.

Now create a measure for OR Dax function

SUM with OR =
CALCULATE(
SUM('Global-Superstore'[Sales]),
FILTER ('Global-Superstore',
OR (
'Global-Superstore'[Category] = "Furniture",
'Global-Superstore'[Sub-Category]="Art"
)
)
)

Now drag measure to Table and in Card visual, It will return SUM of sales whether one condition true.

===============================
Another way to write OR function-
Instead of OR  you can use || sign

SUM with Or= CALCULATE(
SUM('Global-Superstore'[Sales]),
FILTER (
'Global-Superstore',
'Global-Superstore'[Category] = "Furniture" ||
'Global-Superstore'[Sub-Category]="Art"
) )

=================NOT DAX==============
It’s a logical DAX function that used to change a value or expression from FALSE to TRUE or TRUE to False.

Now create a measure for NOT Function

NOT_DAX =
CALCULATE(
SUM('Global-Superstore'[Sales]),
FILTER('Global-Superstore',
NOT('Global-Superstore'[Region]) IN {"Africa", "Canada", "Caribbean"}
))

Above DAX function will returns total sales of region excluding these three regions – “Africa”, “Canada”, “Caribbean”.

================COALESCE ====================
It’s a logical DAX function that used to returns the first expression that does not evaluate to BLANK. If all expressions evaluate to BLANK, BLANK is returned.

Example -1:
Add one measure to understand the working of Coalesce DAX-

Coalesce_DAX = COALESCE( BLANK() , "No value")

Example-2
Add another measure and write below DAX code

Coalesce_DAX = COALESCE( 12345 , "No value")

Example-3
Add one more measure and write below DAX code-

Coalesce_DAX = COALESCE( BLANK() , BLANK())







