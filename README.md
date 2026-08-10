Conversation with Gemini

# 🎮 Unity Inventory System


A robust, SOLID-principle-based inventory system for Unity games featuring drag-and-drop functionality, item stacking, splitting, and merging capabilities.


## ✨ Features


- 🖱️ **Drag & Drop Interface** - Intuitive mouse-based item management

- 📦 **Item Stacking** - Automatic stacking of identical items up to max stack size

- ✂️ **Item Splitting** - Right-click to split item stacks in half

- 🔄 **Item Merging** - Combine compatible items automatically

- 🔁 **Item Swapping** - Swap items between slots seamlessly

- 💡 **Tooltip System** - Hover tooltips with item information

- 🏗️ **SOLID Architecture** - Clean, maintainable, and extensible code structure

- 🔧 **ScriptableObject Configuration** - Easy customization without code changes

- 🌐 **Network Ready** - Built with Unity Netcode integration in mind


## 🛠️ Dependencies


https://github.com/user-attachments/assets/dfa65463-711f-4976-9297-323d5d0a7070


### Unity Version

- **Unity 2022.3 LTS** or higher


### Required Packages

```json

{

  "com.unity.textmeshpro": "3.0.6",

  "com.unity.netcode.gameobjects": "1.7.1" 

}

```


### Installation via Package Manager

1. Open Unity Package Manager (`Window > Package Manager`)

2. Install **TextMeshPro** from Unity Registry

3. Install **Netcode for GameObjects** from Unity Registry


## 📁 Project Structure


```

Assets/

├── 📂 Scripts/

│   ├── 📂 Core/

│   │   ├── 🔧 ItemDefinition.cs

│   │   ├── 🔧 ItemContainerConfig.cs

│   │   └── 🔧 ItemContainerSlotUIConfig.cs

│   ├── 📂 Inventory/

│   │   ├── 📦 ItemContainer.cs

│   │   ├── 🎯 ItemContainerItemUI.cs

│   │   └── 🎪 ItemContainerSlotUI.cs

│   ├── 📂 DragSystem/

│   │   ├── 🎮 ItemDragManager.cs

│   │   ├── 🎯 InventoryInputHandler.cs

│   │   ├── 🔧 ItemDragService.cs

│   │   ├── ⚙️ ItemOperationService.cs

│   │   └── 🎨 DragVisualizer.cs

│   └── 📂 UI/

│       └── 💬 TooltipUI.cs

├── 📂 Prefabs/

│   ├── 📦 InventoryContainer.prefab

│   ├── 🎪 InventorySlot.prefab

│   └── 🎮 ItemDragManager.prefab

└── 📂 ScriptableObjects/

    ├── 📂 Items/

    │   ├── ⚔️ Sword.asset

    │   ├── 🛡️ Shield.asset

    │   └── 🧪 Potion.asset

    └── 📂 Configs/

        ├── 🔧 DefaultContainerConfig.asset

        └── 🎨 DefaultSlotConfig.asset

```


## 🚀 Quick Start


### 1. Setup Item Definitions

```csharp

// Create items via: Assets > Create > Inventory System > Item

// Configure: ID, Name, Description, Icon, Max Stack Size, Prefab

```


### 2. Create Inventory Container

```csharp

// 1. Create empty GameObject

// 2. Add ItemContainer component

// 3. Assign ItemContainerConfig

// 4. Add ItemContainerSlotUI components as children

// 5. Assign slots to the Slots list in ItemContainer

```


### 3. Setup Drag Manager

```csharp

// 1. Create ItemDragManager prefab in scene

// 2. Assign DragVisualizer component

// 3. Configure drag visual elements (Image, Text)

```


### 4. Configure UI Elements

```csharp

// Each slot needs:

// - ItemContainerSlotUI component

// - UI Image for slot background

// - UI Image for held item display

// - TextMeshProUGUI for amount display

```


## 🎯 Usage Examples


### Adding Items to Inventory

