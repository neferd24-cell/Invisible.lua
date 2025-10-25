-- ⚡ Script de invisibilidad total con botón ya hecho
-- Pega este LocalScript directamente en StarterGui

local player = game.Players.LocalPlayer
local gui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
gui.Name = "InvisSystem"

-- 🎨 Crear botón
local button = Instance.new("TextButton")
button.Parent = gui
button.Size = UDim2.new(0, 180, 0, 60)
button.Position = UDim2.new(0.7, 0, 0.85, 0)
button.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
button.TextColor3 = Color3.fromRGB(255, 255, 255)
button.Text = "👻 Invisibilidad (OFF)"
button.Font = Enum.Font.GothamBold
button.TextScaled = true
button.BorderSizePixel = 0
button.BackgroundTransparency = 0.15
button.Active = true
button.Draggable = true

-- 💡 Estado
local invisible = false

-- 🔧 Función de invisibilidad
local function setInvisible(state)
	invisible = state
	local character = player.Character or player.CharacterAdded:Wait()

	for _, v in pairs(character:GetDescendants()) do
		if v:IsA("BasePart") then
			v.LocalTransparencyModifier = state and 1 or 0
		elseif v:IsA("Decal") then
			v.Transparency = state and 1 or 0
		end
	end

	-- 🔩 Si el jugador tiene un objeto (ejemplo un Brainrot)
	local tool = character:FindFirstChildOfClass("Tool") or player.Backpack:FindFirstChildOfClass("Tool")
	if tool then
		for _, part in pairs(tool:GetDescendants()) do
			if part:IsA("BasePart") or part:IsA("Decal") then
				part.LocalTransparencyModifier = state and 1 or 0
			end
		end
	end

	button.Text = state and "👻 Invisibilidad (ON)" or "👁 Invisibilidad (OFF)"
end

-- 🖱️ Click para activar o desactivar
button.MouseButton1Click:Connect(function()
	setInvisible(not invisible)
end)
