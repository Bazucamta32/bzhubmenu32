local Players = game:GetService("Players")
local Player = Players.LocalPlayer
local PlayerGui = Player:FindFirstChildOfClass("PlayerGui")
local TweenService = game:GetService("TweenService")
local Workspace = game:GetService("Workspace")

-- Criando a ScreenGui
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Parent = PlayerGui

-- Criando o Frame do Menu
local Frame = Instance.new("Frame")
Frame.Size = UDim2.new(0, 250, 0, 150)
Frame.Position = UDim2.new(0.5, -125, 0.3, 0)
Frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
Frame.BorderSizePixel = 2
Frame.Parent = ScreenGui

-- Criando o título RGB "Bazuca Hub"
local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(1, 0, 0, 30)
Title.Position = UDim2.new(0, 0, 0, 0)
Title.Text = "Bazuca Hub"
Title.TextSize = 20
Title.Font = Enum.Font.SourceSansBold
Title.Parent = Frame

-- Função para RGB no título
spawn(function()
    while true do
        for i = 0, 1, 0.01 do
            Title.TextColor3 = Color3.fromHSV(i, 1, 1)
            wait(0.05)
        end
    end
end)

-- Criando o botão Auto Farm
local AutoFarmButton = Instance.new("TextButton")
AutoFarmButton.Size = UDim2.new(1, -20, 0, 30)
AutoFarmButton.Position = UDim2.new(0, 10, 0, 40)
AutoFarmButton.Text = "Auto Farm"
AutoFarmButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
AutoFarmButton.TextColor3 = Color3.fromRGB(255, 255, 255)
AutoFarmButton.Parent = Frame

-- Criando o botão Chest Farm
local ChestFarmButton = Instance.new("TextButton")
ChestFarmButton.Size = UDim2.new(1, -20, 0, 30)
ChestFarmButton.Position = UDim2.new(0, 10, 0, 80)
ChestFarmButton.Text = "Chest Farm: false"
ChestFarmButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
ChestFarmButton.TextColor3 = Color3.fromRGB(255, 255, 255)
ChestFarmButton.Parent = Frame

local chestFarmActive = false

ChestFarmButton.MouseButton1Click:Connect(function()
    chestFarmActive = not chestFarmActive
    ChestFarmButton.Text = "Chest Farm: " .. tostring(chestFarmActive)
    
    if chestFarmActive then
        local chests = Workspace:FindFirstChild("Chest")
        if chests then
            for _, chest in pairs(chests:GetChildren()) do
                if chest:IsA("Model") and chest.Name == "Chest1" then
                    Player.Character:SetPrimaryPartCFrame(chest.PrimaryPart.CFrame)
                    wait(0.5) 
                end
            end
            
            local message = Instance.new("TextLabel")
            message.Size = UDim2.new(0, 200, 0, 50)
            message.Position = UDim2.new(0.5, -100, 0.8, 0)
            message.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
            message.TextColor3 = Color3.fromRGB(255, 255, 255)
            message.Text = "As Chests acabaram!"
            message.Parent = ScreenGui
            
            wait(4)
            message:Destroy()
        end
    end
end)

-- Criando o botão Fechar
local CloseButton = Instance.new("TextButton")
CloseButton.Size = UDim2.new(0, 30, 0, 30)
CloseButton.Position = UDim2.new(1, -35, 0, 0)
CloseButton.Text = "X"
CloseButton.BackgroundColor3 = Color3.fromRGB(200, 0, 0)
CloseButton.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseButton.Parent = Frame
CloseButton.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)

-- Criando o botão Minimizar
local MinimizeButton = Instance.new("TextButton")
MinimizeButton.Size = UDim2.new(0, 30, 0, 30)
MinimizeButton.Position = UDim2.new(1, -70, 0, 0)
MinimizeButton.Text = "-"
MinimizeButton.BackgroundColor3 = Color3.fromRGB(200, 200, 0)
MinimizeButton.TextColor3 = Color3.fromRGB(0, 0, 0)
MinimizeButton.Parent = Frame
MinimizeButton.MouseButton1Click:Connect(function()
    Frame.Visible = not Frame.Visible
end)
