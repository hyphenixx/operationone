local Players = game:GetService("Players")
local workspace = game:GetService("Workspace")

local lPlr = Players.LocalPlayer
local character = lPlr.Character or lPlr.CharacterAdded:Wait() or workspace:FindFirstChild(lPlr.Name)

-- Bomb ESP drawings
local BombDot = nil
local BombText = nil

-- Store drawing objects for players
local PlayerDrawings = {}

local function clearAllPlayerESP()
    for model, drawings in pairs(PlayerDrawings) do
        drawings.box:Remove()
        drawings.headDot:Remove()
    end
    PlayerDrawings = {}
end

local function drawPlayers()
    local playerList = Players:GetPlayers()
    local seenModels = {}
    
    local validNames = {}
    for _, player in ipairs(playerList) do
        if player ~= lPlr then
            if player.Name then
                validNames[player.Name] = true
            end
            if player.DisplayName then
                validNames[player.DisplayName] = true
            end
        end
    end
    
    -- Clean up drawings for models that no longer exist
    for model, drawings in pairs(PlayerDrawings) do
        if not model or not model.Parent then
            drawings.box:Remove()
            drawings.headDot:Remove()
            PlayerDrawings[model] = nil
        end
    end
    
    for _, obj in ipairs(workspace:GetChildren()) do
        if obj:IsA("Model") and obj.Name and validNames[obj.Name] then
            local hrp = obj:FindFirstChild("HumanoidRootPart")
            local humanoid = obj:FindFirstChild("Humanoid")
            local stateObject = obj:FindFirstChild("StateObject")
            
            if hrp and humanoid and stateObject then
                seenModels[obj] = true
                
                local footPos = hrp.Position - Vector3.new(0, 2.5, 0)
                local headPos = hrp.Position + Vector3.new(0, 3, 0)
                
                local screenFoot, visFoot = WorldToScreen(footPos)
                local screenHead, visHead = WorldToScreen(headPos)
                
                local vis = visFoot or visHead
                
                if not PlayerDrawings[obj] then
                    local box = Drawing.new("Square")
                    box.Color = Color3.fromRGB(255, 255, 255)
                    box.Filled = false
                    box.Transparency = 1
                    box.ZIndex = 100
                    box.Visible = false
                    
                    local headDot = Drawing.new("Circle")
                    headDot.Color = Color3.fromRGB(255, 255, 255)
                    headDot.Filled = true
                    headDot.Transparency = 1
                    headDot.Radius = 3
                    headDot.ZIndex = 102
                    headDot.Visible = false
                    
                    PlayerDrawings[obj] = {
                        box = box,
                        headDot = headDot
                    }
                end
                
                local drawings = PlayerDrawings[obj]
                
                if vis then
                    local boxHeight = math.abs(screenFoot.Y - screenHead.Y)
                    local boxWidth = boxHeight / 1.7
                    local boxX = screenHead.X - (boxWidth / 2)
                    local boxY = screenHead.Y
                    
                    drawings.box.Position = Vector2.new(boxX, boxY)
                    drawings.box.Size = Vector2.new(boxWidth, boxHeight)
                    drawings.box.Visible = true
                    
                    -- Head dot at actual head level (slightly lower than box top)
                    local headDotPos = hrp.Position + Vector3.new(0, 1, 0)
                    local screenDot, visDot = WorldToScreen(headDotPos)
                    drawings.headDot.Position = screenDot
                    drawings.headDot.Visible = visDot
                else
                    drawings.box.Visible = false
                    drawings.headDot.Visible = false
                end
            end
        end
    end
    
    for model, drawings in pairs(PlayerDrawings) do
        if not seenModels[model] then
            drawings.box:Remove()
            drawings.headDot:Remove()
            PlayerDrawings[model] = nil
        end
    end
end

local function hideAllPlayerESP()
    for model, drawings in pairs(PlayerDrawings) do
        drawings.box.Visible = false
        drawings.headDot.Visible = false
    end
end

local function drawBomb()
    local bomb = workspace:FindFirstChild("Bomb")
    
    if bomb then
        local bombRoot = bomb:FindFirstChild("Root") or bomb:FindFirstChildOfClass("BasePart") or bomb.PrimaryPart
        
        if bombRoot then
            local pos, vis = WorldToScreen(bombRoot.Position)
            
            if not BombDot then
                BombDot = Drawing.new("Circle")
                BombDot.Color = Color3.fromRGB(255, 255, 0)
                BombDot.Filled = true
                BombDot.Transparency = 1
                BombDot.Radius = 5
                BombDot.ZIndex = 100
                BombDot.Visible = false
            end
            
            if not BombText then
                BombText = Drawing.new("Text")
                BombText.Color = Color3.fromRGB(255, 255, 0)
                BombText.Text = "Bomb"
                BombText.Size = 18
                BombText.Center = true
                BombText.Outline = true
                BombText.Transparency = 1
                BombText.ZIndex = 101
                BombText.Visible = false
            end
            
            if vis then
                BombDot.Position = pos
                BombDot.Visible = true
                
                BombText.Position = Vector2.new(pos.X, pos.Y - 20)
                BombText.Visible = true
            else
                BombDot.Visible = false
                BombText.Visible = false
            end
        else
            if BombDot then BombDot.Visible = false end
            if BombText then BombText.Visible = false end
        end
    else
        if BombDot then BombDot.Visible = false end
        if BombText then BombText.Visible = false end
    end
