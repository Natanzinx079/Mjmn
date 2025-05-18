-- Coloque esse script em StarterGui (LocalScript)
local player = game.Players.LocalPlayer
local gui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
gui.Name = "NatHub"

-- Janela Principal
local mainFrame = Instance.new("Frame", gui)
mainFrame.Size = UDim2.new(0, 400, 0, 300)
mainFrame.Position = UDim2.new(0.5, -200, 0.5, -150)
mainFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
mainFrame.BorderSizePixel = 0
mainFrame.Active = true
mainFrame.Draggable = true

-- Título
local title = Instance.new("TextLabel", mainFrame)
title.Size = UDim2.new(1, 0, 0, 40)
title.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
title.Text = "NatHub | Dead Rails (0.3.1)"
title.Font = Enum.Font.SourceSansBold
title.TextSize = 20
title.TextColor3 = Color3.new(1, 1, 1)

-- Abas laterais
local tabs = {"Main", "Character", "Teleport", "Visual", "Combat", "Configuration"}
local tabButtons = {}

for i, tabName in ipairs(tabs) do
    local button = Instance.new("TextButton", mainFrame)
    button.Size = UDim2.new(0, 120, 0, 30)
    button.Position = UDim2.new(0, 0, 0, 40 + (i - 1) * 32)
    button.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
    button.Text = tabName
    button.TextColor3 = Color3.new(1, 1, 1)
    button.Font = Enum.Font.SourceSans
    button.TextSize = 16
    tabButtons[tabName] = button
end

-- Conteúdo das Abas
local contentFrames = {}

local function createContentFrame(name)
    local frame = Instance.new("Frame", mainFrame)
    frame.Name = name
    frame.Position = UDim2.new(0, 130, 0, 40)
    frame.Size = UDim2.new(1, -130, 1, -40)
    frame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
    frame.Visible = false
    contentFrames[name] = frame
    return frame
end

for _, name in ipairs(tabs) do
    createContentFrame(name)
end

-- Mostrar aba selecionada
local function showTab(tabName)
    for name, frame in pairs(contentFrames) do
        frame.Visible = (name == tabName)
    end
end

-- Conectar botões às abas
for name, button in pairs(tabButtons) do
    button.MouseButton1Click:Connect(function()
        showTab(name)
    end)
end

-- Ativar aba Main por padrão
showTab("Main")

-- Conteúdo da aba Main
local mainTab = contentFrames["Main"]

-- Webhook Box
local webhookBox = Instance.new("TextBox", mainTab)
webhookBox.Size = UDim2.new(0, 220, 0, 30)
webhookBox.Position = UDim2.new(0, 10, 0, 10)
webhookBox.PlaceholderText = "Your Webhook Link"
webhookBox.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
webhookBox.TextColor3 = Color3.new(1, 1, 1)

-- Auto Bond Toggle
local autoBond = Instance.new("TextButton", mainTab)
autoBond.Size = UDim2.new(0, 150, 0, 30)
autoBond.Position = UDim2.new(0, 10, 0, 50)
autoBond.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
autoBond.Text = "Auto Bond: OFF"
autoBond.TextColor3 = Color3.new(1, 1, 1)
autoBond.MouseButton1Click:Connect(function()
    local state = autoBond.Text:find("OFF") and "ON" or "OFF"
    autoBond.Text = "Auto Bond: " .. state
    -- Aqui você pode colocar a função de coleta segura (legítima)
end)

-- Auto Win Botão
local autoWin = Instance.new("TextButton", mainTab)
autoWin.Size = UDim2.new(0, 150, 0, 30)
autoWin.Position = UDim2.new(0, 10, 0, 90)
autoWin.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
autoWin.Text = "Auto Win"
autoWin.TextColor3 = Color3.new(1, 1, 1)
autoWin.MouseButton1Click:Connect(function()
    print("Simulando vitória legítima...")
    -- Aqui você pode inserir lógica legítima do jogo (sem abusos)
end)
