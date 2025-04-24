local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/Kavo-UI-Library/main/source.lua"))()
local Window = Library.CreateLib("Menu Exclusivo - by Você", "Sentinel")

-- Aba principal
local MainTab = Window:NewTab("Principal")
local MainSection = MainTab:NewSection("Automação")

MainSection:NewToggle("Auto Farm", "Ativa o farm automático", function(state)
    if state then
        print("Auto Farm Ativado")
    else
        print("Auto Farm Desativado")
    end
end)

MainSection:NewButton("Farmar Katakuri", "Vai até Katakuri e inicia o farm", function()
    print("Farmando Katakuri...")
end)

MainSection:NewButton("Farmar Novo Boss", "Farm automático do novo boss", function()
    print("Farmando Novo Boss...")
end)

-- Aba de Teleporte
local TeleportTab = Window:NewTab("Teleportes")
local TeleportSection = TeleportTab:NewSection("Ilhas e Locais")

TeleportSection:NewDropdown("Escolha a Ilha", "Teleporta para a ilha selecionada", {
    "Ilha Inicial", "Ilha do Gelo", "Ilha do Fogo", "Mirage Island"
}, function(currentOption)
    print("Teleportando para: "..currentOption)
end)

-- Extras
local ExtraTab = Window:NewTab("Extras")
local ExtraSection = ExtraTab:NewSection("Funções Adicionais")

ExtraSection:NewButton("Auto Matar Rip Indra", "Ativa combate automático contra Rip Indra", function()
    print("Auto matar Rip Indra ativado")
end)

ExtraSection:NewButton("Remover Nevoeiro (Fog)", "Remove o fog do jogo para melhor visão", function()
    game.Lighting.FogEnd = 100000
end)

ExtraSection:NewButton("Ativar God Human", "Farma e ativa God Human", function()
    print("Ativando God Human...")
end)

Library:Notify("Script carregado com sucesso!", 5)
