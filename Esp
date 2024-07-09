local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local Workspace = game:GetService("Workspace")

-- Configuration
local TEAM_COLOR = Color3.fromRGB(0, 255, 0) -- Green color for teammates
local ENEMY_COLOR = Color3.fromRGB(255, 0, 0) -- Red color for enemies
local ESP_TRANSPARENCY = 0.7
local BOX_COLOR = Color3.fromRGB(255, 255, 255) -- White color for the hollow box
local BOX_THICKNESS = 2
local FONT_SIZE = 16

-- UI Elements
local guiFolder = Instance.new("Folder")
guiFolder.Name = "PlayerESP"
guiFolder.Parent = Workspace.CurrentCamera

-- Function to create or update ESP for a player
local function updatePlayerESP(player)
    local character = player.Character
    if character then
        task.wait(0.1) -- Wait for character to load
        local head = character:FindFirstChild("Head")
        local humanoid = character:FindFirstChildOfClass("Humanoid")

        if head and humanoid and humanoid.Health > 0 then
            local guiName = "PlayerESP_" .. player.Name
            local existingGui = guiFolder:FindFirstChild(guiName)
            local distance = (head.Position - Workspace.CurrentCamera.CFrame.Position).Magnitude

            if not existingGui then
                existingGui = Instance.new("BillboardGui")
                existingGui.Name = guiName
                existingGui.Size = UDim2.new(0, 200, 0, 100)
                existingGui.StudsOffset = Vector3.new(0, 2, 0)
                existingGui.AlwaysOnTop = true

                local frame = Instance.new("Frame", existingGui)
                frame.Size = UDim2.new(1, 0, 1, 0)
                frame.BackgroundTransparency = 1

                local nameLabel = Instance.new("TextLabel", frame)
                nameLabel.Name = "NameLabel"
                nameLabel.Size = UDim2.new(1, 0, 0.3, 0)
                nameLabel.Position = UDim2.new(0, 0, 0, 0)
                nameLabel.BackgroundTransparency = 1
                nameLabel.TextColor3 = Color3.new(1, 1, 1)
                nameLabel.Font = Enum.Font.SourceSansBold
                nameLabel.TextSize = FONT_SIZE
                nameLabel.TextStrokeTransparency = 0.5
                nameLabel.TextScaled = true

                local healthLabel = Instance.new("TextLabel", frame)
                healthLabel.Name = "HealthLabel"
                healthLabel.Size = UDim2.new(1, 0, 0.3, 0)
                healthLabel.Position = UDim2.new(0, 0, 0.3, 0)
                healthLabel.BackgroundTransparency = 1
                healthLabel.TextColor3 = Color3.new(1, 1, 1)
                healthLabel.Font = Enum.Font.SourceSansBold
                healthLabel.TextSize = FONT_SIZE
                healthLabel.TextStrokeTransparency = 0.5
                healthLabel.TextScaled = true

                local distanceLabel = Instance.new("TextLabel", frame)
                distanceLabel.Name = "DistanceLabel"
                distanceLabel.Size = UDim2.new(1, 0, 0.3, 0)
                distanceLabel.Position = UDim2.new(0, 0, 0.6, 0)
                distanceLabel.BackgroundTransparency = 1
                distanceLabel.TextColor3 = Color3.new(1, 1, 1)
                distanceLabel.Font = Enum.Font.SourceSansBold
                distanceLabel.TextSize = FONT_SIZE
                distanceLabel.TextStrokeTransparency = 0.5
                distanceLabel.TextScaled = true

                existingGui.Parent = guiFolder
            end

            existingGui.Adornee = head
            local frame = existingGui:FindFirstChildOfClass("Frame")
            if frame then
                local nameLabel = frame:FindFirstChild("NameLabel")
                local healthLabel = frame:FindFirstChild("HealthLabel")
                local distanceLabel = frame:FindFirstChild("DistanceLabel")

                if nameLabel and healthLabel and distanceLabel then
                    local isTeammate = player.Team == Players.LocalPlayer.Team
                    local color = isTeammate and TEAM_COLOR or ENEMY_COLOR
                    nameLabel.Text = player.Name
                    healthLabel.Text = "Health: " .. math.floor(humanoid.Health)
                    distanceLabel.Text = "Distance: " .. math.floor(distance) .. " studs"

                    nameLabel.TextColor3 = color
                    healthLabel.TextColor3 = color
                    distanceLabel.TextColor3 = color
                end
            end
        end
    end
end

-- Function to update ESP for all players
local function updateAllPlayerESP()
    for _, player in ipairs(Players:GetPlayers()) do
        if player ~= Players.LocalPlayer then
            updatePlayerESP(player)
        end
    end
end

-- Function to handle player added
local function onPlayerAdded(player)
    player.CharacterAdded:Connect(function()
        updatePlayerESP(player)
    end)
end

-- Connect to PlayerAdded event
Players.PlayerAdded:Connect(onPlayerAdded)

-- Initial update for existing players
for _, player in ipairs(Players:GetPlayers()) do
    onPlayerAdded(player)
end

-- Update ESP on every frame
RunService.RenderStepped:Connect(updateAllPlayerESP)
