local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")

-- Remote
local evento = Instance.new("RemoteEvent")
evento.Name = "AdminForcaExtrema"
evento.Parent = ReplicatedStorage

-- lista branca (quem pode usar)
local admins = {
	["Nunes"] = true,
}

Players.PlayerAdded:Connect(function(player)
	local power = Instance.new("NumberValue")
	power.Name = "ThrowPower"
	power.Value = 1 -- padrão
	power.Parent = player
end)

evento.OnServerEvent:Connect(function(player, estado)
	if not admins[player.Name] then return end

	local power = player:FindFirstChild("ThrowPower")
	if not power then return end

	if estado then
		power.Value = 75 -- valor absurdo, mas controlado
	else
		power.Value = 1
	end
end)
local forcaBase = 180

local mult = 1
local power = player:FindFirstChild("ThrowPower")
if power then
	mult = power.Value
end

local forcaFinal = forcaBase * mult
-- aplica no impulso / LinearVelocity / força
