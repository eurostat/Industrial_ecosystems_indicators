# Industrial_ecosystems_indicators
Demonstration of a methodology to estimate Industrial ecosystems indicators published in the Annual Single Market Report (ASMR) from publicly available Eurostat data.

Each folder includes 4 subfolders:
-	Scripts: Including Python Scripts as Jupyter notebook. Can be executed in Jupyter labs. Make sure that the Auxiliary files are in the same folder as the script. 
-	Html: Including Python Scripts with the cell output to be open with the web browser.
-	Output: Output tables with the calculation results as an excel file.  Is we rerun the script the output will be overwritten.
-	Auxiliary: excel files that are requested by the script to load data that is needed for the calculation of the kpi. Should be in the same folder as the script.
o	In some cases there are no auxiliary files and all the data is retrieved from Eurostat directly
o	In other cases, you will have a excosystemweights file (regular or extended) which it is fixed for all the calculations.
o	In some cases there are auxiliary files that are an output of another indicator. As long as we are calculating the same period 2011-2018 these auxiliary files are valid. If we want a different period (ej. 2011-2020) and the auxiliary file is from an output, we should recalculate first the output for the period we are interested in (e.g. 2011-2020) and then copy the output (used as an auxiliary) in the same folder as the script we want to recalculate (otherwise an error might emerge).

## POP-UPS
Some files have been configured with pop-up windows for selection:
For example, for value added calculation we can select the units=[CP_MEUR] and the indicator [B1G].
When running the script the script will stop when the window pops-up. The window will allow you to pick the corresponding value (for example for units) and then you will click accept and it will display the selected value and you will confirm with ok (there is no option to cancel, if you are mistaken then restart the kernel and rerun the script again). If there is a second or a third window it will work the same way. The calculations will only be performed if you go through the windows and select the values.
This has been done to be able to select other indicators from the same database and other units. 
This pop-up window can also be done for the years, see for example Eurostat-sbs-ratioc31-N80valueadded.ipynb, however for the purpose of this work we decided to eliminate this option from most of the scripts to be more efficient when preparing and rerunning the script till the final version.
Be aware that the pop-ups might take some time to appear (typically less than 1 min).





## TO CHANGE THE PERIOD OF THE STUDY
First step is to update the Auxiliary files.
In this case Eurostat-sbs-ratioc31-N80valueadded.ipynb
We can see that although National Accounts have until 2021, the SBS data only is available till 2020 (as of December 2022). Then we can only update till 2020 and therefore update our Value Added kpi calculation with 2019 and 2020 values (from the original files that have the period 2011-2018).

We updated this file and called it ratioCN-Value added at factor cost - million euro2011-2020.xslx to differentiate it from the original files

Now we can go to the Value Added file Eurostat-NA-Value Added.ipynb and duplicate it. We renamed it Eurostat-NA-Value Added-Change period.ipynb and incorporated the calculation to the files. 
There are typically two steps to change the period of the study: 
-	Limit the year of the database to the first year of the study (we will maintain 2011 to make it easier, which will only result on adding more years to the original study)
-	Limit the last year of the study

Let’s see the Value added script:

In **cell [6]** we can see the years of the study. In this case starting from 1975 (and going till 2021 as of today). 
Then, in **cell [7]** we select the columns we want to drop from the study. In the original file from 1975 to 2010.

“year_start=1975
year_study=2011”

If in our new request we wanted from 2013 to 2020 then we change it accordingly. Then, in year_start we will put 1975 and in year_study we will put the first year we want to calculate (in this case 2013):“year_start=1975. year_study=2013”

As we are maintaining 2011 we don’t need to change anything in cell [7]

In **cell [10]** we change the calculation to the new ratio file ratioCN-Value added at factor cost - million euro2011-2020.xlsx. *We do it here this way because we don’t want to overwrite the original ratioCN-Value added at factor cost - million euro.xlsx, but if we update the Eurostat-sbs-ratioc31-N80valueadded.ipynb and overwrite its output file (atioCN-Value added at factor cost - million euro.xlsx), it won’t be necessary to change anything in this cell.  

Later in **cell [13]** we will select the range of years that we want to calculate in the line:

“for j in range (2011,2019):”

This will calculate from 2011 to 2018.

Then if I want to calculate from 2013 to 2020 the line should be:

“for j in range (2011,2021):”

Once we have changed this in the script we can rerun it and get the new results. 

To maintain a different name of the output file in **cell [14]** we added 2011-2022 to the filename. If we are overwriting this is not needed.

In cell[15] we extract gdp values from 2011 till the last year available (2021 by December 2022)
In the original file in this part we eliminated also years 2020 and 2021, but there is no need really. Then by putting a comment symbol in python “#”  
“#years.append(2020)
#years.append(2021)”
we don’t eliminate these columns from the gdp extraction. As the iteration for the additional kpis (e.g. value added as percentage of the gdp) is starting 2011 and finishing in the last column of the Value Added table per year, then the program will only take the gdp values for the same years as the Value Added table (in this example from 2011 to 2020, even gdp table retrieved as an output of **cell [15]** might include an additional column for 2021)

To maintain a different name of the output file in **cell [17]** we added 2011-2022 to the filename. If we are overwriting this is not needed.

To maintain a different name of the output file in **cell [19]** we added 2011-2022 to the filename. If we are overwriting this is not needed.

**we didn’t update kpi productivity because to update this table it is needed to update first "Total employment domestic concept.xlsx” (Eurostat-NA-employment.ipynb) which at the same time requires to update: “ratioCN-Persons employed - number.xlsx” (Eurostat-sbs-ratioc31-N80employment.ipynb) but the dynamics to update these files is very simmilar.


This project has been implemented by GOPA Luxembourg. 

