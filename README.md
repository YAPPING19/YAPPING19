local player = game.Players.LocalPlayer
local UIS = game:GetService("UserInputService")

-- GUI Setup
local screenGui = Instance.new("ScreenGui", game.CoreGui)
screenGui.Name = "SpeedTabsGUI"

local main = Instance.new("Frame", screenGui)
main.Size = UDim2.new(0, 240, 0, 280)
main.Position = UDim2.new(0.5, -120, 0.1, 0)
main.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
main.Active = true
main.Draggable = true
main.BorderSizePixel = 0
main.BackgroundTransparency = 0.1

-- Toggle Button
local toggleButton = Instance.new("TextButton", screenGui)
toggleButton.Size = UDim2.new(0, 100, 0, 30)
toggleButton.Position = UDim2.new(0.5, -50, 0, 10)
toggleButton.Text = "Toggle GUI"
toggleButton.BackgroundColor3 = Color3.fromRGB(70, 130, 180)
toggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
toggleButton.TextSize = 14
toggleButton.Font = Enum.Font.SourceSansBold

toggleButton.MouseButton1Click:Connect(function()
	main.Visible = not main.Visible
end)

-- Tabs
local tabBar = Instance.new("Frame", main)
tabBar.Size = UDim2.new(1, 0, 0, 30)
tabBar.BackgroundColor3 = Color3.fromRGB(30, 30, 30)

local content = Instance.new("Frame", main)
content.Position = UDim2.new(0, 0, 0, 30)
content.Size = UDim2.new(1, 0, 1, -30)
content.BackgroundColor3 = Color3.fromRGB(25, 25, 25)

local tabNames = {"Speed", "DR", "Universal", "Games", "TSB", "SB", "GAG"}
local tabButtons, pages = {}, {}