```csharp

public class InventoryManager : MonoBehaviour

{

    [SerializeField] private ItemContainer playerInventory;

    [SerializeField] private ItemDefinition swordItem;

    

    void Start()

    {

        // Add 5 swords to inventory

        playerInventory.TryAddItem(swordItem, 5);

    }

}

```


### Custom Item Operations

```csharp

public class CustomItemOperations : MonoBehaviour, IItemOperationService

{

    public bool TryMoveItem(ItemContainerItemUI item, ItemContainerSlotUI targetSlot)

    {

        // Add custom logic (e.g., equipment restrictions)

        if (item.ItemDefinition.ItemType == ItemType.Weapon && targetSlot.SlotType != SlotType.WeaponSlot)

            return false;

            

        return defaultOperationService.TryMoveItem(item, targetSlot);

    }

    

    // Implement other interface methods...

}

```


## 🎨 Customization


### Item Configuration

Create new items through the ScriptableObject menu:

- **Right-click in Project** → **Create** → **Inventory System** → **Item**


### Visual Customization

- **Slot Icons**: Configure active/passive slot sprites in `ItemContainerSlotUIConfig`

- **Drag Visuals**: Customize drag appearance in `DragVisualizer` component

- **Tooltips**: Modify `TooltipUI` for custom tooltip styles


### Extending Functionality

```csharp

// Add new item operations

public class EnchantmentService : IItemOperationService

{

    public bool TryEnchantItem(ItemContainerItemUI item, EnchantmentType enchantment)

    {

        // Custom enchantment logic

        return true;

    }

}

```


## 🏗️ Architecture Overview


### SOLID Principles Implementation


- **🔧 Single Responsibility**: Each class has one clear purpose

- **📖 Open/Closed**: Easy to extend without modifying existing code

- **🔄 Liskov Substitution**: Interfaces can be swapped seamlessly

- **🎯 Interface Segregation**: Focused, specific interfaces

- **🔗 Dependency Inversion**: Depends on abstractions, not concrete classes


### Key Components


| Component | Responsibility |

|-----------|---------------|

| `ItemDragService` | 🎯 Manages drag state |

| `ItemOperationService` | ⚙️ Handles item operations |

| `DragVisualizer` | 🎨 Visual drag representation |

| `InventoryInputHandler` | 🎮 Input processing |

| `ItemDragManager` | 🎪 Facade coordinator |


## 🧪 Testing


### Unit Testing Setup

```csharp

[Test]

public void TestItemMerging()

{

    // Arrange

    var mockDragService = new Mock<IItemDragService>();

    var operationService = new ItemOperationService();

    

    // Act & Assert

    Assert.IsTrue(operationService.TryMergeItems(item1, slot));

}

```


## 🤝 Contributing


1. 🍴 Fork the repository

2. 🌟 Create a feature branch (`git checkout -b feature/amazing-feature`)

3. 💾 Commit changes (`git commit -m 'Add amazing feature'`)

4. 📤 Push to branch (`git push origin feature/amazing-feature`)

5. 🔄 Open a Pull Request


## 📋 Requirements


- ✅ Unity 2022.3 LTS+

- ✅ TextMeshPro

- ✅ Unity Netcode for GameObjects (optional)

- ✅ C# 9.0+ support


## 📝 License


This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.


## 🙏 Acknowledgments


- 🎮 Unity Technologies for the excellent game engine

- 👥 Game development community for inspiration and best practices

- 📚 Clean Code principles by Robert C. Martin


## 📞 Support


- 🐛 **Bug Reports**: Open an issue with detailed reproduction steps

- 💡 **Feature Requests**: Open an issue with [FEATURE REQUEST] prefix

- 💬 **Questions**: Use GitHub Discussions for general questions


---


⭐ **Star this repository if you find it helpful!** ⭐


Made with ❤️ for the Unity community

remove emojis, make it look like wrote by human, delete this candy sections like made with love etc. RETURN IN EASY TO COPY FORMAT
Unity Inventory System

