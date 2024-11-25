# Homework 3 (Individual)

## Question 1

In this problem, you will examine accounting data for NVIDIA.

1. Import data stored in `data/NVIDIA_compustat.csv` into a Pandas dataframe

2. Report the number of columns in the dataset. We don't need most of them. Keep only the following columns: `conm`, `datadate`, `fyear`, `sale`, `cogs`, `xsga`, `xrd`, `ebitda`

3. At what frequency is the accounting data reported? Monthly? Quarterly? Annual? How can you tell? Show your work for this answer. In other words, include the Python code you needed to run to examine the data in preparing your answer.

4. Retrieve and report NVIDIA's total net sales (`sale`) for the 2016 fiscal year (`fyear`). Do it in three different ways:
    1. By indexing the position (row number, column number) with `iloc`
    2. Using the column name for sales and boolean/logical indexing to find the year
    3. Using row/column name indexing (`loc`). To do this, you'll first need to set the `fyear` column as the index.

5. Calculate annual sales growth in percent. Plot *as a bar chart* sales growth for all years starting with 2000. Sales growth is defined as

$$ S_t / S_{t-1} - 1 $$

6. Of the years plotted, in what year was sales growth lowest? In what year was it highest? Use Python code to identify these years, and check your answer by looking at the plot you made above.

7. Calculate NVIDIA's gross profit as its sales (`sale`) minus the cost of goods sold (`cogs`)

8. Calculate NVIDIA's earnings before depreciation, amortization, and taxes, usually abbreviated as EBITDA, as gross profit minus selling, general, and administrative expenses, usually abbreviated at SG&A (`xsga`). Your calculation should match exactly the `ebitda` column already in the dataset. Check to make sure that is the case.

9. What fraction of its profit does NVIDIA spend on research and development (R&D) expenses (`xrd`). Calculate and report the average of this fraction?

10. How do you think this fraction compares with most other companies? Is it higher or lower? Why do you think so?

When a question asks you to report an answer, print your result nicely formatted with enough text to give the reader appropriate context.

## Question 2

In this question, you will practice working with dates. The `data/vti.csv` file contains monthly returns (in percent) on VTI, Vanguard's ETF that tracks the S&P 500 stock index. We want to calculate the average *daily* return for each month.

To calculate the average daily return, we can use the compounding formula. It tells us how to get the monthly return $R_m$ from the daily return $R_d$, but you can solve for $R_d$ to get daily from monthly.

$$ R_m = (1 + R_d)^t - 1 $$

The problem is that $t$ is not the number of calendar days, but the number of trading days. The stock market is closed on weekends and holidays, so the number of trading days $t$ is lower than the number of calendar days in each month.

In this question, we will ignore holidays. But we will figure how to count only weekdays between two dates.

### Part A

Write a function called `nweekdays` that takes an argument called `date` and calculates the number of weekdays between January 1, 2023 and `date`. Your function should not use any built-in Python or pandas functions to accomplish this, but you can use `pd.bdate_range()` to check your answer. 

Hint: there are a few ways you can do this. Here's my suggestion. Use `pd.date_range()` to create a Series of all dates between two given dates. Then write a `for` loop that goes through all dates and checks if its `.weekday` property. Weekdays are numbered 0 through 6, with 0 being Monday and 6 being Sunday.

Hint: To check your answer, use `pd.bdate_range()` which creates a range of only weekdays between two dates. The number of dates it creates should match the number your function returns.

### Part B

Import the data and make sure the `date` column is parsed as a date. Use the `.apply()` method to apply the function you wrote to every date in the `date` column. That will tell you the number of weekdays between January 1 and the last day of the given month. Use the `.diff()` method to calculate the number of weekdays in a given month.

### Part C

Use the number of days you calculated in Part B to calculate the average daily return for each month. Because your daily returns should be very small, I suggest plotting them as basis points (100 basis point = 1 percent). Plot as a bar chart. Don't forget to label your axes and give the plot a title.

