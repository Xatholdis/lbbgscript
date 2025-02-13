local LBBattlegrounds = Instance.new("ScreenGui")
local BG = Instance.new("Frame")
local TitleLabel = Instance.new("TextLabel")  -- Create a TextLabel for the title
TitleLabel.Parent = BG  -- Set the parent to BG to place it in the background frame
TitleLabel.BackgroundTransparency = 1  -- Make the background transparent
TitleLabel.Size = UDim2.new(0, 661, 0, 50)  -- Set the size (same width as BG, adjust height)
TitleLabel.Position = UDim2.new(0, 0, 0, 27)  -- Move it 7 pixels lower (from 20 to 27)
TitleLabel.Font = Enum.Font.SourceSansBold  -- Choose a bold font for emphasis
TitleLabel.Text = "Lucky Block Battlegrounds Hub"  -- The main title text
TitleLabel.TextSize = 24  -- Set the text size for the main title
TitleLabel.TextColor3 = Color3.fromRGB(255, 255, 255)  -- White text color
TitleLabel.TextScaled = true  -- Make the text scale properly
TitleLabel.TextWrapped = true  -- Allow the text to wrap if needed

-- Add a smaller label for "by Xatholdis"
local ByLabel = Instance.new("TextLabel")  -- Create a smaller TextLabel for "by Xatholdis"
ByLabel.Parent = BG  -- Set the parent to BG to place it in the background frame
ByLabel.BackgroundTransparency = 1  -- Make the background transparent
ByLabel.Size = UDim2.new(0, 661, 0, 25)  -- Set the size (same width as BG, smaller height)
ByLabel.Position = UDim2.new(0, 0, 0, 70)  -- Position it a bit lower, below the main title
ByLabel.Font = Enum.Font.SourceSans  -- Use a regular font for the smaller text
ByLabel.Text = "by Xatholdis"  -- The smaller text
ByLabel.TextSize = 16  -- Set the smaller text size
ByLabel.TextColor3 = Color3.fromRGB(255, 255, 255)  -- White text color
ByLabel.TextScaled = true  -- Make the text scale properly
ByLabel.TextWrapped = true  -- Allow the text to wrap if needed
local Exit = Instance.new("TextButton")
local Minimize = Instance.new("TextButton")
local ActivateAll = Instance.new("TextButton")
local UICorner = Instance.new("UICorner")
local LuckyBlock = Instance.new("TextButton")
local SuperLuckyBlock = Instance.new("TextButton")
local DiamondLuckyBlock = Instance.new("TextButton")
local RainbowLuckyBlock = Instance.new("TextButton")
local GalaxyLuckyBlock = Instance.new("TextButton")

LBBattlegrounds.Name = "LB Battlegrounds"
LBBattlegrounds.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
LBBattlegrounds.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

BG.Name = "BG"
BG.Parent = LBBattlegrounds
BG.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
BG.BorderColor3 = Color3.fromRGB(141, 14, 14)
BG.BorderSizePixel = 4
BG.Position = UDim2.new(0.258, 0, 0.231, 0)
BG.Size = UDim2.new(0, 661, 0, 314)

Exit.Name = "Exit"
Exit.Parent = BG
Exit.BackgroundColor3 = Color3.fromRGB(161, 161, 161)
Exit.Position = UDim2.new(0.013, 0, 0.025, 0)
Exit.Size = UDim2.new(0, 22, 0, 21)
Exit.Font = Enum.Font.SourceSans
Exit.Text = "X"
Exit.TextColor3 = Color3.fromRGB(0, 0, 0)
Exit.TextScaled = true
Exit.TextWrapped = true

UICorner.CornerRadius = UDim.new(1, 0)
UICorner.Parent = Exit

Minimize.Name = "Minimize"
Minimize.Parent = BG
Minimize.BackgroundColor3 = Color3.fromRGB(161, 161, 161)
Minimize.Position = UDim2.new(0.06, 0, 0.025, 0)
Minimize.Size = UDim2.new(0, 22, 0, 21)
Minimize.Font = Enum.Font.SourceSans
Minimize.Text = "-"
Minimize.TextColor3 = Color3.fromRGB(0, 0, 0)
Minimize.TextScaled = true
Minimize.TextWrapped = true

