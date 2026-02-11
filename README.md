# Pharmacy-Billing-System
# Pharmacy Billing System - Only Python

medicines = {
    "Paracetamol": {"price": 20, "stock": 50},
    "Cetrizine": {"price": 10, "stock": 30},
    "Amoxicillin": {"price": 50, "stock": 20},
    "Pan40": {"price": 30, "stock": 40},
    "Rantac": {"price": 5, "stock": 10}
}

def show_medicines():
    print("\n Available Medicines")
    print("Medicine \t Price \t Stock")
    print("-" * 30)
    for name, details in medicines.items():
       print(f"{name:<15}{details['price']:>6}{details['stock']:>6}")



def add_medicine():
    name = input("Enter medicine name: ")
    price = int(input("Enter price: "))
    stock = int(input("Enter stock: "))
    medicines[name] = {"price": price, "stock": stock}
    print("Medicine added successfully!")

def search_medicine():
    name = input("Enter medicine name to search: ")
    if name in medicines:
        print(f"{name} - Price: ₹{medicines[name]['price']}, Stock: {medicines[name]['stock']}")
    else:
        print("Medicine not found!")

def update_price():
    name = input("Enter medicine name: ")
    if name in medicines:
        new_price = int(input("Enter new price: "))
        medicines[name]["price"] = new_price
        print("Price updated successfully!")
    else:
        print("Medicine not found!")

def restock_medicine():
    name = input("Enter medicine name: ")
    if name in medicines:
        qty = int(input("Enter quantity to add: "))
        medicines[name]["stock"] += qty
        print("Stock updated successfully!")
    else:
        print("Medicine not found!")

def delete_medicine():
    name = input("Enter medicine name to delete: ")
    if name in medicines:
        del medicines[name]
        print("Medicine deleted successfully!")
    else:
        print("Medicine not found!")

def low_stock_alert():
    print("\nLow Stock Medicines (less than 10)")
    found = False
    for name, details in medicines.items():
        if details["stock"] < 10:
            print(f"{name} - Stock: {details['stock']}")
            found = True
    if not found:
        print("No low stock medicines")

def generate_bill():
    total = 0
    print("\n--- Billing ---")
    while True:
        show_medicines()
        med = input("Enter medicine name (or 'done' to finish): ")
        if med.lower() == "done":
            break
        if med in medicines:
            qty = int(input("Enter quantity: "))
            if qty <= medicines[med]["stock"]:
                cost = qty * medicines[med]["price"]
                total += cost
                medicines[med]["stock"] -= qty
                print(f"Added ₹{cost}")
            else:
                print("Insufficient stock!")
        else:
            print("Medicine not found!")
    print("\nTotal Bill Amount: ₹", total)

def main():
    while True:
        print("\n--- Pharmacy Billing System ---")
        print("1. View Medicines")
        print("2. Add Medicine")
        print("3. Generate Bill")
        print("4. Search Medicine")
        print("5. Update Price")
        print("6. Restock Medicine")
        print("7. Delete Medicine")
        print("8. Low Stock Alert")
        print("9. Exit")
      choice = input("Enter your choice: ")
        if choice == "1":
            show_medicines()
        elif choice == "2":
            add_medicine()
        elif choice == "3":
            generate_bill()
        elif choice == "4":
            search_medicine()
        elif choice == "5":
            update_price()
        elif choice == "6":
            restock_medicine()
        elif choice == "7":
            delete_medicine()
        elif choice == "8":
            low_stock_alert()
        elif choice == "9":
            print("Thank you! Visit again 😊")
            break
        else:
            print("Invalid choice!")
main()
