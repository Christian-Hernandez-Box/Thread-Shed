# Thread-Shed

You’ve recently been hired as a cashier at the local sewing hobby shop, Thread Shed. Some of your daily responsibilities involve tallying the number of sales made during the day, calculating the total amount of money made, and keeping track of the names of the customers.

Unfortunately, the Thread Shed has an extremely outdated register system and stores all of the transaction information in one huge, unwieldy string called daily_sales.

All day, for each transaction, the name of the customer, amount spent, types of thread purchased, and date of sale are all recorded in this same string. Watch me clean up each transaction and store all the information in easier-to-access lists using my newly acquired Python skills.

```
# Sales Data for the Day - Omitted

#---------------------------------------------------------------------------

# String Clean-up Before Splitting Into Individual Transactions
daily_sales_replaced = daily_sales.replace(";,;", "+")

# Splitting String Into Individual Transactions
daily_transactions = daily_sales_replaced.split(",")

# Splitting Individual Transaction Into A List Of Its Own
daily_transactions_split = []
for transaction in daily_transactions:
  daily_transactions_split.append(transaction.split("+"))

# Cleaning Up Data i.e. Whitespace & "\n"
transactions_clean = []
for test in daily_transactions_split:
  transaction_clean = []
  for data_point in test:
    transaction_clean.append(data_point.replace("\n", "").strip(" "))
  transactions_clean.append(transaction_clean)
    
# Collecting Individual Data For Each Transaction
customers = []
sales = []
thread_sold = []

for transaction in transactions_clean:
  customers.append(transaction[0])
  sales.append(transaction[1])
  thread_sold.append(transaction[2])

# Calculating Total $ Value Of Sales
total_sales = 0
for sale in sales:
  total_sales += float(sale.strip("$"))
  
# Calculating How Many Of Each Color Thread Was sold
thread_sold_split = []

for sale in thread_sold:
  for color in sale.split("&"):
    thread_sold_split.append(color)

def color_count(color):
  color_count = 0
  for thread_color in thread_sold_split:
    if thread_color == color:
      color_count += 1
  return color_count

# Output w/ # of Threads Sold For Given Color
colors = ['red', 'yellow', 'green', 'white', 'black', 'blue', 'purple']

for color in colors:
  print("Thread Shed sold {} threads of {} thread today".format(color_count(color), color))
```
