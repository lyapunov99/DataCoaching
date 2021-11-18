# PPG Minus One Calculations

This example uses the following data from a CCC to demonstrate PPG minus one calculations:

|Cohort|CohortSz|CohortSuccessNum |
|------| --------:| ---------------:|
|african am|5758|3686|
|asian|70512|58525|
|decline|2364|1939|
|filipinx|9652|7143|
|latinx|37660|25986|
|native am|708|510|
|pac islander|1175|823|
|white|26513|21476|

## read your data from a url (incomplete. Not integrated.)
(convert the input file from url to match input residing on personal computer) 

To read your data file from url, utilize the following code:

```python
#pandas - python data analysis (pda) library 
import pandas as pd

url = "http://dept.swccd.edu/bsmith/Files/input-deanza.csv"
df = pd.read_csv(url)         #indicate that the csv file doesn't have a header row

df.head(9)   #print first  9 lines
```

## read your data from your computer
If the file is on your computer, use the following:

```python
category_nm, cohort_sz, num_successful_cohort = [], [], []
#f = open("input-deanza.csv", 'r')

f = open("C:/Users/khots/Google Drive/SWC/Data Coach/Model calculations and reports/Code/Python/input-deanza.csv", 'r')    
#f = open("C:/Users/khots/Google Drive/SWC/Data Coach/Model calculations and reports/Code/Python/input.csv", 'r')
next(f)  # skip the first line that contains column names

# read information from the above file, and store into arraylists
for line in f.readlines():
    fields = line.split(',')                        # e.g., returns ['african am', '5758', '3686\n']
    category_nm.append((fields[0]))                 # appends 'african am' to an array list
    cohort_sz.append(int(fields[1]))                # appends 5758 to an array list
    num_successful_cohort.append(int(fields[2]))    # appends 3686 to an array list
f.close()
```


## print the cohorts under consideration

```python
l=[]
for x in category_nm:
    l.append(x)
s = ' '.join(l)
print('The cohorts read in are: \n', s)
```
## perform the essential calculations:

```python
successList = []
print("\n", "       PPG minus one values:")
for i in range(len(category_nm) ):
    categSuccessRate = num_successful_cohort[i] / cohort_sz[i]     # success rate for a cohort
    successList.append(categSuccessRate)
    ppg_minus_one_success = (cohort_total_successes - num_successful_cohort[i]) / (cohort_total_size -  cohort_sz[i])

    ppgOut = "{:>8.1f}".format((categSuccessRate - ppg_minus_one_success) * 100)
    print("{:>18}".format(category_nm[i]), ": ", ppgOut,"%")
```
    
