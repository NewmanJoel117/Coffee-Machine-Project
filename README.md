# Coffee Machine Program

## Overview
This Coffee Machine program is a simple command-line application that simulates the functionality of a coffee vending machine. It allows users to select from three types of coffee: espresso, latte, and cappuccino. The program manages resources, processes payments, and dispenses coffee while providing options to turn off the machine and display a report of resources and profits.

## Author
Onyedika Joel Chukwuka

## Features
- **Select Coffee**: Users can choose from espresso, latte, and cappuccino.
- **Resource Management**: The program checks if there are enough resources (water, milk, coffee) to make the selected coffee.
- **Payment Processing**: The program calculates the total amount of coins inserted by the user.
- **Transaction Handling**: It checks if the payment is sufficient and processes the transaction.
- **Dispense Coffee**: The program dispenses coffee and deducts the used resources.
- **Reports**: Users can request a report of the current resources and total profit.
- **Machine Control**: Users can turn off the machine.

## Code Explanation

### MENU and Resources
```python
MENU = {
    "espresso": {
        "ingredients": {
            "water": 50,
            "coffee": 18,
        },
        "cost": 1.5,
    },
    "latte": {
        "ingredients": {
            "water": 200,
            "milk": 150,
            "coffee": 24,
        },
        "cost": 2.5,
    },
    "cappuccino": {
        "ingredients": {
            "water": 250,
            "milk": 100,
            "coffee": 24,
        },
        "cost": 3.0,
    }
}

profit = 0
resources = {
    "water": 300,
    "milk": 200,
    "coffee": 100,
}
```
The `MENU` dictionary contains information about the available coffee types, their required ingredients, and costs. The `resources` dictionary keeps track of the available ingredients. The `profit` variable stores the total money earned.

### Check Resource Sufficiency
```python
def is_resource_sufficient(order_ingredients):
    """Returns True when order can be made, False if ingredients are insufficient."""
    for item in order_ingredients:
        if order_ingredients[item] >= resources[item]:
            print(f"Sorry there is not enough {item}.")
    return True
```
This function checks if there are enough ingredients to make the selected coffee. It returns `True` if resources are sufficient and prints a message if any ingredient is lacking.

### Process Coins
```python
def process_coins():
    """Returns the total calculated from coins inserted."""
    print("Please insert coins.")
    total = int(input("how many quarters?: ")) * 0.25
    total += int(input("how many dimes?: ")) * 0.1
    total += int(input("how many nickels?: ")) * 0.5
    total += int(input("how many pennies?: ")) * 0.01
    return total
```
This function calculates the total amount of money inserted by the user in coins (quarters, dimes, nickels, pennies).

### Transaction Success
```python
def is_transaction_successful(money_received, drink_cost):
    """Return True the payment is accepted, or False if money is insufficient."""
    if money_received >= drink_cost:
        change = round(money_received - drink_cost, 2)
        print(f"Here is ${change} in change.")
        global profit
        profit += drink_cost
        return True
    else:
        print("Sorry that's not enough money. Money refunded.")
        return False
```
This function checks if the inserted money is sufficient to cover the cost of the selected coffee. If yes, it processes the transaction, updates the profit, and returns change. If not, it refunds the money.

### Make Coffee
```python
def make_coffee(drink_name, order_ingredients):
    """Deduct the required ingredients from the resources."""
    for item in order_ingredients:
        resources[item] -= order_ingredients[item]
    print(f"Here is your {drink_name}☕️")
```
This function deducts the required ingredients from the resources and prints a message indicating that the coffee is ready.

### Main Program Loop
```python
is_on = True

while is_on:
    choice = input("What would you like? (espresso/latte/cappuccino): ")
    if choice == "off":
        is_on = False
    elif choice == "report":
        print(f"Water: {resources['water']}ml")
        print(f"Milk: {resources['milk']}ml")
        print(f"Coffee: {resources['coffee']}g")
        print(f"Money: ${profit}")
    else:
        drink = MENU[choice]
        if is_resource_sufficient(drink["ingredients"]):
            payment = process_coins()
            if is_transaction_successful(payment, drink["cost"]):
                make_coffee(choice, drink["ingredients"])
```
The main loop runs the coffee machine. It prompts the user to choose an action: turn off the machine, print a report, or select a type of coffee. Based on the user input, it performs the necessary operations such as checking resources, processing payments, and making coffee.

## Usage
1. Run the program.
2. Choose an action: `espresso`, `latte`, `cappuccino`, `report`, or `off`.
3. Follow the prompts to insert coins and complete the transaction.
4. Enjoy your coffee!
   
Feel free to drop your contributions.
