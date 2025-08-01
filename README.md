#making of a simple calculator
def calculator():
     num1 = float(input("Enter the first number: "))
     num2 = float(input("Enter the second number: "))

     print("choose an operation:" )
     print("1. Addition")
     print("2. Subtraction")
     print("3. Multiplication")
     print("4. Division")

     choice = int(input("enter your choice(1/2/3/4):"))

     if choice == 1:
         result = num1 + num2
         print(f"{num1} + {num2} = {result}")
     elif choice ==2:
         result = num1 - num2
         print(f"{num1} - {num2} = {result}")
     elif choice == 3:
         result = num1*num2
         print(f"{num1} * {num2} = {result}")
     elif choice ==4:
         if num2 !=0:
             result = num1/num2
             print(f"{num1} / {num2} = {result}")
         else:
              print("error: Division by zero is not allowed.")
     else :
        print("error: Invalid choice. ")
calculator()
# CODSFT