end

local function hideAllBombESP()
    if BombDot then BombDot.Visible = false end
    if BombText then BombText.Visible = false end
end

-- Clean up when player leaves
Players.PlayerRemoving:Connect(function(player)
    if PlayerDrawings[player] then
        PlayerDrawings[player]:Remove()
        PlayerDrawings[player] = nil
    end
end)


-- Generated by Matcha GUI Builder
local Mouse = game.Players.LocalPlayer:GetMouse()

-- TitleHolder (Square)
local TitleHolder = Drawing.new("Square")
TitleHolder.Visible = true
TitleHolder.Transparency = 1
TitleHolder.ZIndex = 30
TitleHolder.Color = Color3.fromHex("#111921")
TitleHolder.Position = Vector2.new(77, 46)
TitleHolder.Size = Vector2.new(503, 30)
TitleHolder.Filled = true

-- Intelligent Border for TitleHolder
local TitleHolder_Border = Drawing.new("Square")
TitleHolder_Border.Visible = true
TitleHolder_Border.Transparency = 1
TitleHolder_Border.ZIndex = 31
TitleHolder_Border.Color = Color3.fromHex("#8f8f8f")
TitleHolder_Border.Filled = false
TitleHolder_Border.Thickness = 1
TitleHolder_Border.Position = TitleHolder.Position
TitleHolder_Border.Size = TitleHolder.Size

-- TabSelector (Square)
local TabSelector = Drawing.new("Square")
TabSelector.Visible = true
TabSelector.Transparency = 1
TabSelector.ZIndex = 10
TabSelector.Color = Color3.fromHex("#111921")
TabSelector.Position = TitleHolder.Position + Vector2.new(0, 18)
TabSelector.Size = Vector2.new(181, 307)
TabSelector.Filled = true

-- SettingsHolder (Square)
local SettingsHolder = Drawing.new("Square")
SettingsHolder.Visible = true
SettingsHolder.Transparency = 0.5
SettingsHolder.ZIndex = 0
SettingsHolder.Color = Color3.fromHex("#000000")
SettingsHolder.Position = TitleHolder.Position + Vector2.new(182, 8)
SettingsHolder.Size = Vector2.new(321, 317)
SettingsHolder.Filled = true

-- GuiName (Text)
local GuiName = Drawing.new("Text")
GuiName.Visible = true
GuiName.Transparency = 1
GuiName.ZIndex = 40
GuiName.Color = Color3.fromHex("#FFFFFF")
GuiName.Position = TitleHolder.Position + Vector2.new(6, 0)
GuiName.Text = "Operation One"
GuiName.Size = 25
GuiName.Center = false
GuiName.Outline = false
GuiName.Font = Drawing.Fonts.SystemBold

-- VisualTab (Button)
local VisualTab = Drawing.new("Square")
VisualTab.Visible = true
VisualTab.Transparency = 1
VisualTab.ZIndex = 60
VisualTab.Color = Color3.fromHex("#344a60")
VisualTab.Position = TitleHolder.Position + Vector2.new(37.5, 60)
VisualTab.Size = Vector2.new(106, 37)
VisualTab.Filled = true
VisualTab.Corner = 9

local VisualTab_Text = Drawing.new("Text")
VisualTab_Text.Text = "Visuals"
VisualTab_Text.Size = 28
VisualTab_Text.Center = true
VisualTab_Text.Outline = true
VisualTab_Text.Font = 1
VisualTab_Text.Color = Color3.fromHex("#ffffff")
VisualTab_Text.Position = VisualTab.Position + Vector2.new(106/2, 37/2)
VisualTab_Text.Visible = true
VisualTab_Text.ZIndex = 62

-- PlayerEspEnable (Checkbox)

