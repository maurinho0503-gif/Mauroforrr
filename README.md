-- ====================================================================
-- PAINEL OFICIAL RAYFIELD: Mauro e seus poderes (LISTA ATUALIZADA)
-- ====================================================================

local Players = game:GetService("Players")
local localPlayer = Players.LocalPlayer

-- 1. SCRIPT DE PROTEÇÃO POR AMIZADE (CONTA: A4Fmauro)
local donoNome = "A4Fmauro"
local function verificarAcesso()
    if localPlayer.Name == donoNome then return true end
    local s, res = pcall(function() 
        return localPlayer:IsFriendsWith(Players:GetUserIdFromNameAsync(donoNome)) 
    end)
    return s and res
end

if not verificarAcesso() then
    localPlayer:Kick("Manda mensagem em discord para inameheartless")
    return
end

-- 2. CARREGAMENTO DA INTERFACE OFICIAL RAYFIELD
local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

local Window = Rayfield:CreateWindow({
   Name = "Mauro e seus poderes",
   LoadingTitle = "Carregando Poderes...",
   LoadingSubtitle = "by A4Fmauro",
   ConfigurationSaving = { Enabled = false },
   Discord = { Enabled = false },
   KeySystem = false
})

local MainTab = Window:CreateTab("Scripts", 4483362458)

