-- Carregar a Rayfield UI
local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

local Window = Rayfield:CreateWindow({
   Name = "Script Brookhaven",
   LoadingTitle = "Carregando Brookhaven...",
   LoadingSubtitle = "by SeuNome",
   ConfigurationSaving = {
      Enabled = true,
      FolderName = nil,
      FileName = "ScriptBrook"
   },
   Discord = {
      Enabled = false,
      Invite = "",
      RememberJoins = true
   },
   KeySystem = false
})

local MainTab = Window:CreateTab("Brookhaven Menu", 4483362458)

-- Teleporte para Locais
MainTab:CreateButton({
   Name = "Ir para Hospital",
   Callback = function()
      game.Players.LocalPlayer.Character:MoveTo(Vector3.new(-284.52, 34.31, -353.74))
   end
})

MainTab:CreateButton({
   Name = "Ir para Banco",
   Callback = function()
      game.Players.LocalPlayer.Character:MoveTo(Vector3.new(-433.4, 22.16, -287.5))
   end
})

MainTab:CreateButton({
   Name = "Ir para Escola",
   Callback = function()
      game.Players.LocalPlayer.Character:MoveTo(Vector3.new(-285, 33, -623))
   end
})

-- Modificar velocidade
MainTab:CreateSlider({
   Name = "Velocidade do Jogador",
   Range = {16, 100},
   Increment = 1,
   Suffix = "Speed",
   CurrentValue = 16,
   Callback = function(Value)
      game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = Value
   end,
})

-- Trollar Jogadores (ex: tocar sirene)
MainTab:CreateButton({
   Name = "Tocar Sirene da Polícia",
   Callback = function()
      for _, v in pairs(workspace:GetDescendants()) do
         if v:IsA("Sound") and v.Name == "Siren" then
            v:Play()
         end
      end
   end
})

-- Ativar visão noturna (efeito)
MainTab:CreateButton({
   Name = "Visão Noturna",
   Callback = function()
      game.Lighting.Ambient = Color3.fromRGB(0, 255, 0)
      game.Lighting.OutdoorAmbient = Color3.fromRGB(0, 255, 0)
   end
})

-- Resetar visão
MainTab:CreateButton({
   Name = "Resetar Visão",
   Callback = function()
      game.Lighting.Ambient = Color3.fromRGB(128, 128, 128)
      game.Lighting.OutdoorAmbient = Color3.fromRGB(128, 128, 128)
   end
})
