<div align="center">
  <h1>🌌 Catraz Hub UI Library</h1>
  <p><em>The ultimate, highly-customizable modified Orion Library for Roblox.</em></p>
  
  <p>
    <img src="https://img.shields.io/badge/Version-1.0.0-blue?style=for-the-badge&logo=roblox" alt="Version">
    <img src="https://img.shields.io/badge/Status-Active-success?style=for-the-badge" alt="Status">
    <img src="https://img.shields.io/badge/UI-Modern_Glass-8A2BE2?style=for-the-badge" alt="UI Style">
  </p>
</div>

---

🚀 Initialization & Window Creation
To start using the library, load the source and create your main window. The window supports auto-resizing based on device (PC/Mobile) and features a modern floating toggle when minimized.
local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/nurvian/Catraz-x-Orion-UI/refs/heads/main/source.lua')))()

```lua
local Window = OrionLib:MakeWindow({
    Name = "Catraz Hub",
    Subtext = "Premium Script Hub",
    Version = "v1.0.0",
    VersionIcon = "shield-check", -- Uses Lucide icons
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "CatrazConfig",
    IntroEnabled = true,
    IntroText = "Welcome to Catraz",
    IntroIcon = "rbxassetid://8834748103",
    Icon = "rbxassetid://8834748103",
    ShowIcon = true,
    
    -- Custom Theme & Appearance
    ImageBackground = "rbxassetid://93195749393891", -- Custom background image
    ImageTransparency = 0.8,
    WindowTransparency = 0.1, -- Overall window transparency
    
    -- Floating Toggle Customization
    ToggleIcon = "rbxassetid://105921924721005",
    ToggleSize = 50
})

-- Available Themes: "Default" (Red Outline), "Ocean", "Void", "Hackerman"
OrionLib.SelectedTheme = "Ocean"
```

📑 Core Features
Creating a Tab
Tabs now support a Glass design and toggleable outlines.

```lua
local MainTab = Window:MakeTab({
    Name = "Main Features",
    Icon = "swords", -- Lucide Icon string or rbxassetid
    PremiumOnly = false,
    Glass = true,   -- Transparent glass effect
    Outline = true  -- Toggle border outline
})
```

Creating a Section
Sections can be folded and also support the new Glass and Outline aesthetics.

```lua
local FarmSection = MainTab:AddSection({
    Name = "Auto Farming",
    TextSize = 17,
    Folded = false,
    Glass = true,
    Outline = true
})
```

The Built-in Config Manager
Instead of building your own config UI, use the built-in advanced Config Tab. It handles saving, loading, overwriting, auto-loading, and even cloud sharing via clipboard/URLs!

```lua
-- Simply call this on your Window object to generate a fully functional Config Tab
Window:AddConfigTab({
    Name = "Settings",
    Icon = "settings"
})
```

🧩 UI Elements
All elements support the Outline = true/false parameter to match your preferred aesthetic.

Buttons
```lua
FarmSection:AddButton({
    Name = "Execute Script",
    Icon = "play",
    Outline = true,
    Callback = function()
        print("Script executed!")
    end
})
```

Toggles
```lua
local AutoFarmToggle = FarmSection:AddToggle({
    Name = "Enable Auto Farm",
    Default = false,
    Color = Color3.fromRGB(0, 150, 255), -- Custom active color
    Outline = true,
    Flag = "AutoFarmFlag",
    Save = true,
    Callback = function(Value)
        print("Auto Farm is now:", Value)
    end
})

-- Update a toggle remotely:
-- AutoFarmToggle:Set(true)
```

Advanced Dynamic Paragraphs
Unlike standard text labels, paragraphs now support images, descriptions, and interactive inline buttons. You can also update them on the fly.
```lua
local InfoParagraph = FarmSection:AddParagraph({
    Title = "Player Stats",
    Desc = "Level: 100\nCoins: 50,000",
    Image = "user", -- Lucide icon or rbxassetid
    ImageSize = 38,
    Buttons = {
        {
            Title = "Refresh",
            Callback = function()
                print("Stats Refreshed!")
            end
        }
    }
})

-- Live Updating:
-- InfoParagraph:SetTitle("New Title")
-- InfoParagraph:SetDesc("Updated Description")
-- InfoParagraph:SetImage("new-icon")
```

Sliders
```lua
FarmSection:AddSlider({
    Name = "WalkSpeed",
    Min = 16,
    Max = 100,
    Default = 16,
    Color = Color3.fromRGB(255, 255, 255),
    Increment = 1,
    ValueName = "WS",
    Outline = true,
    Callback = function(Value)
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = Value
    end    
})
```

Dropdowns (with Search & Multi-select)
```lua
local ItemDropdown = FarmSection:AddDropdown({
    Name = "Select Item",
    Default = "Sword",
    Options = {"Sword", "Bow", "Staff", "Shield"},
    Multi = false,
    Search = true, -- Enables search bar inside dropdown
    AllowNone = true,
    Outline = true,
    Callback = function(Value)
        print("Selected:", Value)
    end
})

-- Refreshing Dropdown Options:
-- ItemDropdown:Refresh({"New Item 1", "New Item 2"}, true)
```

Keybinds
```lua
FarmSection:AddBind({
    Name = "Toggle Menu",
    Default = Enum.KeyCode.RightShift,
    Hold = false,
    Outline = true,
    Callback = function()
        print("Key pressed")
    end    
})
```

Textboxes
```lua
FarmSection:AddTextbox({
    Name = "Target Player",
    Default = "",
    TextDisappear = false,
    Outline = true,
    Callback = function(Value)
        print("Targetting: " .. Value)
    end	  
})
```

Colorpickers
```lua
FarmSection:AddColorpicker({
    Name = "ESP Color",
    Default = Color3.fromRGB(255, 0, 0),
    Outline = true,
    Callback = function(Value)
        print("Color changed")
    end	  
})
```

🔔 Notifications & Dialogs
Custom Dialog Box
Prompt users with a clean, animated Yes/No dialog box. Perfect for preventing accidental exits.

```lua
OrionLib:AddDialog({
    Title = "Warning",
    Content = "Are you sure you want to delete this config?",
    YesText = "Confirm",
    NoText = "Cancel",
    Callback = function()
        print("Confirmed!")
    end
})
```

Advanced Notifications
Notifications now support custom background images.

```lua
OrionLib:MakeNotification({
    Name = "Alert",
    Content = "This is a custom notification.",
    Image = "bell",
    Time = 5,
    ImageBackground = "rbxassetid://93195749393891", -- Optional background image
    ImageTransparency = 0.8
})
```

🛠️ Utility Functions
Change Floating Toggle Icon Dynamically

```lua
OrionLib:ChangeToggleIcon("rbxassetid://1234567890") 
-- Or use a Lucide icon string if your icon system supports it
```

Destroying the Interface
Safely removes the UI from the CoreGui.
```lua
OrionLib:Destroy()
```

Initializing Auto-Load Configs
Call this at the very end of your script, after setting up all your tabs and elements, to automatically load the user's saved startup config.
```lua
OrionLib:Init()
```
