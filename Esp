local FILL_COLOR = Color3.fromHex("#d4d4d4")
local OUTLINE_COLOR = Color3.fromHex("#6b34eb")

local FILL_TRANSPARENCY = 0.15
local OUTLINE_TRANSPARENCY = 0.15

local Players = game:GetService("Players")

local function addHealthBar(character)
    local humanoid = character:FindFirstChildOfClass("Humanoid")
    local head = character:FindFirstChild("Head")
    if not humanoid or not head then return end
    if head:FindFirstChild("ESP_Health") then return end

    local gui = Instance.new("BillboardGui")
    gui.Name = "ESP_Health"
    gui.Adornee = head
    gui.Size = UDim2.fromScale(4, 0.5)
    gui.StudsOffset = Vector3.new(0, 3, 0)
    gui.AlwaysOnTop = true
    gui.Parent = head

    local bg = Instance.new("Frame")
    bg.Size = UDim2.fromScale(1, 1)
    bg.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
    bg.BorderSizePixel = 0
    bg.Parent = gui

    local bgCorner = Instance.new("UICorner")
    bgCorner.CornerRadius = UDim.new(0, 6)
    bgCorner.Parent = bg

    local bar = Instance.new("Frame")
    bar.Size = UDim2.fromScale(1, 1)
    bar.BackgroundColor3 = Color3.fromRGB(100, 255, 100)
    bar.BorderSizePixel = 0
    bar.Parent = bg

    local barCorner = Instance.new("UICorner")
    barCorner.CornerRadius = UDim.new(0, 6)
    barCorner.Parent = bar

    local function update()
        bar.Size = UDim2.fromScale(
            math.clamp(humanoid.Health / humanoid.MaxHealth, 0, 1),
            1
        )
    end

    update()
    humanoid.HealthChanged:Connect(update)
end



local function addHighlight(character)
    if not character:IsA("Model") then return end
    if not character:FindFirstChildOfClass("Humanoid") then return end
    if character:FindFirstChildOfClass("Highlight") then return end
    if character == Players.LocalPlayer.Character then return end

    local highlight = Instance.new("Highlight")
    highlight.Name = "ESP"
    highlight.Adornee = character
    highlight.Parent = character

    highlight.FillColor = FILL_COLOR
    highlight.OutlineColor = OUTLINE_COLOR
    highlight.FillTransparency = FILL_TRANSPARENCY
    highlight.OutlineTransparency = OUTLINE_TRANSPARENCY

    addHealthBar(character)

end


for _, obj in ipairs(workspace:GetDescendants()) do
    if obj:IsA("Model") then
        addHighlight(obj)
    end
end

workspace.DescendantAdded:Connect(function(obj)
    if obj:IsA("Model") then
        addHighlight(obj)
    end
end)
