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
