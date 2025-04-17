-- By Hixdow

-- Função para Auto Kill (Sea Beast e todos os Bosses)
local function autoKillBoss(boss)
    while true do
        if boss and boss:FindFirstChild("Humanoid") then
            boss.Humanoid.Health = 0
        end
        wait(1)
    end
end

-- Função para Auto Farm Instantâneo (Risco de Banimento)
local function autoFarm()
    while true do
        local seaBeast = game.Workspace:FindFirstChild("SeaBeast")
        if seaBeast then
            autoKillBoss(seaBeast)
        end
        wait(1)
    end
end

-- Função de entrada (Intro) no script
local function showIntro()
    local introGui = Instance.new("ScreenGui")
    introGui.Name = "IntroGUI"
    introGui.Parent = game.Players.LocalPlayer.PlayerGui

    local introText = Instance.new("TextLabel")
    introText.Size = UDim2.new(0.5, 0, 0.1, 0)
    introText.Position = UDim2.new(0.25, 0, 0.45, 0)
    introText.BackgroundTransparency = 1
    introText.Text = "Script By Hixdow"
    introText.TextColor3 = Color3.fromRGB(255, 255, 255)
    introText.Font = Enum.Font.SourceSans
    introText.TextSize = 48
    introText.Parent = introGui

    wait(2) -- Exibe o texto por 2 segundos
    introGui:Destroy()
end

-- Exibe a cena de entrada quando o script é iniciado
showIntro()

-- Funções de UI para Controles de Auto Farm e Auto Kill
local ui = Instance.new("ScreenGui")
ui.Name = "ScriptUI"
ui.Parent = game.Players.LocalPlayer.PlayerGui

local toggleFarmButton = Instance.new("TextButton")
toggleFarmButton.Size = UDim2.new(0.2, 0, 0.1, 0)
toggleFarmButton.Position = UDim2.new(0.4, 0, 0.8, 0)
toggleFarmButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
toggleFarmButton.Text = "Toggle Auto Farm"
toggleFarmButton.Font = Enum.Font.SourceSans
toggleFarmButton.TextSize = 24
toggleFarmButton.Parent = ui

local toggleKillButton = Instance.new("TextButton")
toggleKillButton.Size = UDim2.new(0.2, 0, 0.1, 0)
toggleKillButton.Position = UDim2.new(0.7, 0, 0.8, 0)
toggleKillButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
toggleKillButton.Text = "Toggle Auto Kill"
toggleKillButton.Font = Enum.Font.SourceSans
toggleKillButton.TextSize = 24
toggleKillButton.Parent = ui

local autoFarmActive = false
local autoKillActive = false

-- Toggle Auto Farm
toggleFarmButton.MouseButton1Click:Connect(function()
    autoFarmActive = not autoFarmActive
    if autoFarmActive then
        toggleFarmButton.BackgroundColor3 = Color3.fromRGB(255, 255, 0)
        spawn(autoFarm)
    else
        toggleFarmButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
    end
end)

-- Toggle Auto Kill
toggleKillButton.MouseButton1Click:Connect(function()
    autoKillActive = not autoKillActive
    if autoKillActive then
        toggleKillButton.BackgroundColor3 = Color3.fromRGB(255, 255, 0)
        -- Adicione as funções de auto kill para os bosses desejados aqui
    else
        toggleKillButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
    end
end)
