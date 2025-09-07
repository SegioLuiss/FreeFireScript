_G.Config = {
    Size = UDim2.fromOffset(580, 460)
}

repeat task.wait() until game:IsLoaded()


local Players = game:GetService("Players")
local localPlayer = Players.LocalPlayer
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local VirtualUser = game:GetService("VirtualUser")
local PlayerGui = localPlayer:WaitForChild("PlayerGui")




local Packages = ReplicatedStorage.Packages
local index = Packages._Index

local WindUI = loadstring(game:HttpGet("https://github.com/Footagesus/WindUI/releases/latest/download/main.lua"))()

local islandCoords = {
    ["01"] = { name = "Weather Machine", position = CFrame.new(-1495, 7, 1886) },
    ["02"] = { name = "Esoteric Depths", position = CFrame.new(3157, -1303, 1439) },
    ["03"] = { name = "Tropical Grove", position = CFrame.new(-2038, 3, 3650) },
    ["04"] = { name = "Stingray Shores", position = CFrame.new(-32, 4, 2773) },
    ["05"] = { name = "Kohana Volcano", position = CFrame.new(-519, 24, 189) },
    ["06"] = { name = "Coral Reefs", position = CFrame.new(-3095, 1, 2177) },
    ["07"] = { name = "Crater Island", position = CFrame.new(968, 1, 4854) },
    ["08"] = { name = "Kohana", position = CFrame.new(-658, 3, 719) },
    ["09"] = { name = "Winter Fest", position = CFrame.new(1611, 4, 3280) },
    ["10"] = { name = "Isoteric Island", position = CFrame.new(1987, 4, 1400) },
    ["11"] = { name = "Lost Isle", position = CFrame.new(-3670.30078125, -113.00000762939453, -1128.0589599609375)},
    ["12"] = { name = "Lost Isle [Lost Shore]", position = CFrame.new(-3697, 97, -932)},
    ["13"] = { name = "Lost Isle [Sisyphus]", position = CFrame.new(-3719.850830078125, -113.00000762939453, -958.6303100585938)},
    ["14"] = { name = "Lost Isle [Treasure Hall]", position = CFrame.new(-3652, -298.25, -1469)},
    ["15"] = { name = "Lost Isle [Treasure Room]", position = CFrame.new(-3740, -135, -1009)}
}



local baits = {
    { Name = "Topwater Bait", Price = "100 Coins", ID = 10, Desc = "Luck: 8%" },
    { Name = "Luck Bait", Price = "1k Coins", ID = 2, Desc = "Luck: 10%" },
    { Name = "Midnight Bait", Price = "3k Coins", ID = 3, Desc = "Luck: 20%" },
    { Name = "Chroma Bait", Price = "290k Coins", ID = 6, Desc = "Luck: 100%" },
    { Name = "Dark Mater Bait", Price = "630k Coins", ID = 8, Desc = "Luck: 175%" },
    { Name = "Corrupt Bait", Price = "1.15M Coins", ID = 15, Desc = "Luck: 200% | Mutation Chance: 10% | Shiny Chance: 10%" }
}

local oldNamecall
oldNamecall = hookmetamethod(game, "__namecall", newcclosure(function(self, ...)
    local method = getnamecallmethod()
    local args = {...}

    if method == "FireServer" and tostring(self) == "URE/UpdateOxygen" then
        warn("Tahan Napas Bang")
        return nil -- prevent call
    end

    return oldNamecall(self, unpack(args))
end))






local Window = WindUI:CreateWindow({
    Title = "GOOFY SCRIPT",
    Icon = "rbxassetid://129260712070622",
    IconThemed = true,
    Author = "FISH IT!",
    Folder = "EEE",
    Size = _G.Config.Size,
    Transparent = true,
    Theme = "Dark",
    User = {
        Enabled = true, -- <- or false
        Callback = function() print(tostring(game.Players.LocalPlayer.Name)) end,
        Anonymous = false -- <- or true
    },
    SideBarWidth = 200,
    -- HideSearchBar = true,
    ScrollBarEnabled = true,
})


local Tabs = {}

do
    Tabs.MainSection = Window:Section({
        Title = "Main",
        Opened = true,
    })
    
    Tabs.LocalSection = Window:Section({
        Title = "Local Client",
        Opened = false,
    })
    
    Tabs.OtherSection = Window:Section({
        Title = "Other",
        Opened = false,
    })

    
    Tabs.GeneralTab = Tabs.MainSection:Tab({ Title = "General", Icon = "layout-dashboard" })
    Tabs.TeleportTab = Tabs.MainSection:Tab({ Title = "Island-Teleport", Icon = "tree-palm" })
    
    Tabs.LocalTab = Tabs.LocalSection:Tab({ Title = "LocalPlayer", Icon = "baby" })
end

Tabs.GeneralTab:Toggle({
    Title = "Auto Fishing",
    Value = false,
    Callback = function(state) 
        _G.Auto_Fishing = state
    end
})

