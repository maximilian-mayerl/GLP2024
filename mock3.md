# Probeprüfung 3


```csharp
namespace MockExam3 {
    class InventoryFullException : Exception {
        public InventoryFullException() { }
        public InventoryFullException(string message) : base(message) { }
        public InventoryFullException(string message, Exception innerException) : base(message, innerException) { }
    }

    enum ItemType {
        Normal,
        Equip,
        Key
    }

    class Item {
        public int Id { get; private set; }
        public string Name { get; private set; }
        public ItemType ItemType { get; private set; }

        public Item(int id, string name, ItemType itemType) {
            this.Id = id;
            this.Name = name;
            ItemType = itemType;
        }
    }

    class Inventory {
        private Dictionary<ItemType, List<Item>> items;
        private int itemCount;

        public int Capacity { get; private set; }

        public Inventory(int capacity) {
            this.items = new();
            this.Capacity = capacity;
            this.itemCount = 0;
        }

        public void AddItem(Item item) {
            // Throw exception if the inventory is already full.
            if (this.itemCount >= this.Capacity) {
                throw new InventoryFullException("The inventory is full");
            }

            // Create list of items for this ItemType if it
            // doesn't exist yet.
            if (!items.ContainsKey(item.ItemType)) {
                items[item.ItemType] = new List<Item>();
            }

            // Add item.
            items[item.ItemType].Add(item);
            this.itemCount++;
        }

        public void PrintItems() {
            // Loop over keys to get the different ItemTypes.
            foreach (ItemType type in items.Keys) {
                Console.WriteLine($"Items of type {type}:");

                // Loop over all item for the current type and print them.
                foreach (Item item in items[type]) {
                    Console.WriteLine($"    {item.Id}: {item.Name}");
                }
            }
        }
    }

    internal class Program {
        static void Main(string[] args) {
            // Create a new inventory with a capacity of 5.
            Inventory inventory = new Inventory(5);

            // Insert ten items into the inventory. Catch the InventoryFullException
            // that is thrown and print its message.
            try {
                inventory.AddItem(new Item(1, "Wood", ItemType.Normal));
                inventory.AddItem(new Item(2, $"Basic Sword", ItemType.Equip));
                inventory.AddItem(new Item(3, $"Basic Shield", ItemType.Equip));
                inventory.AddItem(new Item(4, $"Dungeon Key", ItemType.Key));
                inventory.AddItem(new Item(5, $"Enhanced Sword", ItemType.Equip));
                inventory.AddItem(new Item(6, $"Item #6", ItemType.Equip));
                inventory.AddItem(new Item(7, $"Item #7", ItemType.Normal));
                inventory.AddItem(new Item(8, $"Item #8", ItemType.Equip));
                inventory.AddItem(new Item(9, $"Item #9", ItemType.Key));
                inventory.AddItem(new Item(10, $"Item #10", ItemType.Normal));
            }
            catch (InventoryFullException ex) {
                Console.WriteLine(ex.Message);
            }

            // Print the current inventory.
            inventory.PrintItems();
        }
    }
}
```
