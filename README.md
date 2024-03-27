#Class definition for the WarehouseTrackingSystem
class WarehouseTrackingSystem:
    def __init__(self):
        self.items = []  # Initialize the items list

    #Function to add a new item 
    def add_item(self, name, unique_id, quantity):
        item = {
            'name': name,
            'unique_id': unique_id,
            'quantity': quantity
        }
        self.items.append(item)

    #Function to Update Quantity using Unique ID
    def update_quantity(self, unique_id, new_quantity):
        for item in self.items:
            if item['unique_id'] == unique_id:
                item['quantity'] = max(0, new_quantity)

    #Function to display all items
    def display_items(self):
        if not self.items:
            print("No items in the warehouse.")
        else:
            print("Items in the warehouse:")
            for item in self.items:
                print(f"Name: {item['name']}, Unique ID: {item['unique_id']}, Quantity: {item['quantity']}")

    #Function to search for an item by name
    def search_item(self, name):
        found = False
        for item in self.items:
            if item['name'] == name:
                found = True
                print(f"Name: {item['name']}, Unique ID: {item['unique_id']}, Quantity: {item['quantity']}")
        if not found:
            print(f"No item with name '{name}' found.")

    #Adjust inventory by adding new stock and not subtracting
    def adjust_inventory(self, unique_id, adjustment_quantity):
        for item in self.items:
            if item['unique_id'] == unique_id:
                item['quantity'] = max(0, item['quantity'] + adjustment_quantity)

    #Function to present stock represent stocks that are 10 and below
    def low_stock_alert(self, threshold=10):
        low_stock_items = [item for item in self.items if item['quantity'] < threshold]
        if low_stock_items:
            print("Low stock alerts:")
            for item in low_stock_items:
                print(f"Name: {item['name']}, Unique ID: {item['unique_id']}, Quantity: {item['quantity']}")
        else:
            print("No low stock items found.")

    #Function to represent Total Quantity of stock
    def total_quantity(self):
        return sum(item['quantity'] for item in self.items)

# Main Function 
def main():
    warehouse = WarehouseTrackingSystem()

    while True:
        print("\nWarehouse Tracking System Menu:")
        print("1. Add Item")
        print("2. Update Quantity")
        print("3. Display Items")
        print("4. Search for Item")
        print("5. Adjust Inventory")
        print("6. Low Stock Alert")
        print("7. Total Quantity Calculation")
        print("8. Exit")

        choice = input("Enter your choice (1-8): ")

        if choice == '1':
            name = input("Enter item name: ")
            unique_id = input("Enter unique ID: ")
            quantity = int(input("Enter quantity: "))
            warehouse.add_item(name, unique_id, quantity)

        elif choice == '2':
            unique_id = input("Enter unique ID of the item to update: ")
            new_quantity = int(input("Enter new quantity: "))
            warehouse.update_quantity(unique_id, new_quantity)

        elif choice == '3':
            warehouse.display_items()

        elif choice == '4':
            name = input("Enter item name to search for: ")
            warehouse.search_item(name)

        elif choice == '5':
            unique_id = input("Enter unique ID of the item to adjust inventory: ")
            adjustment_quantity = int(input("Enter adjustment quantity: "))
            warehouse.adjust_inventory(unique_id, adjustment_quantity)

        elif choice == '6':
            warehouse.low_stock_alert()

        elif choice == '7':
            total_qty = warehouse.total_quantity()
            print(f"Total quantity of all items: {total_qty}")

        elif choice == '8':
            print("Exiting Warehouse Tracking System.")
            break

        else:
            print("Invalid choice. Please enter a valid option (1-8).")

if __name__ == "__main__":
    main()