-- Checkbox PlayerEspEnable
local PlayerEspEnable = Drawing.new("Square")
PlayerEspEnable.Visible = true
PlayerEspEnable.Transparency = 1
PlayerEspEnable.Color = Color3.fromHex("#808080")
PlayerEspEnable.Thickness = 3
PlayerEspEnable.Filled = false
PlayerEspEnable.Size = Vector2.new(20, 20)
PlayerEspEnable.Position = Vector2.new(272, 106)
PlayerEspEnable.ZIndex = 81
PlayerEspEnable.Corner = 25
local PlayerEspEnable_Inner = Drawing.new("Square")
PlayerEspEnable_Inner.Visible = true and PlayerEspEnable_IsChecked
PlayerEspEnable_Inner.Transparency = 1
PlayerEspEnable_Inner.Color = Color3.fromHex("#07a5f0")
PlayerEspEnable_Inner.Filled = true
PlayerEspEnable_Inner.Size = PlayerEspEnable.Size
PlayerEspEnable_Inner.Position = PlayerEspEnable.Position
PlayerEspEnable_Inner.ZIndex = 80
PlayerEspEnable_Inner.Corner = 25
local PlayerEspEnable_Label = Drawing.new("Text")
PlayerEspEnable_Label.Visible = true
PlayerEspEnable_Label.Text = "Player Esp"
PlayerEspEnable_Label.Size = 24
PlayerEspEnable_Label.Outline = true
PlayerEspEnable_Label.Font = 2
PlayerEspEnable_Label.Color = Color3.fromHex("#FFFFFF")
PlayerEspEnable_Label.Position = PlayerEspEnable.Position + Vector2.new(25, -2)
PlayerEspEnable_Label.ZIndex = 80

-- EspTogglesHolder (Square)
local EspTogglesHolder = Drawing.new("Square")
EspTogglesHolder.Visible = true
EspTogglesHolder.Transparency = 1
EspTogglesHolder.ZIndex = 70
EspTogglesHolder.Color = Color3.fromHex("#050d1a")
EspTogglesHolder.Position = TitleHolder.Position + Vector2.new(189, 51)
EspTogglesHolder.Size = Vector2.new(200, 145)
EspTogglesHolder.Filled = true
EspTogglesHolder.Corner = 10

-- Checkbox13 (Checkbox)

-- Checkbox Checkbox13
local Checkbox13 = Drawing.new("Square")
Checkbox13.Visible = true
Checkbox13.Transparency = 1
Checkbox13.Color = Color3.fromHex("#808080")
Checkbox13.Thickness = 3
Checkbox13.Filled = false
Checkbox13.Size = Vector2.new(20, 20)
Checkbox13.Position = Vector2.new(272, 147)
Checkbox13.ZIndex = 81
Checkbox13.Corner = 25
local Checkbox13_Inner = Drawing.new("Square")
Checkbox13_Inner.Visible = true and Checkbox13_IsChecked
Checkbox13_Inner.Transparency = 1
Checkbox13_Inner.Color = Color3.fromHex("#07a5f0")
Checkbox13_Inner.Filled = true
Checkbox13_Inner.Size = Checkbox13.Size
Checkbox13_Inner.Position = Checkbox13.Position
Checkbox13_Inner.ZIndex = 80
Checkbox13_Inner.Corner = 25
local Checkbox13_Label = Drawing.new("Text")
Checkbox13_Label.Visible = true
Checkbox13_Label.Text = "Bomb Esp"
Checkbox13_Label.Size = 24
Checkbox13_Label.Outline = true
Checkbox13_Label.Font = 2
Checkbox13_Label.Color = Color3.fromHex("#FFFFFF")
Checkbox13_Label.Position = Checkbox13.Position + Vector2.new(25, -2)
Checkbox13_Label.ZIndex = 80

local KeyNames = {
    [48] = "0",
    [49] = "1",
    [50] = "2",
    [51] = "3",
    [52] = "4",
    [53] = "5",
    [54] = "6",
    [55] = "7",
    [56] = "8",
    [57] = "9",
    [1] = "LeftMouse",
    [2] = "RightMouse",
    [4] = "MiddleMouse",
    [8] = "Backspace",
    [9] = "Tab",
    [13] = "Enter",
    [16] = "Shift",
    [17] = "Ctrl",
    [18] = "Alt",
    [19] = "Pause",
    [20] = "CapsLock",
    [27] = "Esc",
    [32] = "Space",
    [33] = "PageUp",
    [34] = "PageDown",
    [35] = "End",
    [36] = "Home",
    [37] = "Left",
    [38] = "Up",
    [39] = "Right",
    [40] = "Down",
    [45] = "Insert",
    [46] = "Delete",
    [65] = "A",
    [66] = "B",
    [67] = "C",
    [68] = "D",
    [69] = "E",
    [70] = "F",
    [71] = "G",
    [72] = "H",
    [73] = "I",
    [74] = "J",
    [75] = "K",
    [76] = "L",
    [77] = "M",
    [78] = "N",
    [79] = "O",
    [80] = "P",
    [81] = "Q",
    [82] = "R",
    [83] = "S",
    [84] = "T",
    [85] = "U",
    [86] = "V",
    [87] = "W",
    [88] = "X",
    [89] = "Y",
    [90] = "Z",
    [112] = "F1",
    [113] = "F2",
    [114] = "F3",
    [115] = "F4",
    [116] = "F5",
    [117] = "F6",
    [118] = "F7",
    [119] = "F8",
    [120] = "F9",
    [121] = "F10",
    [122] = "F11",
    [123] = "F12",
}

