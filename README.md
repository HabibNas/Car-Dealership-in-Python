# Car-Dealership-in-Python
#APCSP Project
#This code utilizes a json structured file to display any of the cars in the
#inventory
#It also adds and can remove employees from the dealership
#The aim of the project is to write out a simple car dealership management
#system where you can add, and remove, employees & cars alike

import json
class Car:
def __init__(self, brand, model, year, cost):
self.brand = brand
self.model = model
self.year = year
self.cost = cost
self.available = True
def __str__(self):
availability = "Available" if self.available else "Not Available"
return f"{self.year} {self.brand} {self.model}, cost: {self.cost},
{availability}"
def set_availability(self, available):
self.available = available
class Employee:
def __init__(self, name, employee_id):
self.name = name
self.employee_id = employee_id
def __str__(self):
return f"{self.employee_id}: {self.name}"
# Define the car and employee lists.
cars = []
employees = []
# Add a car to the inventory
def add_car(brand, model, year, cost):
car = Car(brand, model, year, cost)
cars.append(car)
# Write updated inventory to the json file
with open('inventory.json', 'w') as f:
json.dump([car.__dict__ for car in cars], f)
print(f"Added {year} {brand} {model} to inventory with cost {cost}")
# Remove a car from the inventory
def remove_car(brand, model, year):
for car in cars:
if car.brand == brand and car.model == model and car.year == year:
cars.remove(car)
# Write updated inventory to file
with open('inventory.json', 'w') as f:
json.dump([car.__dict__ for car in cars], f)
print(f"Removed {year} {brand} {model} from inventory")
return
print(f"{year} {brand} {model} not found in inventory")
# Display a car from the inventory
def display_cars():
for car in cars:
print(car)
# Add an employee
def add_employee(name, employee_id):
employee = Employee(name, employee_id)
employees.append(employee)
# Write updated employee list to file
with open('employees.json', 'w') as f:
json.dump([employee.__dict__ for employee in employees], f)
print(f"Added {name} to employees with ID {employee_id}")
# Remove an employee
def remove_employee(employee_id):
for employee in employees:
if employee.employee_id == employee_id:
employees.remove(employee)
# Write updated employee list to file
with open('employees.json', 'w') as f:
json.dump([employee.__dict__ for employee in employees], f)
print(f"Removed {employee.name} from employees")
return
print(f"Employee with ID {employee_id} not found")
# Display employee list
def display_employees():
for employee in employees:
print(employee)
while True:
print("\nCar Dealership Management System")
print("1. Add car to inventory")
print("2. Remove car from inventory")
print("3. Display car inventory")
print("4. Add employee")
print("5. Remove employee")
print("6. Display employee list")
print("7. Quit")
choice = input("Enter choice (1-7): ")
if choice == "1":
brand = input("Enter brand: ")
model = input("Enter model: ")
year = int(input("Enter year: "))
cost = float(input("Enter cost: "))
add_car(brand, model, year, cost)
elif choice == "2":
brand = input("Enter brand: ")
model = input("Enter model: ")
year = int(input("Enter year: "))
remove_car(brand, model, year)
elif choice == "3":
display_cars()
elif choice == "4":
name = input("Enter employee name: ")
employee_id = int(input("Enter employee ID: "))
add_employee(name, employee_id)
elif choice == "5":
employee_id = int(input("Enter employee ID: "))
remove_employee(employee_id)
elif choice == "6":
display_employees()
elif choice == "7":
# Generate report of the cars that are in the inventory
available_cars = [car for car in cars if car.available]
with open('available_cars.txt', 'w') as f:
for car in available_cars:
f.write(str(car) + "\n")
print(f"Report generated: {len(available_cars)} available cars written to
available_cars.txt")
break
else:
print("Invalid choice. Please enter a number from 1-7.")
