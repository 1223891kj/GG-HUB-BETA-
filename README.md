-- GG HUB [BETA] Script

-- Criar a interface do Hub
local ScreenGui = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local OpenCloseButton = Instance.new("TextButton")
local PlayerListFrame = Instance.new("Frame")
local PlayerList = Instance.new("ScrollingFrame")
local RefreshButton = Instance.new("TextButton")

-- Configurar a interface
ScreenGui.Name = "GGHub"
ScreenGui.Parent = game.CoreGui

MainFrame.Name = "MainFrame"
MainFrame.Parent = ScreenGui
MainFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
MainFrame.Position = UDim2.new(0.5, -200, 0.5, -150)
MainFrame.Size = UDim2.new(0, 400, 0, 300)
MainFrame.Visible = false

OpenCloseButton.Name = "OpenCloseButton"
OpenCloseButton.Parent = ScreenGui
OpenCloseButton.BackgroundColor3 = Color3.fromRGB(0, 0, 255)
OpenCloseButton.Position = UDim2.new(0, 10, 0, 10)
OpenCloseButton.Size = UDim2.new(0, 100, 0, 50)
OpenCloseButton.Text = "Abrir GG HUB"

PlayerListFrame.Name = "PlayerListFrame"
PlayerListFrame.Parent = MainFrame
PlayerListFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
PlayerListFrame.Position = UDim2.new(0, 10, 0, 10)
PlayerListFrame.Size = UDim2.new(0, 380, 0, 200)

PlayerList.Name = "PlayerList"
PlayerList.Parent = PlayerListFrame
PlayerList.BackgroundColor3 = Color3.fromRGB(200, 200, 200)
PlayerList.Size = UDim2.new(1, 0, 1, 0)
PlayerList.CanvasSize = UDim2.new(0, 0, 2, 0)

RefreshButton.Name = "RefreshButton"
RefreshButton.Parent = MainFrame
RefreshButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
RefreshButton.Position = UDim2.new(0, 10, 0, 220)
RefreshButton.Size = UDim2.new(0, 100, 0, 50)
RefreshButton.Text = "Atualizar Lista"

-- Função para abrir e fechar o Hub
OpenCloseButton.MouseButton1Click:Connect(function()
    MainFrame.Visible = not MainFrame.Visible
end)

-- Função para atualizar a lista de jogadores
local function updatePlayerList()
    PlayerList:ClearAllChildren()
    for _, player in pairs(game.Players:GetPlayers()) do
        local playerButton = Instance.new("TextButton")
        playerButton.Size = UDim2.new(1, -10, 0, 30)
        playerButton.Position = UDim2.new(0, 5, 0, (#PlayerList:GetChildren() - 1) * 35)
        playerButton.Text = player.Name
        playerButton.Parent = PlayerList

        -- Função para flingar o jogador com o sofá
        playerButton.MouseButton1Click:Connect(function()
            local character = player.Character
            if character then
                local sofa = Instance.new("Part")
                sofa.Size = Vector3.new(2, 1, 1)
                sofa.Position = character.HumanoidRootPart.Position + Vector3.new(0, 5, 0)
                sofa.Parent = workspace
                local bodyVelocity = Instance.new("BodyVelocity")
                bodyVelocity.Velocity = Vector3.new(0, 100, 0)
                bodyVelocity.Parent = sofa
                game.Debris:AddItem(sofa, 2)
            end
        end)
    end
end

-- Conectar a função de atualizar lista ao botão
RefreshButton.MouseButton1Click:Connect(updatePlayerList)

-- Atualizar a lista de jogadores ao iniciar
updatePlayerList()