Tabs.GeneralTab:Toggle({
    Title = "Auto Upgrade Rod",
    Value = false,
    Callback = function(state) 
        _G.Auto_UpgradeRod = state
    end
})
local function convertToNumber(str)
    local num, suffix = str:match("([%d%.]+)([KMB]?)")

    num = tonumber(num)
    if not num then return nil end

    if suffix == "K" then
        num = num * 1e3
    elseif suffix == "M" then
        num = num * 1e6
    elseif suffix == "B" then
        num = num * 1e9
    end

    return math.floor(num + 0.5)
end
local function getCoins()
    return convertToNumber(PlayerGui.Events.Frame.CurrencyCounter.Counter.Text)
end

local rods = {
    { Name = "Luck Rod", Price = 350, ID = 79 },
    { Name = "Carbon Rod", Price = 900, ID = 76 },
    { Name = "Grass Rod", Price = 1500, ID = 85 },
    { Name = "Demascus Rod", Price = 3000, ID = 77 },
    { Name = "Ice Rod", Price = 5000, ID = 78 },
    { Name = "Lucky Rod", Price = 15000, ID = 4 },
    { Name = "Midnight Rod", Price = 50000, ID = 80 },
    { Name = "Steampunk Rod", Price = 215000, ID = 6 },
    { Name = "Chrome Rod", Price = 437000, ID = 7 },
    { Name = "Astral Rod", Price = 1000000, ID = 5 }
}

local function getCoins()
    return convertToNumber(PlayerGui.Events.Frame.CurrencyCounter.Counter.Text)
end

local rods = {
    { Name = "Luck Rod", Price = 350, ID = 79 },
    { Name = "Carbon Rod", Price = 900, ID = 76 },
    { Name = "Grass Rod", Price = 1500, ID = 85 },
    { Name = "Demascus Rod", Price = 3000, ID = 77 },
    { Name = "Ice Rod", Price = 5000, ID = 78 },
    { Name = "Lucky Rod", Price = 15000, ID = 4 },
    { Name = "Midnight Rod", Price = 50000, ID = 80 },
    { Name = "Steampunk Rod", Price = 215000, ID = 6 },
    { Name = "Chrome Rod", Price = 437000, ID = 7 },
    { Name = "Astral Rod", Price = 1000000, ID = 5 }
}


spawn(function()
    while true do wait()
        pcall(function()
            if _G.Auto_Fishing then
                if workspace.Characters[localPlayer.Name]:FindFirstChild("!!!EQUIPPED_TOOL!!!") then
                    if workspace.CosmeticFolder:FindFirstChild(tostring(game.Players.LocalPlayer.UserId)) then -- ถ้าไม่เจอ child ที่ชื่อตรงกับ userid ของฉัน
                        task.wait(0.1)
                        index["sleitnick_net@0.2.0"].net["RE/FishingCompleted"]:FireServer()
                    else
                        index["sleitnick_net@0.2.0"].net["RF/ChargeFishingRod"]:InvokeServer(1757240106.480528)
                        index["sleitnick_net@0.2.0"].net["RF/RequestFishingMinigameStarted"]:InvokeServer(-1.233184814453125, 0.9807072773666918)
                    end
                else
                    index["sleitnick_net@0.2.0"].net["RF/CancelFishingInputs"]:InvokeServer()
                    task.wait(0.3)
                    index["sleitnick_net@0.2.0"].net["RE/EquipToolFromHotbar"]:FireServer(1)
                end
            end
        end)
    end
end)


Tabs.TeleportTab:Dropdown({
    Title = "Select an Island",
    Values = {
        "Weather Machine",
        "Esoteric Depths",
        "Tropical Grove",
        "Stingray Shores",
        "Kohana Volcano",
        "Coral Reefs",
        "Crater Island",
        "Kohana",
        "Winter Fest",
        "Isoteric Island",
        "Lost Isle",
        "Lost Isle [Lost Shore]",
        "Lost Isle [Sisyphus]",
        "Lost Isle [Treasure Hall]",
        "Lost Isle [Treasure Room]"
    },
    Value = "Lost Isle [Treasure Room]",
    Callback = function(option)
        _G.Selected_Island = option
    end
})

Tabs.TeleportTab:Button({
    Title = "Teleport",
    Desc = "Teleport to selected island",
    Callback = function()
        if _G.Selected_Island then
            for _, island in pairs(islandCoords) do
                if island.name == _G.Selected_Island then
                    if localPlayer.Character and localPlayer.Character:FindFirstChild("HumanoidRootPart") then
                        localPlayer.Character.HumanoidRootPart.CFrame = island.position
                    end
                    break
                end
            end
        end
    end
})





WindUI:Notify({
    Title = "Inf Oxygen",
    Content = "Has Actived!",
    Duration = 3,
})

-- Sell Item
--Packages._Index["sleitnick_net@0.2.0"].net["RF/SellAllItems"]:InvokeServer()

