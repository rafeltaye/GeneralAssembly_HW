'''
Python Homework with Chipotle data
https://github.com/TheUpshot/chipotle
'''

'''
BASIC LEVEL
PART 1: Read in the data with csv.reader() and store it in a list of lists called 'data'.
Hint: This is a TSV file, and csv.reader() needs to be told how to handle it.
      https://docs.python.org/2/library/csv.html
'''
import csv
with open('chipotle.tsv', 'rU') as f:
    data = [row for row in csv.reader(f,delimiter='\t')]


'''
BASIC LEVEL
PART 2: Separate the header and data into two different lists.
'''
header= data[0]
data=data[1:]


'''
INTERMEDIATE LEVEL
PART 3: Calculate the average price of an order.
Hint: Examine the data to see if the 'quantity' column is relevant to this calculation.
Hint: Think carefully about the simplest way to do this!
'''
orders=[]
prices=[]
for row in data:
    orders.append(row[0])
    prices.append(float(row[4][1:-1]))
num_order=len(set(orders))
avg_price=round((sum(prices))/ (num_order),2)
    


'''
INTERMEDIATE LEVEL
PART 4: Create a list (or set) of all unique sodas and soft drinks that they sell.
Note: Just look for 'Canned Soda' and 'Canned Soft Drink', and ignore other drinks like 'Izze'.
'''
#creat an empty list called soda.
#look for the string "Canned" in the second collumn and append the corresponding
#string in the third collumn to sada list taking just the name of the soda
#then just take the unique names and put it in a new list 

soda=[]
for row in data:
    if "Canned" in row[2]:
        soda.append(row[3][1:-1])
uniq_soda=set(soda)
        


'''
ADVANCED LEVEL
PART 5: Calculate the average number of toppings per burrito.
Note: Let's ignore the 'quantity' column to simplify this task.
Hint: Think carefully about the easiest way to count the number of toppings!
'''
#initialize burrito count and topping count to 0
#if order name has string "Burrito", add 1 to the burrito count to get number of burritos
#and set count number of toppings by counting commas and adding 1 to calculate number of toppings per row for all rows
#then calculate the average by dividing topping count by burrito count 
 
burrito_count=0
topping_count=0
for row in data:
    if "Burrito" in row[2]:
        burrito_count= float(burrito_count +1) 
        topping_count=topping_count+(row[3].count(",") +1)
topping_avg= round(topping_count/(burrito_count),3)


'''
ADVANCED LEVEL
PART 6: Create a dictionary in which the keys represent chip orders and
  the values represent the total number of orders.
Expected output: {'Chips and Roasted Chili-Corn Salsa': 18, ... }
Note: Please take the 'quantity' column into account!
Optional: Learn how to use 'defaultdict' to simplify your code.
'''
#creat an empty dictionary called chip
#run a for loop to find the orders that has "Chips" in them
#from those lists, if the order name is not in the dictionary "chip" then add the ordername as the key and total order as the value
#if the order name already exist, just add the order quanity to the existing value 

#ANSWER OPTION 1

chip={}
for row in data:
    if "Chips" in row[2]:
        if row[2] not in chip:
            chip[row[2]]= int(row[1]) #create type_of_chips in dict with initial value of order
        else:
            chip[row[2]]+= int(row[1])
   
#ANSWER OPTION 2

from collections import defaultdict

chip=defaultdict(int) #the value of the dict is integers
for row in data:
    if "Chips" in row[2]:
        chip[row[2]]+= int(row[1])
        
    

'''
BONUS: Think of a question about this data that interests you, and then answer it!
'''
