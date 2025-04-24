
local loja = {}
local inventario = {}

-- Função para adicionar itens à loja
function adicionarItem(nome, preco)
    local item = { nome = nome, preco = preco }
    table.insert(loja, item)
end

-- Função para exibir os itens da loja
function exibirLoja()
    print("Itens disponíveis na loja:")
    for i, item in ipairs(loja) do
        print(i .. ". " .. item.nome .. " - " .. (item.preco == 0 and "Grátis" or item.preco .. " Robux"))
    end
end

-- Função para adicionar um item ao inventário
function adicionarAoInventario(itemNome)
    table.insert(inventario, itemNome)
    print(itemNome .. " foi adicionado ao seu inventário!")
end

-- Função para executar a compra do item
function executarCompra(itemIndex)
    local item = loja[itemIndex]
    if item and item.preco == 0 then
        adicionarAoInventario(item.nome)
    else
        print("Item inválido ou não é grátis.")
    end
end

-- Adicionando o item "Dark Blade" à loja como gratuito
adicionarItem("Dark Blade", 0)

-- Exibindo a loja
exibirLoja()

-- Executando a compra do item "Dark Blade"
executarCompra(1)  -- Aqui, 1 é o índice do item "Dark Blade"




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