-- 3. BOTÃO ÚNICO DE ATIVAÇÃO GERAL
MainTab:CreateButton({
   Name = "Uma doze de poder do mauro",
   Callback = function()
        Rayfield:Notify({
            Title = "Sistema",
            Content = "Injetando seus novos poderes...",
            Duration = 3
        })

        -- =======================================================
        -- A. SCRIPT: UNIVERSAL HITBOX V5
        -- =======================================================
        task.spawn(pcall, function()
            loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Hitbox-V5-108660"))()
        end)

        -- =======================================================
        -- B. SCRIPT: AUTO CLICK MOBILE/PC
        -- =======================================================
        getgenv().AutoClick = false
        getgenv().ClickDelay = 50 

        local Players_AC = game:GetService("Players")
        local VirtualUser_AC = game:GetService("VirtualUser")
        local UIS_AC = game:GetService("UserInputService")
        local player_AC = Players_AC.LocalPlayer

        local gui_AC = Instance.new("ScreenGui")
        gui_AC.Name = "AutoClickGui"
        gui_AC.ResetOnSpawn = false
        gui_AC.Parent = game.CoreGui

        local frame_AC = Instance.new("Frame")
        frame_AC.Parent = gui_AC
        frame_AC.Size = UDim2.new(0, 170, 0, 110)
        frame_AC.Position = UDim2.new(1, -180, 0, 20) 
        frame_AC.BackgroundColor3 = Color3.fromRGB(25,25,25)
        frame_AC.BorderSizePixel = 0

        local corner_AC = Instance.new("UICorner", frame_AC)
        corner_AC.CornerRadius = UDim.new(0,12)

        local title_AC = Instance.new("TextLabel")
        title_AC.Parent = frame_AC
        title_AC.Size = UDim2.new(1,0,0,25)
        title_AC.BackgroundTransparency = 1
        title_AC.Text = "AUTO CLICK"
        title_AC.TextColor3 = Color3.new(1,1,1)
        title_AC.Font = Enum.Font.GothamBold
        title_AC.TextSize = 14

        local toggle_AC = Instance.new("TextButton")
        toggle_AC.Parent = frame_AC
        toggle_AC.Size = UDim2.new(0.85,0,0,35)
        toggle_AC.Position = UDim2.new(0.075,0,0.3,0)
        toggle_AC.BackgroundColor3 = Color3.fromRGB(170,0,0)
        toggle_AC.Text = "OFF"
        toggle_AC.TextColor3 = Color3.new(1,1,1)
        toggle_AC.Font = Enum.Font.GothamBold
        toggle_AC.TextSize = 16

        local toggleCorner_AC = Instance.new("UICorner", toggle_AC)
        toggleCorner_AC.CornerRadius = UDim.new(0,10)

        local speedBox_AC = Instance.new("TextBox")
        speedBox_AC.Parent = frame_AC
        speedBox_AC.Size = UDim2.new(0.85,0,0,25)
        speedBox_AC.Position = UDim2.new(0.075,0,0.72,0)
        speedBox_AC.BackgroundColor3 = Color3.fromRGB(40,40,40)
        speedBox_AC.Text = tostring(getgenv().ClickDelay)
        speedBox_AC.PlaceholderText = "Velocidade MS"
        speedBox_AC.TextColor3 = Color3.new(1,1,1)
        speedBox_AC.Font = Enum.Font.Gotham
        speedBox_AC.TextSize = 14

        local speedCorner_AC = Instance.new("UICorner", speedBox_AC)
        speedCorner_AC.CornerRadius = UDim.new(0,8)

        speedBox_AC.FocusLost:Connect(function()
            local num = tonumber(speedBox_AC.Text)
            if num and num >= 1 then getgenv().ClickDelay = num else speedBox_AC.Text = tostring(getgenv().ClickDelay) end
        end)

        toggle_AC.MouseButton1Click:Connect(function()
            getgenv().AutoClick = not getgenv().AutoClick
            if getgenv().AutoClick then
                toggle_AC.Text = "ON"
                toggle_AC.BackgroundColor3 = Color3.fromRGB(0,170,0)
            else
                toggle_AC.Text = "OFF"
                toggle_AC.BackgroundColor3 = Color3.fromRGB(170,0,0)
            end
        end)

        task.spawn(function()
            while true do
                if getgenv().AutoClick then
                    VirtualUser_AC:Button1Down(Vector2.new(0,0), workspace.CurrentCamera.CFrame)
                    task.wait(getgenv().ClickDelay / 1000)
                    VirtualUser_AC:Button1Up(Vector2.new(0,0), workspace.CurrentCamera.CFrame)
                else
                    task.wait(0.1)
                end
            end
        end)

        -- =======================================================
        -- C. SCRIPT: AIMBOT COM BOTÃO DE 120x40 (OFF/ON)
        -- =======================================================
        local P = game:GetService("Players")
        local R = game:GetService("RunService")
        local V = game:GetService("VirtualUser")
        local lp = P.LocalPlayer
        local cam = workspace.CurrentCamera
        local active = false

        local gui = Instance.new("ScreenGui", lp.PlayerGui)
        gui.Name, gui.ResetOnSpawn = "G", false
        
        local btn = Instance.new("TextButton", gui)
        btn.Size, btn.Position, btn.Text = UDim2.new(0,120,0,40), UDim2.new(0,10,0.7,0), "OFF"
        btn.BackgroundColor3 = Color3.new(1,0,0)
        btn.TextColor3 = Color3.new(1,1,1)
        btn.Font = Enum.Font.GothamBold
        btn.TextSize = 14

        btn.MouseButton1Click:Connect(function()
            active = not active
            btn.Text = active and "ON" or "OFF"
            btn.BackgroundColor3 = active and Color3.new(0,1,0) or Color3.new(1,0,0)
        end)

        R.RenderStepped:Connect(function()
            if not active or not lp.Character then return end
            local target, dist = nil, 350
            for _, p in pairs(P:GetPlayers()) do
                if p ~= lp and p.Character and p.Character:FindFirstChild("HumanoidRootPart") then
                    local d = (p.Character.HumanoidRootPart.Position - lp.Character.HumanoidRootPart.Position).Magnitude
                    if d < dist then dist, target = d, p.Character.HumanoidRootPart end
                end
            end
            if target then 
                workspace.CurrentCamera.CFrame = CFrame.new(workspace.CurrentCamera.CFrame.Position, target.Position)
                for i=1, 5 do V:Button1Down(Vector2.zero) V:Button1Up(Vector2.zero) end
            end
        end)

        -- =======================================================
        -- D. SCRIPT: ANGEL.LOL
        -- =======================================================
        task.spawn(pcall, function()
            loadstring(game:HttpGet("https://raw.githubusercontent.com/angel1LOL/angel.LOL4/refs/heads/main/Angel.LOL"))()
        end)
   end,
})
