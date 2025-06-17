--[[
Meme Sea Script by ChatGPT
Funções: Aimbot (mira direta), Auto Farm, Auto Raids (gemas), Auto Meme
]]

-- Aimbot simples (acerta os tiros diretamente no inimigo mais próximo)
function getClosestEnemy()
    local players = game:GetService("Players")
    local localPlayer = players.LocalPlayer
    local closestEnemy = nil
    local shortestDistance = math.huge

    for _, enemy in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
        if enemy:FindFirstChild("HumanoidRootPart") and enemy:FindFirstChild("Humanoid") and enemy.Humanoid.Health > 0 then
            local distance = (enemy.HumanoidRootPart.Position - localPlayer.Character.HumanoidRootPart.Position).magnitude
            if distance < shortestDistance then
                closestEnemy = enemy
                shortestDistance = distance
            end
        end
    end

    return closestEnemy
end

function aimAtEnemy(enemy)
    if enemy and enemy:FindFirstChild("HumanoidRootPart") then
        local args = {
            [1] = enemy.HumanoidRootPart.Position
        }
        game:GetService("ReplicatedStorage").RemoteEvent:FireServer(unpack(args))
    end
end

-- Auto Click/Farm
spawn(function()
    while wait(0.3) do
        pcall(function()
            local tool = game.Players.LocalPlayer.Character:FindFirstChildOfClass("Tool")
            if tool then
                tool:Activate()
            end
        end)
    end
end)

-- Auto Raid (exemplo genérico, depende do sistema de raids do jogo)
spawn(function()
    while wait(1) do
        pcall(function()
            local raidButton = game:GetService("Workspace"):FindFirstChild("RaidStarter")
            if raidButton then
                fireclickdetector(raidButton.ClickDetector)
            end
        end)
    end
end)

-- Auto Meme (ganha memes automaticamente, depende do botão/objeto do jogo)
spawn(function()
    while wait(2) do
        pcall(function()
            local memeBtn = game:GetService("Workspace"):FindFirstChild("MemeButton")
            if memeBtn then
                fireclickdetector(memeBtn.ClickDetector)
            end
        end)
    end
end)

-- Aimbot ativação automática
spawn(function()
    while wait(0.5) do
        local enemy = getClosestEnemy()
        if enemy then
            aimAtEnemy(enemy)
        end
    end
end)