A SOLID-principle-based inventory system for Unity games featuring drag-and-drop functionality, item stacking, splitting, and merging capabilities.
Features

    Mouse-based drag-and-drop item management

    Automatic stacking of identical items up to maximum stack size

    Right-click stack splitting

    Automatic item merging and slot swapping

    Hover tooltips for item details

    Modular architecture built using ScriptableObjects

    Unity Netcode integration ready

Dependencies
Unity Version

    Unity 2022.3 LTS or higher

Required Packages

    TextMeshPro (com.unity.textmeshpro: 3.0.6)

    Netcode for GameObjects (com.unity.netcode.gameobjects: 1.7.1)

Installation via Package Manager

    Open Unity Package Manager (Window > Package Manager).

    Install TextMeshPro from the Unity Registry.

    Install Netcode for GameObjects from the Unity Registry.

Project Structure

Assets/
├── Scripts/
│   ├── Core/
│   │   ├── ItemDefinition.cs
│   │   ├── ItemContainerConfig.cs
│   │   └── ItemContainerSlotUIConfig.cs
│   ├── Inventory/
│   │   ├── ItemContainer.cs
│   │   ├── ItemContainerItemUI.cs
│   │   └── ItemContainerSlotUI.cs
│   ├── DragSystem/
│   │   ├── ItemDragManager.cs
│   │   ├── InventoryInputHandler.cs
│   │   ├── ItemDragService.cs
│   │   ├── ItemOperationService.cs
│   │   └── DragVisualizer.cs
│   └── UI/
│       └── TooltipUI.cs
├── Prefabs/
│   ├── InventoryContainer.prefab
│   ├── InventorySlot.prefab
│   └── ItemDragManager.prefab
└── ScriptableObjects/
    ├── Items/
    │   ├── Sword.asset
    │   ├── Shield.asset
    │   └── Potion.asset
    └── Configs/
        ├── DefaultContainerConfig.asset
        └── DefaultSlotConfig.asset

Quick Start
1. Setup Item Definitions

Create item assets using Assets > Create > Inventory System > Item. Configure the ID, Name, Description, Icon, Max Stack Size, and Prefab.
2. Create Inventory Container

    Create an empty GameObject in your scene.

    Add the ItemContainer component.

    Assign an ItemContainerConfig.

    Add ItemContainerSlotUI components as child objects.

    Reference the slots inside the Slots list on the ItemContainer.

3. Setup Drag Manager

    Add the ItemDragManager prefab to the scene.

    Attach the DragVisualizer component.

    Assign the visual UI elements (Image, Text).

4. Configure UI Elements

Each slot requires:

    ItemContainerSlotUI component

    Background Image

    Item Display Image

    TextMeshProUGUI element for stack counts

Usage Examples
Adding Items to Inventory
C#

public class InventoryManager : MonoBehaviour
{
    [SerializeField] private ItemContainer playerInventory;
    [SerializeField] private ItemDefinition swordItem;
    
    private void Start()
    {
        playerInventory.TryAddItem(swordItem, 5);
    }
}

Custom Item Operations
C#

public class CustomItemOperations : MonoBehaviour, IItemOperationService
{
    public bool TryMoveItem(ItemContainerItemUI item, ItemContainerSlotUI targetSlot)
    {
        if (item.ItemDefinition.ItemType == ItemType.Weapon && targetSlot.SlotType != SlotType.WeaponSlot)
        {
            return false;
        }
            
        return defaultOperationService.TryMoveItem(item, targetSlot);
    }
}

Customization

    Item Definitions: Right-click in Project view -> Create > Inventory System > Item.

    Slot Visuals: Configure active/passive slot sprites in ItemContainerSlotUIConfig.

    Drag UI: Customize the drag layer appearance in DragVisualizer.

    Tooltips: Extend TooltipUI to adjust tooltip layouts or content.

Architecture Overview

The system strictly follows SOLID principles:

    Single Responsibility: Individual services handle input, drag state, visuals, and container logic separately.

    Open/Closed & Dependency Inversion: Behaviors rely on interfaces (IItemOperationService, IItemDragService), allowing core logic changes without modifying existing components.

