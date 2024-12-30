def calculator():
    print("Welcome to the Simple Calculator!")
    print("Choose an operation:")
    print("1. Addition (+)")
    print("2. Subtraction (-)")
    print("3. Multiplication (*)")
    print("4. Division (/)")

    try:
        num1 = float(input("Enter the first number: "))
        num2 = float(input("Enter the second number: "))
        operation = input("Enter the operation (+, -, *, /): ").strip()

        if operation == '+':
            result = num1 + num2
            print(f"The result of {num1} + {num2} is {result}")
        elif operation == '-':
            result = num1 - num2
            print(f"The result of {num1} - {num2} is {result}")
        elif operation == '*':
            result = num1 * num2
            print(f"The result of {num1} * {num2} is {result}")
        elif operation == '/':
            if num2 != 0:
                result = num1 / num2
                print(f"The result of {num1} / {num2} is {result}")
            else:
                print("Error: Division by zero is not allowed.")
        else:
            print("Invalid operation. Please choose one of the following: +, -, *, /")

    except ValueError:
        print("Invalid input. Please enter numeric values.")

calculator()
