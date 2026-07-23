local Players = game:GetService("Players")
local CoreGui = game:GetService("CoreGui")
local RunService = game:GetService("RunService")
local StarterGui = game:GetService("StarterGui")

local player = Players.LocalPlayer

-- 启动通知
pcall(function()
    StarterGui:SetCore("SendNotification", {
        Title = "提示",
        Text = "启动成功！",
        Duration = 2
    })
end)

-- 主 UI
local gui = Instance.new("ScreenGui", CoreGui)
gui.Name = "UI"

local mainFrame = Instance.new("Frame", gui)
mainFrame.Size = UDim2.new(0, 300, 0, 200)
mainFrame.Position = UDim2.new(0.5, -150, 0.5, -100)
mainFrame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
mainFrame.BorderSizePixel = 0
mainFrame.Active = true
mainFrame.Draggable = true

-- 圆角
pcall(function()
    Instance.new("UICorner", mainFrame).CornerRadius = UDim.new(0, 8)
end)

-- 彩色发光边框（兼容版，不使用 fromHSV）
local stroke = Instance.new("UIStroke", mainFrame)
stroke.Thickness = 2
stroke.Transparency = 0.3
stroke.Color = Color3.fromRGB(255, 100, 100)

local time = 0
RunService.Heartbeat:Connect(function(delta)
    time = time + delta * 2  -- 控制速度
    -- 正弦波生成彩虹色 R,G,B 相位差为 2π/3
    local r = math.sin(time) * 127 + 128
    local g = math.sin(time + 2.094) * 127 + 128
    local b = math.sin(time + 4.188) * 127 + 128
    stroke.Color = Color3.fromRGB(r, g, b)
end)

-- 标题栏
local titleBar = Instance.new("Frame", mainFrame)
titleBar.Size = UDim2.new(1, -10, 0, 30)
titleBar.Position = UDim2.new(0, 5, 0, 5)
titleBar.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
titleBar.BorderSizePixel = 0
pcall(function()
    Instance.new("UICorner", titleBar).CornerRadius = UDim.new(0, 4)
end)

local titleLabel = Instance.new("TextLabel", titleBar)
titleLabel.Size = UDim2.new(1, -70, 1, 0)
titleLabel.Position = UDim2.new(0, 10, 0, 0)
titleLabel.BackgroundTransparency = 1
titleLabel.Text = "老牧师菜单 ⚡✨"
titleLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
titleLabel.Font = Enum.Font.GothamBold
titleLabel.TextSize = 14
titleLabel.TextXAlignment = Enum.TextXAlignment.Left

-- 关闭按钮
local closeBtn = Instance.new("TextButton", mainFrame)
closeBtn.Size = UDim2.new(0, 28, 0, 28)
closeBtn.Position = UDim2.new(1, -30, 0, 1)
closeBtn.BackgroundColor3 = Color3.fromRGB(220, 70, 70)
closeBtn.Text = ""
closeBtn.BorderSizePixel = 0
closeBtn.AutoButtonColor = false
pcall(function()
    Instance.new("UICorner", closeBtn).CornerRadius = UDim.new(0, 6)
end)
closeBtn.MouseEnter:Connect(function()
    closeBtn.BackgroundColor3 = Color3.fromRGB(255, 100, 100)
end)
closeBtn.MouseLeave:Connect(function()
    closeBtn.BackgroundColor3 = Color3.fromRGB(220, 70, 70)
end)
closeBtn.MouseButton1Click:Connect(function()
    gui:Destroy()
end)

-- 缩放按钮
local scaleBtn = Instance.new("TextButton", mainFrame)
scaleBtn.Size = UDim2.new(0, 28, 0, 28)
scaleBtn.Position = UDim2.new(1, -62, 0, 1)
scaleBtn.BackgroundColor3 = Color3.fromRGB(220, 120, 170)
scaleBtn.Text = ""
scaleBtn.BorderSizePixel = 0
scaleBtn.AutoButtonColor = false
pcall(function()
    Instance.new("UICorner", scaleBtn).CornerRadius = UDim.new(0, 6)
end)
scaleBtn.MouseEnter:Connect(function()
    scaleBtn.BackgroundColor3 = Color3.fromRGB(240, 150, 190)
end)
scaleBtn.MouseLeave:Connect(function()
    scaleBtn.BackgroundColor3 = Color3.fromRGB(220, 120, 170)
end)

-- 内容区
local contentFrame = Instance.new("Frame", mainFrame)
contentFrame.Size = UDim2.new(1, -10, 1, -45)
contentFrame.Position = UDim2.new(0, 5, 0, 40)
contentFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
contentFrame.BorderSizePixel = 0
pcall(function()
    Instance.new("UICorner", contentFrame).CornerRadius = UDim.new(0, 4)
end)

-- 厉鬼复苏按钮
local respawnBtn = Instance.new("TextButton", contentFrame)
respawnBtn.Size = UDim2.new(0, 24, 0, 24)
respawnBtn.Position = UDim2.new(0, 10, 0, 10)
respawnBtn.BackgroundColor3 = Color3.fromRGB(100, 100, 100)
respawnBtn.Text = ""
respawnBtn.BorderSizePixel = 0
respawnBtn.AutoButtonColor = false
pcall(function()
    Instance.new("UICorner", respawnBtn).CornerRadius = UDim.new(0, 6)
end)
respawnBtn.MouseEnter:Connect(function()
    respawnBtn.BackgroundColor3 = Color3.fromRGB(150, 150, 150)
end)
respawnBtn.MouseLeave:Connect(function()
    respawnBtn.BackgroundColor3 = Color3.fromRGB(100, 100, 100)
end)
respawnBtn.MouseButton1Click:Connect(function()
    pcall(function()
        if player.Character then
            player.Character:BreakJoints()
        end
    end)
    player:LoadCharacter()
end)

local respawnLabel = Instance.new("TextLabel", contentFrame)
respawnLabel.Size = UDim2.new(0, 120, 0, 24)
respawnLabel.Position = UDim2.new(0, 40, 0, 10)
respawnLabel.BackgroundTransparency = 1
respawnLabel.Text = "厉鬼复苏💀"
respawnLabel.TextColor3 = Color3.fromRGB(255, 50, 50)
respawnLabel.Font = Enum.Font.FredokaOne
respawnLabel.TextSize = 16
respawnLabel.TextXAlignment = Enum.TextXAlignment.Left

-- 最小化按钮
local minimizedBtn = Instance.new("TextButton", gui)
minimizedBtn.Size = UDim2.new(0, 28, 0, 28)
minimizedBtn.BackgroundColor3 = Color3.fromRGB(220, 120, 170)
minimizedBtn.Text = "
