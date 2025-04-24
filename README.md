

local player = game.Players.LocalPlayer
local mouse = player:GetMouse()
local autoClickActive = false
local clickInterval = 0.1 -- Intervalo entre cliques em segundos
local clickConnection

-- Criação do botão
local screenGui = Instance.new("ScreenGui", player.PlayerGui)
local clickButton = Instance.new("TextButton", screenGui)
clickButton.Size = UDim2.new(0, 200, 0, 50)
clickButton.Position = UDim2.new(0.5, -100, 0.5, -25)
clickButton.Text = "Iniciar Auto Click"
clickButton.BackgroundColor3 = Color3.new(0, 1, 0) -- Verde

local function toggleAutoClick()
    autoClickActive = not autoClickActive

    if autoClickActive then
        clickButton.Text = "Parar Auto Click"
        clickButton.BackgroundColor3 = Color3.new(1, 0, 0) -- Vermelho
        clickConnection = game:GetService("RunService").Heartbeat:Connect(function()
            mouse:Click()
        end)
    else
        clickButton.Text = "Iniciar Auto Click"
        clickButton.BackgroundColor3 = Color3.new(0, 1, 0) -- Verde
        if clickConnection then
            clickConnection:Disconnect()
            clickConnection = nil
        end
    end
end

clickButton.MouseButton1Click:Connect(toggleAutoClick)
