-- Fly feito por ChatGPT
-- Ative com a tecla "F"

local Player = game.Players.LocalPlayer
local Character = Player.Character or Player.CharacterAdded:Wait()
local HumanoidRootPart = Character:WaitForChild("HumanoidRootPart")

local flying = false
local speed = 5

local UIS = game:GetService("UserInputService")
local RunService = game:GetService("RunService")

local vel = Instance.new("BodyVelocity")
vel.MaxForce = Vector3.new(1e5, 1e5, 1e5)
vel.Velocity = Vector3.zero
vel.P = 1250

local function startFly()
    vel.Parent = HumanoidRootPart
    flying = true
end

local function stopFly()
    flying = false
    vel.Parent = nil
end

local direction = Vector3.zero

UIS.InputBegan:Connect(function(input, gpe)
    if gpe then return end

    if input.KeyCode == Enum.KeyCode.F then
        if flying then
            stopFly()
        else
            startFly()
        end
    end
end)

RunService.RenderStepped:Connect(function()
    if flying then
        direction = Vector3.zero
        if UIS:IsKeyDown(Enum.KeyCode.W) then direction = direction + (workspace.CurrentCamera.CFrame.LookVector) end
        if UIS:IsKeyDown(Enum.KeyCode.S) then direction = direction - (workspace.CurrentCamera.CFrame.LookVector) end
        if UIS:IsKeyDown(Enum.KeyCode.A) then direction = direction - (workspace.CurrentCamera.CFrame.RightVector) end
        if UIS:IsKeyDown(Enum.KeyCode.D) then direction = direction + (workspace.CurrentCamera.CFrame.RightVector) end
        if UIS:IsKeyDown(Enum.KeyCode.Space) then direction = direction + Vector3.new(0, 1, 0) end
        if UIS:IsKeyDown(Enum.KeyCode.LeftControl) then direction = direction - Vector3.new(0, 1, 0) end

        vel.Velocity = direction.Unit * speed
    end
end)
