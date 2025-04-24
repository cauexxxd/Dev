-- Script Fly + Noclip criado por Cauezxd
-- Modificado por ChatGPT com sistema de chave
-- Fly: F | Aumenta vel: X | Diminui vel: Z | Noclip: N (requer chave) | Chave: K

local Player = game.Players.LocalPlayer
local Character = Player.Character or Player.CharacterAdded:Wait()
local HumanoidRootPart = Character:WaitForChild("HumanoidRootPart")
local Humanoid = Character:WaitForChild("Humanoid")

local UIS = game:GetService("UserInputService")
local RunService = game:GetService("RunService")
local Debris = game:GetService("Debris")

local flying = false
local noclip = false
local speed = 5
local noclipUnlocked = false
local chaveCorreta = "cafex"

-- Velocity e Gyro
local vel = Instance.new("BodyVelocity")
vel.MaxForce = Vector3.new(1e5, 1e5, 1e5)
vel.Velocity = Vector3.zero
vel.P = 1250

local gyro = Instance.new("BodyGyro")
gyro.MaxTorque = Vector3.new(1e5, 1e5, 1e5)
gyro.P = 3000
gyro.CFrame = workspace.CurrentCamera.CFrame

-- Mostrar mensagem
local function showHint(text)
	local hint = Instance.new("Hint", game.CoreGui)
	hint.Text = text
	Debris:AddItem(hint, 2)
end

-- Fly
local function startFly()
	vel.Parent = HumanoidRootPart
	gyro.Parent = HumanoidRootPart
	Humanoid.PlatformStand = true
	flying = true
	showHint("Fly: ON")
end

local function stopFly()
	vel.Parent = nil
	gyro.Parent = nil
	Humanoid.PlatformStand = false
	flying = false
	showHint("Fly: OFF")
end

-- Noclip
local function toggleNoclip()
	if noclipUnlocked then
		noclip = not noclip
		showHint("Noclip: " .. (noclip and "ON" or "OFF"))
	else
		showHint("Chave inválida! Pressione K para digitar.")
	end
end

-- Verifica a chave digitada
local function pedirChave()
	local input = game:GetService("StarterGui"):PromptInput("Digite a chave para desbloquear noclip:")
	if input == chaveCorreta then
		noclipUnlocked = true
		showHint("Chave aceita! Noclip ativado.")
	else
		showHint("Chave incorreta.")
	end
end

-- Entrada do teclado
UIS.InputBegan:Connect(function(input, gpe)
	if gpe then return end

	if input.KeyCode == Enum.KeyCode.F then
		if flying then stopFly() else startFly() end
	elseif input.KeyCode == Enum.KeyCode.X then
		speed = speed + 1
		showHint("Velocidade: " .. speed)
	elseif input.KeyCode == Enum.KeyCode.Z then
		speed = math.max(1, speed - 1)
		showHint("Velocidade: " .. speed)
	elseif input.KeyCode == Enum.KeyCode.N then
		toggleNoclip()
	elseif input.KeyCode == Enum.KeyCode.K then
		pedirChave()
	end
end)

-- Loop principal
RunService.RenderStepped:Connect(function()
	-- Fly
	if flying then
		local dir = Vector3.zero
		if UIS:IsKeyDown(Enum.KeyCode.W) then dir += workspace.CurrentCamera.CFrame.LookVector end
		if UIS:IsKeyDown(Enum.KeyCode.S) then dir -= workspace.CurrentCamera.CFrame.LookVector end
		if UIS:IsKeyDown(Enum.KeyCode.A) then dir -= workspace.CurrentCamera.CFrame.RightVector end
		if UIS:IsKeyDown(Enum.KeyCode.D) then dir += workspace.CurrentCamera.CFrame.RightVector end
		if UIS:IsKeyDown(Enum.KeyCode.Space) then dir += Vector3.new(0, 1, 0) end
		if UIS:IsKeyDown(Enum.KeyCode.LeftControl) then dir -= Vector3.new(0, 1, 0) end

		vel.Velocity = dir.Magnitude > 0 and dir.Unit * speed or Vector3.zero
		gyro.CFrame = workspace.CurrentCamera.CFrame
	end

	-- Noclip
	if noclip then
		for _, part in ipairs(Character:GetDescendants()) do
			if part:IsA("BasePart") and part.CanCollide then
				part.CanCollide = false
			end
		end
	end
end)