Component	Responsibility
ItemDragService	Manages drag state
ItemOperationService	Handles item logic and stack operations
DragVisualizer	Handles visual representation during dragging
InventoryInputHandler	Processes input events
ItemDragManager	Acts as the primary facade coordinator
Testing
C#

[Test]
public void TestItemMerging()
{
    var mockDragService = new Mock<IItemDragService>();
    var operationService = new ItemOperationService();
    
    Assert.IsTrue(operationService.TryMergeItems(item1, slot));
}

Requirements

    Unity 2022.3 LTS or higher

    TextMeshPro

    Unity Netcode for GameObjects (optional)

    C# 9.0+ support

License

This project is licensed under the MIT License.

give me this readme in single mardkown file
Python

md_content = """# Unity Inventory System

A SOLID-principle-based inventory system for Unity games featuring drag-and-drop functionality, item stacking, splitting, and merging capabilities.

## Features

- Mouse-based drag-and-drop item management
- Automatic stacking of identical items up to maximum stack size
- Right-click stack splitting
- Automatic item merging and slot swapping
- Hover tooltips for item details
- Modular architecture built using ScriptableObjects
- Unity Netcode integration ready

## Dependencies

### Unity Version
- Unity 2022.3 LTS or higher

### Required Packages
- TextMeshPro (`com.unity.textmeshpro`: `3.0.6`)
- Netcode for GameObjects (`com.unity.netcode.gameobjects`: `1.7.1`)

### Installation via Package Manager
1. Open Unity Package Manager (`Window > Package Manager`).
2. Install TextMeshPro from the Unity Registry.
3. Install Netcode for GameObjects from the Unity Registry.

## Project Structure

Assets/
├── Scripts/
│   ├── Core/
│   │   ├── ItemDefinition.cs
│   │   ├── ItemContainerConfig.cs
│   │   └── ItemContainerSlotUIConfig.cs
│   ├── Inventory/
│   │   ├── ItemContainer.cs
│   │   ├── ItemContainerItemUI.cs
│   │   └── ItemContainerSlotUI.cs
│   ├── DragSystem/
│   │   ├── ItemDragManager.cs
│   │   ├── InventoryInputHandler.cs
│   │   ├── ItemDragService.cs
│   │   ├── ItemOperationService.cs
│   │   └── DragVisualizer.cs
│   └── UI/
│       └── TooltipUI.cs
├── Prefabs/
│   ├── InventoryContainer.prefab
│   ├── InventorySlot.prefab
│   └── ItemDragManager.prefab
└── ScriptableObjects/
├── Items/
│   ├── Sword.asset
│   ├── Shield.asset
│   └── Potion.asset
└── Configs/
├── DefaultContainerConfig.asset
└── DefaultSlotConfig.asset


## Quick Start

### 1. Setup Item Definitions
Create item assets using `Assets > Create > Inventory System > Item`. Configure the ID, Name, Description, Icon, Max Stack Size, and Prefab.

### 2. Create Inventory Container
1. Create an empty GameObject in your scene.
2. Add the `ItemContainer` component.
3. Assign an `ItemContainerConfig`.
4. Add `ItemContainerSlotUI` components as child objects.
5. Reference the slots inside the `Slots` list on the `ItemContainer`.

### 3. Setup Drag Manager
1. Add the `ItemDragManager` prefab to the scene.
2. Attach the `DragVisualizer` component.
3. Assign the visual UI elements (Image, Text).

### 4. Configure UI Elements
Each slot requires:
- `ItemContainerSlotUI` component
- Background Image
- Item Display Image
- TextMeshProUGUI element for stack counts

## Usage Examples

### Adding Items to Inventory
```csharp
public class InventoryManager : MonoBehaviour
{
    [SerializeField] private ItemContainer playerInventory;
    [SerializeField] private ItemDefinition swordItem;
    
    private void Start()
    {
        playerInventory.TryAddItem(swordItem, 5);
    }
}

Custom Item Operations
C#

public class CustomItemOperations : MonoBehaviour, IItemOperationService
{
    public bool TryMoveItem(ItemContainerItemUI item, ItemContainerSlotUI targetSlot)
    {
        if (item.ItemDefinition.ItemType == ItemType.Weapon && targetSlot.SlotType != SlotType.WeaponSlot)
        {
            return false;
        }
            
        return defaultOperationService.TryMoveItem(item, targetSlot);
    }
}

Customization

    Item Definitions: Right-click in Project view -> Create > Inventory System > Item.

    Slot Visuals: Configure active/passive slot sprites in ItemContainerSlotUIConfig.

    Drag UI: Customize the drag layer appearance in DragVisualizer.

    Tooltips: Extend TooltipUI to adjust tooltip layouts or content.

Architecture Overview

The system strictly follows SOLID principles:

    Single Responsibility: Individual services handle input, drag state, visuals, and container logic separately.

    Open/Closed & Dependency Inversion: Behaviors rely on interfaces (IItemOperationService, IItemDragService), allowing core logic changes without modifying existing components.

Component	Responsibility
ItemDragService	Manages drag state
ItemOperationService	Handles item logic and stack operations
DragVisualizer	Handles visual representation during dragging
InventoryInputHandler	Processes input events
ItemDragManager	Acts as the primary facade coordinator
Testing
C#

[Test]
public void TestItemMerging()
{
    var mockDragService = new Mock<IItemDragService>();
    var operationService = new ItemOperationService();
    
    Assert.IsTrue(operationService.TryMergeItems(item1, slot));
}

Requirements

    Unity 2022.3 LTS or higher

    TextMeshPro

    Unity Netcode for GameObjects (optional)

    C# 9.0+ support

License

This project is licensed under the MIT License.
"""