UICorner:Clone().Parent = Minimize

ActivateAll.Name = "ActivateAll"
ActivateAll.Parent = BG
ActivateAll.BackgroundColor3 = Color3.fromRGB(83, 83, 83)  -- Same color as other buttons
ActivateAll.Position = UDim2.new(0.670, 0, 0.622, 0)  -- Position it near the Galaxy button (same Y position)
ActivateAll.Size = UDim2.new(0, 200, 0, 50)  -- Same size as the other buttons
ActivateAll.Font = Enum.Font.Oswald  -- Same font as other buttons
ActivateAll.Text = "Give Void"  -- Text
ActivateAll.TextColor3 = Color3.fromRGB(0, 0, 0)  -- Text color
ActivateAll.TextScaled = true  -- Text scaling
ActivateAll.TextWrapped = true  -- Text wrapping

-- Variables to track dragging state
local dragging = false
local dragInput, mousePos, mouseDelta

-- Function to start dragging
BG.InputBegan:Connect(function(input, gameProcessed)
    if gameProcessed then return end  -- Ignore input if the game has already processed it
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = true
        mousePos = input.Position  -- Get the initial mouse position
        -- Start dragging the GUI
        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then
                dragging = false
            end
        end)
    end
end)

-- Function to update the position while dragging
BG.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement and dragging then
        -- Calculate how much the mouse has moved
        mouseDelta = input.Position - mousePos
        BG.Position = UDim2.new(0, BG.Position.X.Offset + mouseDelta.X, 0, BG.Position.Y.Offset + mouseDelta.Y)
        mousePos = input.Position  -- Update the mouse position
    end
end)

local isMinimized = false

Minimize.MouseButton1Click:Connect(function()
    isMinimized = not isMinimized
    if isMinimized then
        BG.Size = UDim2.new(0, 50, 0, 50)
        TitleLabel.Visible = false  -- Hide the title when minimized
        ByLabel.Visible = false    -- Hide the subtitle when minimized
    else
        BG.Size = UDim2.new(0, 661, 0, 314)
        TitleLabel.Visible = true  -- Show the title when restored
        ByLabel.Visible = true    -- Show the subtitle when restored
    end
    for _, child in ipairs(BG:GetChildren()) do
        if child:IsA("TextButton") and child ~= Minimize and child ~= Exit then
            child.Visible = not isMinimized
        end
    end
end)

Exit.MouseButton1Click:Connect(function()
    LBBattlegrounds:Destroy()
end)

local function createButton(button, parent, position, text, event)
    button.Parent = parent
    button.BackgroundColor3 = Color3.fromRGB(83, 83, 83)
    button.Position = position
    button.Size = UDim2.new(0, 200, 0, 50)
    button.Font = Enum.Font.Oswald
    button.Text = text
    button.TextColor3 = Color3.fromRGB(0, 0, 0)
    button.TextScaled = true
    button.TextWrapped = true
    button.MouseButton1Click:Connect(event)
end

createButton(LuckyBlock, BG, UDim2.new(0.028, 0, 0.418, 0), "Give LuckyBlock", function()
    game.ReplicatedStorage.SpawnLuckyBlock:FireServer()
end)

createButton(SuperLuckyBlock, BG, UDim2.new(0.348, 0, 0.418, 0), "Give Super", function()
    game.ReplicatedStorage.SpawnSuperBlock:FireServer()
end)

createButton(DiamondLuckyBlock, BG, UDim2.new(0.670, 0, 0.418, 0), "Give Diamond", function()
    game.ReplicatedStorage.SpawnDiamondBlock:FireServer()
end)

createButton(RainbowLuckyBlock, BG, UDim2.new(0.027, 0, 0.622, 0), "Give Rainbow", function()
    game.ReplicatedStorage.SpawnRainbowBlock:FireServer()
end)

createButton(GalaxyLuckyBlock, BG, UDim2.new(0.348, 0, 0.622, 0), "Give Galaxy", function()
    game.ReplicatedStorage.SpawnGalaxyBlock:FireServer()
end)

ActivateAll.MouseButton1Click:Connect(function()
    game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        	 
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        	 
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        	 
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        	 
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnGalaxyBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()
	game:GetService("ReplicatedStorage").SpawnRainbowBlock:FireServer()        
end)
