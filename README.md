--Abaixo esta nossa lib 

local Lib = loadstring(game:HttpGet("https://raw.githubusercontent.com/7yhx/kwargs_Ui_Library/main/source.lua"))()

local UI = Lib:Create{
    Theme = "Dark", -- or any other theme
    Size = UDim2.new(0, 555, 0, 400) -- default
 }
 
 local Main = UI:Tab{
    Name = "Inicia"
 }
 
 local Divider = Main:Divider{
    Name = "Inicia shit"
 }
 
 local QuitDivider = Main:Divider{
    Name = "Sair"
 }

 --Todas as funções possuem os argumentos Name, Description e Callback para que você possa usá-los sempre que ig yes

 Divider:ColorPicker{
    Name = "ESP color",
    Default = Color3.fromRGB(0, 255, 255), -- default,
    Callback = function(player)
        print(player)
    end
 }
    local function criarESP(player)
        -- Verifica se o personagem do jogador existe
        local character = player.Character
        if not character then return end
        
        -- Cria um BillboardGui para exibir a caixa do ESP
        local espGui = Instance.new("BillboardGui")
        espGui.Adornee = character:WaitForChild("Head")  -- Coloca o ESP na cabeça do jogador
        espGui.Size = UDim2.new(0, 100, 0, 100)  -- Tamanho da caixa
        espGui.StudsOffset = Vector3.new(0, 2, 0)  -- Distância do jogador (altura)
        espGui.Parent = character  -- Coloca a GUI no personagem
        
        -- Cria uma Frame dentro do BillboardGui para simular a caixa
        local espBox = Instance.new("Frame")
        espBox.Size = UDim2.new(1, 0, 1, 0)  -- Preenche todo o espaço do BillboardGui
        espBox.BackgroundColor3 = Color3.fromRGB(255, 0, 0)  -- Cor da caixa (vermelha)
        espBox.BackgroundTransparency = 0.5  -- Transparência da caixa
        espBox.BorderSizePixel = 2  -- Tamanho da borda da caixa
        espBox.Parent = espGui  -- Coloca a caixa dentro do BillboardGui
    end
    
    -- Função para remover o ESP quando o jogador sai
    local function removerESP(player)
        -- Verifica se o personagem do jogador existe
        local character = player.Character
        if not character then return end
        
        -- Encontra o BillboardGui e remove
        local espGui = character:FindFirstChildOfClass("BillboardGui")
        if espGui then
            espGui:Destroy()  -- Remove a caixa de ESP
        end
    end
    
    -- Conectar as funções aos eventos do jogo
    game.Players.PlayerAdded:Connect(function(player)
        -- Quando o jogador entrar no jogo, cria o ESP
        player.CharacterAdded:Connect(function()
            criarESP(player)
        end)
    end)
    
    game.Players.PlayerRemoving:Connect(function(player)
        -- Quando o jogador sair do jogo, remove o ESP
        removerESP(player)
    end)
