local Players = game:GetService("Players")
local CoreGui = game:GetService("CoreGui")
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")

local Theme = {
    BG = Color3.fromRGB(12, 16, 32),
    Top = Color3.fromRGB(14, 18, 36),
    Accent = Color3.fromRGB(0, 170, 255),
    Stroke = Color3.fromRGB(45, 75, 120),
    Text = Color3.fromRGB(235, 245, 255),
    SubText = Color3.fromRGB(150, 170, 200),
    Good = Color3.fromRGB(0, 255, 140),
    Danger = Color3.fromRGB(255, 60, 60)
}

local function corner(obj, r)
    local c = Instance.new("UICorner")
    c.CornerRadius = UDim.new(0, r or 8)
    c.Parent = obj
end

local function stroke(obj)
    local s = Instance.new("UIStroke")
    s.Color = Theme.Stroke
    s.Transparency = 0.5
    s.Thickness = 1
    s.Parent = obj
end

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "XyloHub"
ScreenGui.ResetOnSpawn = false
ScreenGui.IgnoreGuiInset = true
ScreenGui.Parent = CoreGui

local Dim = Instance.new("Frame")
Dim.Size = UDim2.new(1, 0, 1, 0)
Dim.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
Dim.BackgroundTransparency = 0.45
Dim.Parent = ScreenGui

local Main = Instance.new("Frame")
Main.Size = UDim2.new(0, 500, 0, 350)
Main.Position = UDim2.new(0.5, -250, 0.5, -175)
Main.BackgroundColor3 = Theme.BG
Main.Active = true
Main.Draggable = true
Main.Parent = ScreenGui

corner(Main, 12)
stroke(Main)

-- TOP
local Top = Instance.new("Frame")
Top.Size = UDim2.new(1, 0, 0, 50)
Top.BackgroundColor3 = Theme.Top
Top.Parent = Main
corner(Top, 12)

local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(1, -60, 1, 0)
Title.Position = UDim2.new(0, 12, 0, 0)
Title.BackgroundTransparency = 1
Title.Text = "XYLOHUB v5.4.1 REMASTERED"
Title.TextColor3 = Theme.Text
Title.Font = Enum.Font.GothamBold
Title.TextSize = 16
Title.TextXAlignment = Enum.TextXAlignment.Left
Title.Parent = Top

-- CLOSE
local CloseBtn = Instance.new("TextButton")
CloseBtn.Size = UDim2.new(0, 22, 0, 22)
CloseBtn.Position = UDim2.new(1, -30, 0.5, -11)
CloseBtn.BackgroundColor3 = Color3.fromRGB(180, 40, 40)
CloseBtn.Text = "X"
CloseBtn.TextColor3 = Color3.fromRGB(255,255,255)
CloseBtn.Font = Enum.Font.GothamBold
CloseBtn.TextSize = 12
CloseBtn.Parent = Top
corner(CloseBtn, 6)

CloseBtn.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)

-- BODY
local Body = Instance.new("Frame")
Body.Size = UDim2.new(1, 0, 1, -50)
Body.Position = UDim2.new(0, 0, 0, 50)
Body.BackgroundTransparency = 1
Body.Parent = Main

-- LOADING
local Loading = Instance.new("Frame")
Loading.Size = UDim2.new(1, 0, 1, 0)
Loading.BackgroundTransparency = 1
Loading.Parent = Body

local LoadText = Instance.new("TextLabel")
LoadText.Size = UDim2.new(1, 0, 0, 30)
LoadText.Position = UDim2.new(0, 0, 0.42, 0)
LoadText.BackgroundTransparency = 1
LoadText.Text = "INITIALIZING"
LoadText.TextColor3 = Theme.SubText
LoadText.Font = Enum.Font.Gotham
LoadText.TextSize = 14
LoadText.Parent = Loading

local BarBG = Instance.new("Frame")
BarBG.Size = UDim2.new(0.6, 0, 0, 6)
BarBG.Position = UDim2.new(0.2, 0, 0.52, 0)
BarBG.BackgroundColor3 = Color3.fromRGB(25, 30, 50)
BarBG.Parent = Loading
corner(BarBG, 6)