file_path = "README.md"
with open(file_path, "w", encoding="utf-8") as f:
f.write(md_content)

print(f"Generated {file_path}")


```text?code_stdout&code_event_index=1
Generated README.md

Your Markdown file is ready
MD icon
README
 MD 

Here is the markdown content in a copyable block:
Markdown

# Unity Inventory System

A SOLID-principle-based inventory system for Unity games featuring drag-and-drop functionality, item stacking, splitting, and merging capabilities.

## Features

- Mouse-based drag-and-drop item management
- Automatic stacking of identical items up to maximum stack size
- Right-click stack splitting
- Automatic item merging and slot swapping
- Hover tooltips for item details
- Modular architecture built using ScriptableObjects
- Unity Netcode integration ready

## Dependencies

### Unity Version
- Unity 2022.3 LTS or higher

### Required Packages
- TextMeshPro (`com.unity.textmeshpro`: `3.0.6`)
- Netcode for GameObjects (`com.unity.netcode.gameobjects`: `1.7.1`)

### Installation via Package Manager
1. Open Unity Package Manager (`Window > Package Manager`).
2. Install TextMeshPro from the Unity Registry.
3. Install Netcode for GameObjects from the Unity Registry.

## Project Structure

Assets/
├── Scripts/
│   ├── Core/
│   │   ├── ItemDefinition.cs
│   │   ├── ItemContainerConfig.cs
│   │   └── ItemContainerSlotUIConfig.cs
│   ├── Inventory/
│   │   ├── ItemContainer.cs
│   │   ├── ItemContainerItemUI.cs
│   │   └── ItemContainerSlotUI.cs
│   ├── DragSystem/
│   │   ├── ItemDragManager.cs
│   │   ├── InventoryInputHandler.cs
│   │   ├── ItemDragService.cs
│   │   ├── ItemOperationService.cs
│   │   └── DragVisualizer.cs
│   └── UI/
│       └── TooltipUI.cs
├── Prefabs/
│   ├── InventoryContainer.prefab
│   ├── InventorySlot.prefab
│   └── ItemDragManager.prefab
└── ScriptableObjects/
├── Items/
│   ├── Sword.asset
│   ├── Shield.asset
│   └── Potion.asset
└── Configs/
├── DefaultContainerConfig.asset
└── DefaultSlotConfig.asset


## Quick Start

### 1. Setup Item Definitions
Create item assets using `Assets > Create > Inventory System > Item`. Configure the ID, Name, Description, Icon, Max Stack Size, and Prefab.

### 2. Create Inventory Container
1. Create an empty GameObject in your scene.
2. Add the `ItemContainer` component.
3. Assign an `ItemContainerConfig`.
4. Add `ItemContainerSlotUI` components as child objects.
5. Reference the slots inside the `Slots` list on the `ItemContainer`.

### 3. Setup Drag Manager
1. Add the `ItemDragManager` prefab to the scene.
2. Attach the `DragVisualizer` component.
3. Assign the visual UI elements (Image, Text).

### 4. Configure UI Elements
Each slot requires:
- `ItemContainerSlotUI` component
- Background Image
- Item Display Image
- TextMeshProUGUI element for stack counts

## Usage Examples

### Adding Items to Inventory
```csharp
public class InventoryManager : MonoBehaviour
{
    [SerializeField] private ItemContainer playerInventory;
    [SerializeField] private ItemDefinition swordItem;
    
