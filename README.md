# RT_INVENTORY_ADDONS
Addons to ox_inventory

# Back Items
# Configuration Variables
The following configuration variables are defined:

- BACK_ITEM_LIMIT: Specifies the maximum number of back items that can be equipped. The default value is 3.

- BACK_ITEM_SLOTS_DEFAULT: Defines the default settings for each back item slot. It is a table containing three entries, each representing a slot number. Each slot has the following properties:

  - backData: Indicates whether back data is enabled for the slot (boolean value).
  - defaultoffset: Specifies the default offset for the back item on the slot.
    
- BACK_ITEMS: Contains the configuration for various back items. Each back item is represented by a key-value pair. The key is a string representing the item's identifier, and the value is a table representing the item's properties. The available properties for each back item are as follows:

  - prio (mandatory): Specifies the priority of the item. Items with higher priority values will be take priority on being displayed.

  - ignoreLimits (optional): Indicates whether the item should be exempted from the back item limit defined by BACK_ITEM_LIMIT. It is a boolean value.

  - hash(mandatory): Specifies the hash value of the weapon or model.

  - customPos (optional, but mandatory when ignoreLimits is used): Contains custom position and rotation data for the item. It is a table with the following properties:

    - pos: Specifies the position of the item as a vector3 (x, y, z).
    - rot: Specifies the rotation of the item as a vector3 (x, y, z).
    - bone: Specifies the bone to attach the item to (optional).
    - overrideDefaultZ: Indicates whether to override the default Z position (optional).
# Adding New Items
To add new items, follow the structure of the existing items in the BACK_ITEMS table. Here is an example of adding a new item with default values:

>['NEW_ITEM'] = {
>    prio = 1,
>    hash = joaat('model_or_weapon_hash'),
>    customPos = {
>        pos = vec3(0.0, 0.0, 0.0),
>        rot = vec3(0.0, 0.0, 0.0)
>    }
>}
In this example, we've added a new item called **'NEW_ITEM'**. Here are the properties used:

- prio: The priority of the item is set to 1.
- isWeapon: Since this is not a weapon, we set it to false.
- hash: We specify the model of the new item using the hash property. Replace model_or_weapon_hash with the appropriate hash value for the desired model or weapon.
- customPos: We provide custom position and rotation data for the item. The pos property is set to the default position (0.0, 0.0, 0.0), and the rot property is set to the default rotation (0.0, 0.0, 0.0).
  
You can modify the values of the properties based on your needs.

Save the changes and run the code with the new item configuration.

# Item Carry
# Configuration Variables
This script is used to automatically carry items when using ox_inventory in your FiveM resource. By adding entries to the CARRY_ITEMS table, you can define the animations, prop models, and placement positions for different items that your players can carry.

# Adding New Entries to CARRY_ITEMS
To add a new entry to the **CARRY_ITEMS** table in your Lua script, follow the structure provided below:

>CARRY_ITEMS = {
>    ['item_name'] = {
>        animation = 'idle',
>        dictionary = 'animation_dictionary',
>        animationFlag = animation_flag,
>        prop = {
>            bone = bone_id,
>            model = 'prop_model',
>            placement = {
>                pos = vector3(x_pos, y_pos, z_pos),
>                rot = vector3(x_rot, y_rot, z_rot),
>            },
>        },
>    },
>}

- item_name: The name of the inventory item. This will be used as the key in the **CARRY_ITEMS** table. NOTE: CARRY ITEMS SHOULD NOT STACK
- animation_dictionary: The name of the animation dictionary associated with the item.
- animation_flag?: The animation flag value for the item. This determines the behavior of the item when carried.
- bone_id: The bone ID on the player's character model where the prop will be attached.
- prop_model: The model name of the prop that represents the item.
- x_pos, y_pos, z_pos: The position coordinates (in meters) relative to the bone where the prop will be placed.
- x_rot, y_rot, z_rot: The rotation angles (in degrees) for the prop in the X, Y, and Z axes.
  
Make sure to maintain the indentation and syntax rules of the existing **CARRY_ITEMS** table for consistency.

# Example Usage
Let's say you want to add a new item called 'briefcase' to the **CARRY_ITEMS** table. Here's how the entry might look:

>CARRY_ITEMS = {
>    ['box'] = {
>        animation = 'idle',
>        dictionary = 'anim@heists@box_carry@',
>        animationFlag = 51,
>        prop = {
>            bone = 60309,
>            model = 'hei_prop_heist_box',
>            placement = {
>                pos = vector3(0.025000, 0.080000, 0.255000),
>                rot = vector3(-145.000000, 290.000000, 0.000000),
>            },
>        },
>    },
>    ['briefcase'] = {
>        animation = 'idle',
>        dictionary = 'anim@heists@briefcase@',
>        animationFlag = 52,
>        prop = {
>            bone = 60310,
>            model = 'prop_briefcase_02',
>            placement = {
>                pos = vector3(0.035000, 0.070000, 0.240000),
>                rot = vector3(-135.000000, 280.000000, 0.000000),
>            },
>        },
>    },
>}
Ensure that the new entry is added within the existing **CARRY_ITEMS** table in **itemCarry/server/data**, maintaining the comma separation between entries.