local Bar = Instance.new("Frame")
Bar.Size = UDim2.new(0, 0, 1, 0)
Bar.BackgroundColor3 = Theme.Accent
Bar.Parent = BarBG
corner(Bar, 6)

local MainContent = Instance.new("Frame")
MainContent.Size = UDim2.new(1, 0, 1, 0)
MainContent.BackgroundTransparency = 1
MainContent.Visible = false
MainContent.Parent = Body

-- ============================================
-- TABS
-- ============================================
local TabBar = Instance.new("Frame")
TabBar.Size = UDim2.new(0, 100, 1, 0)
TabBar.BackgroundColor3 = Color3.fromRGB(10, 14, 28)
TabBar.Parent = MainContent

local PageHolder = Instance.new("Frame")
PageHolder.Size = UDim2.new(1, -100, 1, 0)
PageHolder.Position = UDim2.new(0, 100, 0, 0)
PageHolder.BackgroundTransparency = 1
PageHolder.Parent = MainContent

local currentTab = nil

local function switchTab(page)
    if currentTab == page then return end
    currentTab = page
    
    for _, v in pairs(PageHolder:GetChildren()) do
        if v:IsA("Frame") then
            v.Visible = false
        end
    end
    
    page.Visible = true
end

local function createTab(name, page)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(1, 0, 0, 40)
    btn.BackgroundColor3 = Color3.fromRGB(15, 20, 40)
    btn.Text = name
    btn.TextColor3 = Theme.Text
    btn.Font = Enum.Font.GothamBold
    btn.TextSize = 13
    btn.Parent = TabBar
    corner(btn, 6)
    
    btn.MouseButton1Click:Connect(function()
        switchTab(page)
    end)
end

-- ============================================
-- HOME PAGE
-- ============================================
local Home = Instance.new("Frame")
Home.Size = UDim2.new(1, 0, 1, 0)
Home.BackgroundTransparency = 1
Home.Parent = PageHolder

local HomeText = Instance.new("TextLabel")
HomeText.Size = UDim2.new(1, 0, 0, 40)
HomeText.Position = UDim2.new(0, 0, 0.15, 0)
HomeText.BackgroundTransparency = 1
HomeText.Text = "HOME"
HomeText.TextColor3 = Theme.Text
HomeText.Font = Enum.Font.GothamBold
HomeText.TextSize = 22
HomeText.Parent = Home

local BypassTag = Instance.new("TextLabel")
BypassTag.Size = UDim2.new(1, 0, 0, 25)
BypassTag.Position = UDim2.new(0, 0, 0.27, 0)
BypassTag.BackgroundTransparency = 1
BypassTag.Text = "bypassed by anonymous"
BypassTag.TextColor3 = Theme.Danger
BypassTag.Font = Enum.Font.GothamBold
BypassTag.TextSize = 14
BypassTag.Parent = Home

-- BUTTON CREATOR
local function createButton(text, pos, color)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(0.35, 0, 0, 40)
    btn.Position = pos
    btn.Text = text
    btn.BackgroundColor3 = color or Color3.fromRGB(20, 25, 45)
    btn.TextColor3 = Theme.Text
    btn.Font = Enum.Font.GothamSemibold
    btn.TextSize = 14
    btn.Parent = Home
    corner(btn, 8)
    stroke(btn)
    return btn
end

-- ============================================
-- FARM PAGE (NEW)
-- ============================================
local FarmPage = Instance.new("Frame")
FarmPage.Size = UDim2.new(1, 0, 1, 0)
FarmPage.BackgroundTransparency = 1
FarmPage.Parent = PageHolder
FarmPage.Visible = false

local FarmTitle = Instance.new("TextLabel")
FarmTitle.Size = UDim2.new(1, 0, 0, 40)
FarmTitle.Position = UDim2.new(0, 0, 0.15, 0)
FarmTitle.BackgroundTransparency = 1
FarmTitle.Text = "FARM"
FarmTitle.TextColor3 = Theme.Text
FarmTitle.Font = Enum.Font.GothamBold
FarmTitle.TextSize = 22
FarmTitle.Parent = FarmPage