for i, name in ipairs(tabNames) do
	local btn = Instance.new("TextButton", tabBar)
	btn.Size = UDim2.new(1 / #tabNames, 0, 1, 0)
	btn.Position = UDim2.new((i - 1) / #tabNames, 0, 0, 0)
	btn.Text = name
	btn.TextSize = 14
	btn.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
	btn.TextColor3 = Color3.fromRGB(255, 255, 255)
	btn.Font = Enum.Font.SourceSansBold
	tabButtons[name] = btn

	local page = Instance.new("ScrollingFrame", content)
	page.Size = UDim2.new(1, 0, 1, 0)
	page.CanvasSize = UDim2.new(0, 0, 10, 0)
	page.ScrollBarThickness = 6
	page.BackgroundTransparency = 1
	page.Visible = i == 1
	pages[name] = page
	page.AutomaticCanvasSize = Enum.AutomaticSize.Y

	local layout = Instance.new("UIGridLayout", page)
	layout.CellSize = UDim2.new(0, 70, 0, 35)
	layout.CellPadding = UDim2.new(0, 5, 0, 5)
	layout.FillDirectionMaxCells = 3
end

for _, btn in pairs(tabButtons) do
	btn.MouseButton1Click:Connect(function()
		for name, frame in pairs(pages) do
			frame.Visible = (tabButtons[name] == btn)
		end
	end)
end

-- Speed Buttons
for i = 10, 1000, 5 do
	local b = Instance.new("TextButton", pages["Speed"])
	b.Text = tostring(i)
	b.TextSize = 12
	b.BackgroundColor3 = (i >= 900 and Color3.fromRGB(0, 0, 0)) or (i >= 675 and Color3.fromRGB(139, 0, 0)) or Color3.fromRGB(70, 130, 180)
	b.TextColor3 = Color3.fromRGB(255, 255, 255)
	b.MouseButton1Click:Connect(function()
		if player.Character and player.Character:FindFirstChild("Humanoid") then
			player.Character.Humanoid.WalkSpeed = i
		end
	end)
end

-- Custom Speed Input
local input = Instance.new("TextBox", pages["Speed"])
input.PlaceholderText = "Custom Speed"
input.Text = ""
input.BackgroundColor3 = Color3.fromRGB(80, 80, 80)
input.TextColor3 = Color3.fromRGB(255, 255, 255)
input.Size = UDim2.new(0, 120, 0, 30)
input.Font = Enum.Font.SourceSans
input.TextSize = 14
input.TextTransparency = 0.5

input.FocusLost:Connect(function()
	local val = tonumber(input.Text)
	if val then
		local b = Instance.new("TextButton", pages["Speed"])
		b.Text = tostring(val)
		b.TextSize = 12
		b.BackgroundColor3 = Color3.fromRGB(100, 140, 200)
		b.TextColor3 = Color3.fromRGB(255, 255, 255)
		b.MouseButton1Click:Connect(function()
			if player.Character and player.Character:FindFirstChild("Humanoid") then
				player.Character.Humanoid.WalkSpeed = val
			end
		end)
	end
end)

-- Button Creator
local function createButton(tab, name, func)
	local b = Instance.new("TextButton", pages[tab])
	b.Text = name
	b.TextSize = 12
	b.BackgroundColor3 = Color3.fromRGB(90, 90, 90)
	b.TextColor3 = Color3.fromRGB(255, 255, 255)
	b.Font = Enum.Font.SourceSansBold
	b.MouseButton1Click:Connect(func)
end

-- === Script Buttons (REPLACE BELOW SAFELY) ===

createButton("DR", "KiciaHook", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/kiciahook/kiciahook/refs/heads/main/loader.luau"))() end)

-- === Script Buttons (REPLACE BELOW SAFELY) ===

-- DR Scripts createButton("DR", "KiciaHook", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/kiciahook/kiciahook/refs/heads/main/loader.luau"))() end)

createButton("DR", "NullFire Script", function() loadstring(game:HttpGet("https://rawscripts.net/raw/Dead-Rails-Alpha-NullFire-32921"))() end)

createButton("DR", "Tp To all V2", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/TwoGunVolley/Eeeee/refs/heads/main/RailsDated.txt"))() end)

createButton("DR", "Vehicle Fly Gui", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/GhostPlayer352/Test4/main/Vehicle%20Fly%20Gui"))() end)

createButton("DR", "Teleport All Locations", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/m00ndiety/dead-rails-teleport-everywhere/refs/heads/main/teleport%20all%20locations"))() end)

createButton("DR", "Tp To Sterling", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/ringtaa/sterlingnotifcation.github.io/refs/heads/main/Sterling.lua"))() end)

createButton("DR", "RINGTA", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/ringtaa/NEWFIXEDUI.github.io/refs/heads/main/ui.lua"))() end)

createButton("DR", "Nebula Hub", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/NebulaHubOfc/Public/refs/heads/main/Loader.lua"))() end)

createButton("DR", "My", function() loadstring(game:HttpGet("https://pastebin.com/raw/NNRzb6Zr"))() end)

createButton("DR", "Skull Hub", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/hungquan99/SkullHub/main/loader.lua"))() end)

createButton("DR", "MoonDiety", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/m00ndiety/dead-rails-teleport-everywhere/refs/heads/main/teleport%20all%20locations"))() end)

createButton("DR", "Weld On Air", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/HeadHarse/Dusty/refs/heads/main/WeldObject"))() end)

createButton("DR", "Npc Lock End", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/TwoGunVolley/FixedPlease/refs/heads/main/Protected_7197551640341824.txt"))() end)

createButton("DR", "Zysume Gui", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/GRPGaming/Key-System/refs/heads/Xycer-Hub-Script/Hellos"))() end)

createButton("DR", "Tbao Hub", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/tbao143/thaibao/refs/heads/main/TbaoHubDeadRails"))() end)

createButton("DR", "Neox Hub", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/hassanxzayn-lua/NEOXHUBMAIN/refs/heads/main/loader", true))() end)

createButton("DR", "Teleport Items", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/thiennrb7/Script/refs/heads/main/Bringall"))() end)

createButton("DR", "Spider Hub", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/SpiderScriptRB/Dead-Rails-SpiderXHub-Script/refs/heads/main/SpiderXHub%202.0.txt"))() end)

createButton("DR", "Isna Hamzah Hub", function() loadstring(game:HttpGet("https://isnahamzahpastebin.tech/loader/isna_scripthub_30"))() end)

createButton("DR", "Auto End", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/gumanba/Scripts/refs/heads/main/DeadRailsAuto"))() end)

createButton("DR", "Nat Hub", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/ArdyBotzz/NatHub/refs/heads/master/NatHub.lua"))() end)

createButton("DR", "Dhz Hub", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/ducknovis/DHHz-hub/refs/heads/main/Dead-Rails.lua"))() end)

createButton("DR", "Norepina Hub", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/Vermzky/VermzHub/refs/heads/main/FREE"))() end)

createButton("DR", "Ronix Hub", function() loadstring(game:HttpGet("https://api.luarmor.net/files/v3/loaders/7e85e09e0a7cb75cfc813416ab17672c.lua"))() end)

createButton("DR", "Speed Hub", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/AhmadV99/Speed-Hub-X/main/Speed%20Hub%20X.lua", true))() end)

createButton("DR", "Rins Hub", function() loadstring(game:HttpGet("https://rawscripts.net/raw/Dead-Rails-Alpha-Best-keyless-script-30227"))() end)

createButton("DR", "Sometank Hub", function() loadstring(game:HttpGet("https://zuwz.xyz/Somtank-DR.lua"))() end)

createButton("DR", "Iraq Hub", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/Rly-tech/skill/refs/heads/main/Dead-Rails"))() end)

createButton("DR", "Item Teleport", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/thiennrb7/Script/refs/heads/main/Bringall"))() end)

createButton("DR", "Tora Hub", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/gumanba/Scripts/refs/heads/main/DeadRails", true))() end)

createButton("DR", "Emplic Hub", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/Emplic/deathrails/refs/heads/main/bond"))() end)

createButton("DR", "Anas Hub", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/badass1ia/Merciful/refs/heads/main/Absurdity111"))() end)

createButton("DR", "Mark Hub", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/Markklol/AnimalSimulator/refs/heads/main/DRails.lua"))() end)

createButton("DR", "Fern Hub", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/Mrpopcatfrombupge/FernHub/refs/heads/main/DeadRailsFarm", true))() end)

createButton("DR", "Aussie Hub", function() loadstring(game:HttpGet(request({Url='https://aussie.productions/script'}).Body))() end)

createButton("DR", "Strelizia Hub", function() loadstring(game:HttpGet("https://rawscripts.net/raw/Dead-Rails-Alpha-strelizia-script-hub-31809"))() end)

-- Games Tab Scripts
createButton("Games", "MM2 Tool", function()
	loadstring(game:HttpGet("https://pastebin.com/raw/Vec48eZf"))()
end)

createButton("Games", "ANTI KB Slap Tower", function()
	loadstring(game:HttpGet("https://raw.githubusercontent.com/amdzy088/Immune-slap-tower-/refs/heads/main/Immune%20slap%20tower%20work"))()
end)

-- Universal Tab Scripts
createButton("Universal", "FlashBack", function()
	loadstring(game:HttpGet("https://mscripts.vercel.app/scfiles/reverse-script.lua"))()
end)

createButton("Universal", "Fake WallHop V2", function()
	loadstring(game:HttpGet("https://raw.githubusercontent.com/ScpGuest666/Random-Roblox-script/refs/heads/main/Roblox%20WallHop%20V2%20script"))()
end)

createButton("Universal", "Ghost Freecam", function()
	loadstring(game:HttpGet("https://raw.githubusercontent.com/GhostPlayer352/Test4/main/Freecam"))()
end)

createButton("Universal", "Old Server Finder", function()
	loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Old-server-finder-23398"))()
end)

createButton("Universal", "Save Tp Place", function()
	loadstring(game:HttpGet("https://raw.githubusercontent.com/0Ben1/fe/main/Tp%20Place%20GUI", true))()
end)

createButton("Universal", "Equinox Hub", function()
	loadstring(game:HttpGet("https://pastebin.com/raw/wzB1Qh78", true))()
end)

createButton("Universal", "Instant Interact", function()
	game:GetService("ProximityPromptService").PromptButtonHoldBegan:Connect(function(prompt)
		fireproximityprompt(prompt)
	end)
end)

createButton("Universal", "Infinite Yield Reborn", function()
	loadstring(game:HttpGet("https://raw.githubusercontent.com/mxsynry/infiniteyield-reborn/refs/heads/scriptblox/source"))()
end)

createButton("Universal", "Nameless Admin", function()
	loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Nameless-Admin-cool-admin-commands-36157"))()
end)

createButton("Universal", "FlyGui V3", function()
	loadstring(game:HttpGet("https://raw.githubusercontent.com/XNEOFF/FlyGuiV3/main/FlyGuiV3.txt"))()
end)

createButton("Universal", "Cold Shaking Gui", function()
    -- Cold Effect GUI with Shake Intensity and Speed Adjustment (Simplified)

    local player = game.Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()
    local hrp = character:WaitForChild("HumanoidRootPart")
    local shaking = false

    -- Change these values to control the shake intensity and speed
    local shakeIntensity = 2  -- Intensity of the shake (higher = stronger shake)
    local shakeSpeed = 40     -- Speed of the shake (higher = faster shake)

    -- GUI Setup
    local ScreenGui = Instance.new("ScreenGui", game.CoreGui)
    ScreenGui.Name = "ColdEffectGUI"

    local Frame = Instance.new("Frame", ScreenGui)
    Frame.Size = UDim2.new(0, 100, 0, 50)
    Frame.Position = UDim2.new(0.5, -50, 0, 20)
    Frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
    Frame.BackgroundTransparency = 0.3
    Frame.Active = true
    Frame.Draggable = true

    local DragBar = Instance.new("Frame", Frame)
    DragBar.Size = UDim2.new(1, 0, 0, 20)
    DragBar.Position = UDim2.new(0, 0, 0, 0)
    DragBar.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
    DragBar.BackgroundTransparency = 0.4

    local Button = Instance.new("TextButton", Frame)
    Button.Size = UDim2.new(1, 0, 0, 30)
    Button.Position = UDim2.new(0, 0, 0, 20)
    Button.Text = "Cold: OFF"
    Button.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
    Button.TextColor3 = Color3.new(1, 1, 1)
    Button.Font = Enum.Font.GothamBold
    Button.TextScaled = true

    -- Toggle cold shaking effect
    Button.MouseButton1Click:Connect(function()
        shaking = not shaking
        Button.Text = "Cold: " .. (shaking and "ON" or "OFF")
    end)

    game:GetService("RunService").RenderStepped:Connect(function()
        if shaking and hrp then
            -- Shake intensity and speed are controlled by the shakeIntensity and shakeSpeed variables
            local angle = math.sin(tick() * shakeSpeed) * math.rad(shakeIntensity)
            hrp.CFrame = hrp.CFrame * CFrame.Angles(0, angle, 0)
        end
    end)
end)

createButton("Universal", "ESP", function()

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local Camera = workspace.CurrentCamera
local ESPEnabled = true  -- Toggle flag for ESP
local ESPDistance = 1000000  -- 1 million studs distance for ESP

-- Function to create ESP for a player
local function createESP(player)
    -- Highlight for player body
    local highlight = Instance.new("Highlight")
    highlight.Name = "ESPHighlight"
    highlight.Adornee = player.Character
    highlight.FillColor = Color3.fromRGB(255, 255, 0)  -- Yellow body highlight
    highlight.FillTransparency = 0.5  -- Transparency for the highlight
    highlight.OutlineColor = Color3.fromRGB(0, 0, 0)  -- Black outline
    highlight.OutlineTransparency = 0.2  -- Transparency for outline
    highlight.Parent = player.Character or player.CharacterAdded:Wait()

    -- Text for player's display name and real name
    local displayNameText = Drawing.new("Text")
    displayNameText.Color = Color3.fromRGB(255, 255, 255)
    displayNameText.Size = 10  -- Smaller text size for real name
    displayNameText.Center = true
    displayNameText.Outline = true
    displayNameText.OutlineColor = Color3.fromRGB(0, 0, 0)
    displayNameText.Text = player.DisplayName .. " (" .. player.Name .. ")"

    -- Update ESP every frame
    RunService.RenderStepped:Connect(function()
        if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
            local hrp = player.Character.HumanoidRootPart
            local screenPos, onScreen = Camera:WorldToScreenPoint(hrp.Position)
            if onScreen and (hrp.Position - Camera.CFrame.Position).Magnitude <= ESPDistance then
                -- Update position of text above player
                displayNameText.Position = Vector2.new(screenPos.X, screenPos.Y - 20)  -- Display above player
                displayNameText.Visible = true
            else
                displayNameText.Visible = false
            end
        else
            displayNameText.Visible = false
        end
    end)
end

-- Function to remove ESP for a player
local function removeESP(player)
    if player.Character and player.Character:FindFirstChild("ESPHighlight") then
        player.Character.ESPHighlight:Destroy()
    end
end

-- Create ESP for new players who join the game
Players.PlayerAdded:Connect(function(player)
    player.CharacterAdded:Connect(function()
        if ESPEnabled then
            createESP(player)
        end
    end)
end)

-- Remove ESP when a player leaves the game
Players.PlayerRemoving:Connect(function(player)
    removeESP(player)
end)

-- Function to apply ESP for all existing players (even those already in the server)
for _, player in pairs(Players:GetPlayers()) do
    if player.Character then
        createESP(player)
    end
end

-- Create ESP toggle button at the top-right corner
local toggleButton = Drawing.new("Text")
toggleButton.Text = "Toggle ESP"
toggleButton.Size = 14
toggleButton.Position = Vector2.new(0.95, 0.05)  -- Right-top corner
toggleButton.Color = Color3.fromRGB(255, 255, 255)
toggleButton.Center = true
toggleButton.Outline = true
toggleButton.OutlineColor = Color3.fromRGB(0, 0, 0)

-- Toggle ESP on and off when the button is clicked
toggleButton.MouseButton1Click = function()
    ESPEnabled = not ESPEnabled
    toggleButton.Text = ESPEnabled and "Disable ESP" or "Enable ESP"
    if ESPEnabled then
        -- Enable ESP for all players
        for _, player in pairs(Players:GetPlayers()) do
            if player.Character then
                createESP(player)
            end
        end
    else
        -- Disable ESP for all players
        for _, player in pairs(Players:GetPlayers()) do
            removeESP(player)
        end
    end
end
end)

createButton("Universal", "Draw Chat", function()

loadstring(game:HttpGet("https://raw.githubusercontent.com/balditeacher/obfuscated-mobile-supportloadstring/main/obfuscated"))()
end)

createButton("Universal", "RESET GUI", function()

loadstring(game:HttpGet("https://pastebin.com/raw/HBxXfxiQ"))()
end)

createButton("Universal", "CCTV Gui", function()

loadstring(game:HttpGet("https://pastebin.com/raw/YeAXwREc"))()
end)

createButton("Universal", "Keyboard", function()

loadstring(game:HttpGet("https://gist.githubusercontent.com/RedZenXYZ/4d80bfd70ee27000660e4bfa7509c667/raw/da903c570249ab3c0c1a74f3467260972c3d87e6/KeyBoard%2520From%2520Ohio%2520Fr%2520Fr"))()
end)

createButton("Universal", "Hitbox Tool", function()
	loadstring(game:HttpGet("https://pastefy.app/4525LUdw/raw", true))()
end)

-- Make sure all `createButton(...)` calls go AFTER `createButton` is defined.

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")

-- Create ScreenGui
local gui = Instance.new("ScreenGui")
gui.Name = "FTAPCredit"
gui.ResetOnSpawn = false
gui.IgnoreGuiInset = true
gui.Parent = Players.LocalPlayer:WaitForChild("PlayerGui")

-- Create TextLabel
local label = Instance.new("TextLabel")
label.Name = "CreditLabel"
label.Size = UDim2.new(0, 300, 0, 30)
label.Position = UDim2.new(0.5, 0, 1, -40) -- Center bottom
label.AnchorPoint = Vector2.new(0.5, 0)
label.BackgroundTransparency = 1
label.Text = "Made by 《⨼⸋⼞⼼⼢⼝⾅⾳⸋⨽》TikTok"
label.TextScaled = true
label.Font = Enum.Font.GothamBold
label.TextStrokeTransparency = 0.5
label.TextStrokeColor3 = Color3.new(0, 0, 0)
label.Parent = gui

-- Rainbow effect using HSV
local hue = 0
RunService.RenderStepped:Connect(function(dt)
    hue = (hue + dt * 0.2) % 1
    label.TextColor3 = Color3.fromHSV(hue, 1, 1)
end)