    private void Start()
    {
        playerInventory.TryAddItem(swordItem, 5);
    }
}

Custom Item Operations
C#

public class CustomItemOperations : MonoBehaviour, IItemOperationService
{
    public bool TryMoveItem(ItemContainerItemUI item, ItemContainerSlotUI targetSlot)
    {
        if (item.ItemDefinition.ItemType == ItemType.Weapon && targetSlot.SlotType != SlotType.WeaponSlot)
        {
            return false;
        }
            
        return defaultOperationService.TryMoveItem(item, targetSlot);
    }
}

Customization

    Item Definitions: Right-click in Project view -> Create > Inventory System > Item.

    Slot Visuals: Configure active/passive slot sprites in ItemContainerSlotUIConfig.

    Drag UI: Customize the drag layer appearance in DragVisualizer.

    Tooltips: Extend TooltipUI to adjust tooltip layouts or content.

Architecture Overview

The system strictly follows SOLID principles:

    Single Responsibility: Individual services handle input, drag state, visuals, and container logic separately.

    Open/Closed & Dependency Inversion: Behaviors rely on interfaces (IItemOperationService, IItemDragService), allowing core logic changes without modifying existing components.

Component	Responsibility
ItemDragService	Manages drag state
ItemOperationService	Handles item logic and stack operations
DragVisualizer	Handles visual representation during dragging
InventoryInputHandler	Processes input events
ItemDragManager	Acts as the primary facade coordinator
Testing
C#

[Test]
public void TestItemMerging()
{
    var mockDragService = new Mock<IItemDragService>();
    var operationService = new ItemOperationService();
    
    Assert.IsTrue(operationService.TryMergeItems(item1, slot));
}

Requirements

    Unity 2022.3 LTS or higher

    TextMeshPro

    Unity Netcode for GameObjects (optional)

    C# 9.0+ support

License

This project is licensed under the MIT License.


Gemini is AI and can make mistakes, including about people. Your privacy and GeminiOpens in a new window

# Unity Inventory System

A SOLID-principle-based inventory system for Unity games featuring drag-and-drop functionality, item stacking, splitting, and merging capabilities.

## Features

- Mouse-based drag-and-drop item management
- Automatic stacking of identical items up to maximum stack size
- Right-click stack splitting
- Automatic item merging and slot swapping
- Hover tooltips for item details
- Modular architecture built using ScriptableObjects
- Unity Netcode integration ready

## Dependencies

### Unity Version
- Unity 2022.3 LTS or higher

### Required Packages
- TextMeshPro (`com.unity.textmeshpro`: `3.0.6`)
- Netcode for GameObjects (`com.unity.netcode.gameobjects`: `1.7.1`)

### Installation via Package Manager
1. Open Unity Package Manager (`Window > Package Manager`).
2. Install TextMeshPro from the Unity Registry.
3. Install Netcode for GameObjects from the Unity Registry.

## Project Structure