-- Input Handling
local dragging = nil
local dragStart = nil
local startPos = nil
local knobStartPos = nil
local lastMouse1 = false

while true do
    wait(0.01)
    if isrbxactive() then
        local mouse1 = ismouse1pressed()
        local mPos = Vector2.new(Mouse.X, Mouse.Y)

		if PlayerEspEnable_IsChecked then
            drawPlayers()
        else
            clearAllPlayerESP()
        end
        
        -- Bomb ESP
        if Checkbox13_IsChecked then
            drawBomb()
        else
            hideAllBombESP()
        end

        -- Mouse Down (Just Pressed)
        if mouse1 and not lastMouse1 then
            -- Button VisualTab
            if VisualTab.Visible and mPos.X >= VisualTab.Position.X and mPos.X <= VisualTab.Position.X + VisualTab.Size.X and
               mPos.Y >= VisualTab.Position.Y and mPos.Y <= VisualTab.Position.Y + VisualTab.Size.Y then
                pcall(function() onClick() end)
            end
            -- Button PlayerEspEnable
            if PlayerEspEnable.Visible and mPos.X >= PlayerEspEnable.Position.X and mPos.X <= PlayerEspEnable.Position.X + PlayerEspEnable.Size.X and
               mPos.Y >= PlayerEspEnable.Position.Y and mPos.Y <= PlayerEspEnable.Position.Y + PlayerEspEnable.Size.Y then
                -- Toggle Checkbox
                PlayerEspEnable_IsChecked = not PlayerEspEnable_IsChecked
                PlayerEspEnable_Inner.Visible = PlayerEspEnable_IsChecked
                if onToggle then pcall(function() onToggle(PlayerEspEnable_IsChecked) end) end
            end
            -- Button Checkbox13
            if Checkbox13.Visible and mPos.X >= Checkbox13.Position.X and mPos.X <= Checkbox13.Position.X + Checkbox13.Size.X and
               mPos.Y >= Checkbox13.Position.Y and mPos.Y <= Checkbox13.Position.Y + Checkbox13.Size.Y then
                -- Toggle Checkbox
                Checkbox13_IsChecked = not Checkbox13_IsChecked
                Checkbox13_Inner.Visible = Checkbox13_IsChecked
                if onToggle then pcall(function() onToggle(Checkbox13_IsChecked) end) end
            end
            -- Drag TitleHolder
            if TitleHolder.Visible and mPos.X >= TitleHolder.Position.X and mPos.X <= TitleHolder.Position.X + TitleHolder.Size.X and
               mPos.Y >= TitleHolder.Position.Y and mPos.Y <= TitleHolder.Position.Y + TitleHolder.Size.Y then
                dragging = TitleHolder
                dragStart = mPos
                startPos = TitleHolder.Position
            end
        end

        -- Mouse Up (Just Released)
        if not mouse1 and lastMouse1 then
            dragging = nil
        end

        -- Dragging Update
        if dragging and mouse1 then
            local delta = mPos - dragStart
            dragging.Position = startPos + delta
            if dragging == TitleHolder then
                TitleHolder_Border.Position = dragging.Position
                TabSelector.Position = dragging.Position + Vector2.new(0, 18)
                SettingsHolder.Position = dragging.Position + Vector2.new(182, 8)
                GuiName.Position = dragging.Position + Vector2.new(6, 0)
                VisualTab.Position = dragging.Position + Vector2.new(37.5, 60)
                VisualTab_Text.Position = VisualTab.Position + Vector2.new(106/2, 37/2)
                PlayerEspEnable.Position = dragging.Position + Vector2.new(195, 60)
                PlayerEspEnable_Label.Position = PlayerEspEnable.Position + Vector2.new(25, -2)
                PlayerEspEnable_Inner.Position = PlayerEspEnable.Position
                EspTogglesHolder.Position = dragging.Position + Vector2.new(189, 51)
                Checkbox13.Position = dragging.Position + Vector2.new(195, 101)
                Checkbox13_Label.Position = Checkbox13.Position + Vector2.new(25, -2)
                Checkbox13_Inner.Position = Checkbox13.Position
            end
        end

        lastMouse1 = mouse1
    end
end
