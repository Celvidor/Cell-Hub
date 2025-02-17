local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local UIS = game:GetService("UserInputService")

-- Создание GUI
local ScreenGui = Instance.new("ScreenGui", game.CoreGui)
local FloatingButton = Instance.new("ImageButton", ScreenGui)
local Frame = Instance.new("Frame", ScreenGui)
local TextBox = Instance.new("TextBox", Frame)
local TeleportButton = Instance.new("TextButton", Frame)
local CloseButton = Instance.new("TextButton", Frame)

-- Настройка кнопки (иконки)
FloatingButton.Size = UDim2.new(0, 60, 0, 60)
FloatingButton.Position = UDim2.new(0.8, 0, 0.2, 0) 
FloatingButton.BackgroundTransparency = 1
FloatingButton.Image = "rbxassetid://6031068420" -- Иконка (можно заменить)

-- Настройка окна меню
Frame.Size = UDim2.new(0, 250, 0, 150)
Frame.Position = UDim2.new(0.35, 0, 0.35, 0)
Frame.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
Frame.Visible = false

-- Поле для ввода ника
TextBox.Size = UDim2.new(0, 230, 0, 30)
TextBox.Position = UDim2.new(0, 10, 0, 10)
TextBox.PlaceholderText = "Введите ник..."
TextBox.TextScaled = true
TextBox.Parent = Frame

-- Кнопка телепортации
TeleportButton.Size = UDim2.new(0, 230, 0, 40)
TeleportButton.Position = UDim2.new(0, 10, 0, 50)
TeleportButton.Text = "Телепортироваться"
TeleportButton.BackgroundColor3 = Color3.fromRGB(0, 200, 0)
TeleportButton.Parent = Frame

-- Кнопка закрытия
CloseButton.Size = UDim2.new(0, 230, 0, 30)
CloseButton.Position = UDim2.new(0, 10, 0, 100)
CloseButton.Text = "Закрыть"
CloseButton.BackgroundColor3 = Color3.fromRGB(200, 0, 0)
CloseButton.Parent = Frame

-- Функция телепортации
TeleportButton.MouseButton1Click:Connect(function()
    local targetName = TextBox.Text
    local targetPlayer = Players:FindFirstChild(targetName)
    
    if targetPlayer and targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
        LocalPlayer.Character.HumanoidRootPart.CFrame = targetPlayer.Character.HumanoidRootPart.CFrame
    else
        warn("Игрок не найден!")
    end
end)

-- Открытие меню
FloatingButton.MouseButton1Click:Connect(function()
    Frame.Visible = not Frame.Visible
end)

-- Закрытие меню
CloseButton.MouseButton1Click:Connect(function()
    Frame.Visible = false
end)

-- Движение иконки (адаптировано для телефона)
local dragging = false
local dragInput, dragStart, startPos

FloatingButton.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.Touch or input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = true
        dragStart = input.Position
        startPos = FloatingButton.Position
        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then
                dragging = false
            end
        end)
    end
end)

FloatingButton.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.Touch or input.UserInputType == Enum.UserInputType.MouseMovement then
        dragInput = input
    end
end)

UIS.InputChanged:Connect(function(input)
    if input == dragInput and dragging then
        local delta = input.Position - dragStart
        FloatingButton.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
    end
end)