```
Assets/
├── Scripts/
│   ├── Core/
│   │   ├── ItemDefinition.cs
│   │   ├── ItemContainerConfig.cs
│   │   └── ItemContainerSlotUIConfig.cs
│   ├── Inventory/
│   │   ├── ItemContainer.cs
│   │   ├── ItemContainerItemUI.cs
│   │   └── ItemContainerSlotUI.cs
│   ├── DragSystem/
│   │   ├── ItemDragManager.cs
│   │   ├── InventoryInputHandler.cs
│   │   ├── ItemDragService.cs
│   │   ├── ItemOperationService.cs
│   │   └── DragVisualizer.cs
│   └── UI/
│       └── TooltipUI.cs
├── Prefabs/
│   ├── InventoryContainer.prefab
│   ├── InventorySlot.prefab
│   └── ItemDragManager.prefab
└── ScriptableObjects/
    ├── Items/
    │   ├── Sword.asset
    │   ├── Shield.asset
    │   └── Potion.asset
    └── Configs/
        ├── DefaultContainerConfig.asset
        └── DefaultSlotConfig.asset
```

## Quick Start

### 1. Setup Item Definitions
Create item assets using `Assets > Create > Inventory System > Item`. Configure the ID, Name, Description, Icon, Max Stack Size, and Prefab.

### 2. Create Inventory Container
1. Create an empty GameObject in your scene.
2. Add the `ItemContainer` component.
3. Assign an `ItemContainerConfig`.
4. Add `ItemContainerSlotUI` components as child objects.
5. Reference the slots inside the `Slots` list on the `ItemContainer`.

### 3. Setup Drag Manager
1. Add the `ItemDragManager` prefab to the scene.
2. Attach the `DragVisualizer` component.
3. Assign the visual UI elements (Image, Text).

### 4. Configure UI Elements
Each slot requires:
- `ItemContainerSlotUI` component
- Background Image
- Item Display Image
- TextMeshProUGUI element for stack counts

## Usage Examples

### Adding Items to Inventory
```csharp
public class InventoryManager : MonoBehaviour
{
    [SerializeField] private ItemContainer playerInventory;
    [SerializeField] private ItemDefinition swordItem;
    
    private void Start()
    {
        playerInventory.TryAddItem(swordItem, 5);
    }
}
```

### Custom Item Operations
```csharp
public class CustomItemOperations : MonoBehaviour, IItemOperationService
{
    public bool TryMoveItem(ItemContainerItemUI item, ItemContainerSlotUI targetSlot)
    {
        if (item.ItemDefinition.ItemType == ItemType.Weapon && targetSlot.SlotType != SlotType.WeaponSlot)
        {
            return false;
        }
            
        return defaultOperationService.TryMoveItem(item, targetSlot);
    }
}
```

## Customization

- **Item Definitions:** Right-click in Project view -> `Create > Inventory System > Item`.
- **Slot Visuals:** Configure active/passive slot sprites in `ItemContainerSlotUIConfig`.
- **Drag UI:** Customize the drag layer appearance in `DragVisualizer`.
- **Tooltips:** Extend `TooltipUI` to adjust tooltip layouts or content.

## Architecture Overview

The system strictly follows SOLID principles:
- **Single Responsibility:** Individual services handle input, drag state, visuals, and container logic separately.
- **Open/Closed & Dependency Inversion:** Behaviors rely on interfaces (`IItemOperationService`, `IItemDragService`), allowing core logic changes without modifying existing components.

| Component | Responsibility |
|-----------|---------------|
| `ItemDragService` | Manages drag state |
| `ItemOperationService` | Handles item logic and stack operations |
| `DragVisualizer` | Handles visual representation during dragging |
| `InventoryInputHandler` | Processes input events |
| `ItemDragManager` | Acts as the primary facade coordinator |

## Testing

```csharp
[Test]
public void TestItemMerging()
{
    var mockDragService = new Mock<IItemDragService>();
    var operationService = new ItemOperationService();
    
    Assert.IsTrue(operationService.TryMergeItems(item1, slot));
}
```

## Requirements

- Unity 2022.3 LTS or higher
- TextMeshPro
- Unity Netcode for GameObjects (optional)
- C# 9.0+ support

## License

This project is licensed under the MIT License.

README.md
Displaying README.md.