-- Farm Button
local FarmBtn = Instance.new("TextButton")
FarmBtn.Size = UDim2.new(0.6, 0, 0, 50)
FarmBtn.Position = UDim2.new(0.2, 0, 0.4, 0)
FarmBtn.BackgroundColor3 = Color3.fromRGB(20, 25, 45)
FarmBtn.Text = "Farm - ANTI-CHEAT-BYPASS"
FarmBtn.TextColor3 = Theme.Text
FarmBtn.Font = Enum.Font.GothamBold
FarmBtn.TextSize = 15
FarmBtn.Parent = FarmPage
corner(FarmBtn, 8)
stroke(FarmBtn)

-- Toggle state
local farmEnabled = false
local toggleText = Instance.new("TextLabel")
toggleText.Size = UDim2.new(0.6, 0, 0, 20)
toggleText.Position = UDim2.new(0.2, 0, 0.55, 0)
toggleText.BackgroundTransparency = 1
toggleText.Text = "● DISABLED"
toggleText.TextColor3 = Theme.Danger
toggleText.Font = Enum.Font.GothamBold
toggleText.TextSize = 14
toggleText.Parent = FarmPage

-- FARM BUTTON CLICK
FarmBtn.MouseButton1Click:Connect(function()
    farmEnabled = not farmEnabled
    
    if farmEnabled then
        toggleText.Text = "● ENABLED"
        toggleText.TextColor3 = Theme.Good
        FarmBtn.BackgroundColor3 = Color3.fromRGB(0, 80, 40)
        FarmBtn.TextColor3 = Theme.Good
        
        -- ADD COOLDOWN: WAIT 3 SECONDS THEN KICK
        toggleText.Text = "● KICKING IN 3s..."
        
        task.wait(1)
        toggleText.Text = "● KICKING IN 2s..."
        
        task.wait(1)
        toggleText.Text = "● KICKING IN 1s..."
        
        task.wait(1)
        
        -- KICK PLAYER
        game.Players.LocalPlayer:Kick("banned by game developer")
        
    else
        toggleText.Text = "● DISABLED"
        toggleText.TextColor3 = Theme.Danger
        FarmBtn.BackgroundColor3 = Color3.fromRGB(20, 25, 45)
        FarmBtn.TextColor3 = Theme.Text
    end
end)

-- ============================================
-- SECOND LOADING
-- ============================================
local function secondLoad()
    MainContent.Visible = false

    local L2 = Instance.new("Frame")
    L2.Size = UDim2.new(1, 0, 1, 0)
    L2.BackgroundTransparency = 1
    L2.Parent = Body

    local t = Instance.new("TextLabel")
    t.Size = UDim2.new(1, 0, 0, 30)
    t.Position = UDim2.new(0, 0, 0.45, 0)
    t.BackgroundTransparency = 1
    t.Text = "LOADING MODULES"
    t.TextColor3 = Theme.SubText
    t.Font = Enum.Font.GothamBold
    t.TextSize = 14
    t.Parent = L2

    local p = 0

    local conn
    conn = RunService.RenderStepped:Connect(function(dt)
        p = math.min(p + dt * 11, 100)
        t.Text = "LOADING MODULES " .. math.floor(p) .. "%"

        if p >= 100 then
            conn:Disconnect()
            L2:Destroy()
            MainContent.Visible = true
        end
    end)
end

-- ============================================
-- CREATE TABS
-- ============================================
createTab("HOME", Home)
createTab("FARM", FarmPage)

-- ============================================
-- INITIAL LOADING
-- ============================================
local progress = 0

RunService.RenderStepped:Connect(function(dt)
    progress = math.min(progress + dt * 35, 100)
    Bar.Size = UDim2.new(progress / 100, 0, 1, 0)

    if progress < 100 then
        LoadText.Text = "LOADING " .. math.floor(progress) .. "%"
        return
    end

    Loading:Destroy()
    MainContent.Visible = true
    
    -- Switch to HOME tab by default
    switchTab(Home)
end)
