--[[ 
    PREMIUM EĞİTİM HUB v2 | Modern GUI Şablonu
    Sadece Studio / Kendi Oyunun için - Eğitim Amaçlı
    Brookhaven, Blox Fruits vb. oyunlarda exploit kullanımı ToS ihlalidir
]]
local pcallSuccess, err = pcall(function()
    local Players = game:GetService("Players")
    local UserInputService = game:GetService("UserInputService")
    local TweenService = game:GetService("TweenService")
    local Lighting = game:GetService("Lighting")
    local TeleportService = game:GetService("TeleportService")
    local ReplicatedStorage = game:GetService("ReplicatedStorage")

    local LocalPlayer = Players.LocalPlayer
    local PlayerGui = LocalPlayer:WaitForChild("PlayerGui")

    -- // TEMA
    local Theme = {
        Bg = Color3.fromRGB(18,18,22),
        Card = Color3.fromRGB(28,28,33),
        CardHover = Color3.fromRGB(35,35,42),
        Accent = Color3.fromRGB(109, 89, 255),
        Accent2 = Color3.fromRGB(0, 210, 255),
        Text = Color3.fromRGB(240,240,245),
        SubText = Color3.fromRGB(150,150,165),
        ToggleOff = Color3.fromRGB(55,55,65),
        Success = Color3.fromRGB(0, 200, 110),
        Stroke = Color3.fromRGB(45,45,55)
    }

    local function tween(obj, props, time)
        TweenService:Create(obj, TweenInfo.new(time or 0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), props):Play()
    end

    -- // ANA GUI
    local ScreenGui = Instance.new("ScreenGui")
    ScreenGui.Name = "PremiumEgitimHub_v2"
    ScreenGui.ResetOnSpawn = false
    ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
    ScreenGui.IgnoreGuiInset = true
    ScreenGui.Parent = PlayerGui

    local MainFrame = Instance.new("Frame", ScreenGui)
    MainFrame.Size = UDim2.new(0, 620, 0, 420)
    MainFrame.Position = UDim2.new(0.5, -310, 0.5, -210)
    MainFrame.BackgroundColor3 = Theme.Bg
    MainFrame.BorderSizePixel = 0
    MainFrame.ClipsDescendants = true
    Instance.new("UICorner", MainFrame).CornerRadius = UDim.new(0, 14)
    local MainStroke = Instance.new("UIStroke", MainFrame)
    MainStroke.Color = Theme.Stroke
    MainStroke.Thickness = 1.5

    -- Gölge
    local Shadow = Instance.new("ImageLabel", MainFrame)
    Shadow.ZIndex = -1
    Shadow.Size = UDim2.new(1, 40, 1, 40)
    Shadow.Position = UDim2.new(0, -20, 0, -20)
    Shadow.BackgroundTransparency = 1
    Shadow.Image = "rbxassetid://6015897843"
    Shadow.ImageColor3 = Color3.new(0,0,0)
    Shadow.ImageTransparency = 0.5
    Shadow.ScaleType = Enum.ScaleType.Slice
    Shadow.SliceCenter = Rect.new(49,49,450,450)

    -- // TOPBAR
    local TopBar = Instance.new("Frame", MainFrame)
    TopBar.Size = UDim2.new(1, 0, 0, 52)
    TopBar.BackgroundColor3 = Color3.fromRGB(22,22,27)
    TopBar.BorderSizePixel = 0
    Instance.new("UICorner", TopBar).CornerRadius = UDim.new(0, 14)
    local TopFix = Instance.new("Frame", TopBar) -- alt köşeyi düzelt
    TopFix.Size = UDim2.new(1,0,0,14)
    TopFix.Position = UDim2.new(0,0,1,-14)
    TopFix.BackgroundColor3 = TopBar.BackgroundColor3
    TopFix.BorderSizePixel = 0

    local Logo = Instance.new("Frame", TopBar)
    Logo.Size = UDim2.new(0, 36, 0, 36)
    Logo.Position = UDim2.new(0, 14, 0, 8)
    Logo.BackgroundColor3 = Theme.Accent
    Instance.new("UICorner", Logo).CornerRadius = UDim.new(0, 9)
    local LogoGrad = Instance.new("UIGradient", Logo)
    LogoGrad.Color = ColorSequence.new(Theme.Accent, Theme.Accent2)
    LogoGrad.Rotation = 45
    local LogoText = Instance.new("TextLabel", Logo)
    LogoText.Size = UDim2.new(1,0,1,0)
    LogoText.BackgroundTransparency = 1
    LogoText.Text = "◈"
    LogoText.TextColor3 = Color3.new(1,1,1)
    LogoText.Font = Enum.Font.GothamBold
    LogoText.TextSize = 18

    local Title = Instance.new("TextLabel", TopBar)
    Title.Position = UDim2.new(0, 60, 0, 6)
    Title.Size = UDim2.new(0, 200, 0, 20)
    Title.BackgroundTransparency = 1
    Title.Text = "Premium Hub"
    Title.Font = Enum.Font.GothamBold
    Title.TextSize = 15
    Title.TextColor3 = Theme.Text
    Title.TextXAlignment = 0
    local SubTitle = Instance.new("TextLabel", TopBar)
    SubTitle.Position = UDim2.new(0, 60, 0, 24)
    SubTitle.Size = UDim2.new(0, 250, 0, 14)
    SubTitle.BackgroundTransparency = 1
    SubTitle.Text = "v2.0  •  Eğitim Şablonu  •  RightShift / ESC"
    SubTitle.Font = Enum.Font.Gotham
    SubTitle.TextSize = 11
    SubTitle.TextColor3 = Theme.SubText
    SubTitle.TextXAlignment = 0

    local function topBtn(pos, txt, color)
        local b = Instance.new("TextButton", TopBar)
        b.Size = UDim2.new(0, 32, 0, 32)
        b.Position = UDim2.new(1, pos, 0, 10)
        b.BackgroundColor3 = Color3.fromRGB(35,35,42)
        b.Text = txt
        b.Font = Enum.Font.GothamBold
        b.TextSize = 14
        b.TextColor3 = Theme.Text
        Instance.new("UICorner", b).CornerRadius = UDim.new(0, 8)
        if color then b.BackgroundColor3 = color end
        b.MouseEnter:Connect(function() tween(b, {BackgroundColor3 = Color3.fromRGB(50,50,60)}, 0.15) end)
        b.MouseLeave:Connect(function() tween(b, {BackgroundColor3 = color or Color3.fromRGB(35,35,42)}, 0.15) end)
        return b
    end
    local CloseBtn = topBtn(-42, "✕", Color3.fromRGB(220,50,70))
    local MinBtn = topBtn(-80, "—", nil)

    -- // LAYOUT
    local Body = Instance.new("Frame", MainFrame)
    Body.Position = UDim2.new(0,0,0,52)
    Body.Size = UDim2.new(1,0,1,-52)
    Body.BackgroundTransparency = 1

    local SideBar = Instance.new("Frame", Body)
    SideBar.Size = UDim2.new(0, 155, 1, -16)
    SideBar.Position = UDim2.new(0, 8, 0, 8)
    SideBar.BackgroundColor3 = Theme.Card
    SideBar.BorderSizePixel = 0
    Instance.new("UICorner", SideBar).CornerRadius = UDim.new(0, 10)
    local SidePad = Instance.new("UIPadding", SideBar)
    SidePad.PaddingTop = UDim.new(0,8)
    SidePad.PaddingLeft = UDim.new(0,8)
    SidePad.PaddingRight = UDim.new(0,8)
    local SideList = Instance.new("UIListLayout", SideBar)
    SideList.Padding = UDim.new(0,6)
    SideList.SortOrder = Enum.SortOrder.LayoutOrder

    local PageContainer = Instance.new("Frame", Body)
    PageContainer.Size = UDim2.new(1, -179, 1, -16)
    PageContainer.Position = UDim2.new(0, 171, 0, 8)
    PageContainer.BackgroundTransparency = 1

    -- // HELPERS
    local Pages, TabBtns = {}, {}
    local function createCard(parent)
        local c = Instance.new("Frame", parent)
        c.Size = UDim2.new(1, 0, 0, 54)
        c.BackgroundColor3 = Theme.Card
        c.BorderSizePixel = 0
        Instance.new("UICorner", c).CornerRadius = UDim.new(0, 10)
        Instance.new("UIStroke", c).Color = Theme.Stroke
        c.LayoutOrder = #parent:GetChildren()
        return c
    end

    local function createToggle(parent, title, desc, callback) -- 1:90
        local card = createCard(parent)
        local t = Instance.new("TextLabel", card)
        t.Position = UDim2.new(0,12,0,8)
        t.Size = UDim2.new(1,-70,0,16)
        t.BackgroundTransparency = 1
        t.Text = title
        t.Font = Enum.Font.GothamBold
        t.TextSize = 13
        t.TextColor3 = Theme.Text
        t.TextXAlignment = 0
        local d = Instance.new("TextLabel", card)
        d.Position = UDim2.new(0,12,0,26)
        d.Size = UDim2.new(1,-70,0,14)
        d.BackgroundTransparency = 1
        d.Text = desc
        d.Font = Enum.Font.Gotham
        d.TextSize = 11
        d.TextColor3 = Theme.SubText
        d.TextXAlignment = 0

        local track = Instance.new("Frame", card)
        track.Size = UDim2.new(0, 44, 0, 24)
        track.Position = UDim2.new(1, -56, 0.5, -12)
        track.BackgroundColor3 = Theme.ToggleOff
        Instance.new("UICorner", track).CornerRadius = UDim.new(1,0)
        local knob = Instance.new("Frame", track)
        knob.Size = UDim2.new(0, 18, 0, 18)
        knob.Position = UDim2.new(0, 3, 0.5, -9)
        knob.BackgroundColor3 = Color3.new(1,1,1)
        Instance.new("UICorner", knob).CornerRadius = UDim.new(1,0)

        local enabled = false
        local btn = Instance.new("TextButton", card)
        btn.Size = UDim2.new(1,0,1,0)
        btn.BackgroundTransparency = 1
        btn.Text = ""
        btn.MouseEnter:Connect(function() tween(card, {BackgroundColor3 = Theme.CardHover}, 0.15) end)
        btn.MouseLeave:Connect(function() tween(card, {BackgroundColor3 = Theme.Card}, 0.15) end)
        btn.MouseButton1Click:Connect(function()
            enabled = not enabled
            pcall(callback, enabled)
            tween(track, {BackgroundColor3 = enabled and Theme.Success or Theme.ToggleOff}, 0.2)
            tween(knob, {Position = enabled and UDim2.new(1,-21,0.5,-9) or UDim2.new(0,3,0.5,-9)}, 0.2)
        end)
    end

    local function createAction(parent, title, desc, btnText, callback) -- 1:91
        local card = createCard(parent)
        local t = Instance.new("TextLabel", card)
        t.Position = UDim2.new(0,12,0,8)
        t.Size = UDim2.new(1,-110,0,16)
        t.BackgroundTransparency = 1
        t.Text = title; t.Font = Enum.Font.GothamBold; t.TextSize = 13; t.TextColor3 = Theme.Text; t.TextXAlignment = 0
        local d = Instance.new("TextLabel", card)
        d.Position = UDim2.new(0,12,0,26)
        d.Size = UDim2.new(1,-110,0,14)
        d.BackgroundTransparency = 1
        d.Text = desc; d.Font = Enum.Font.Gotham; d.TextSize = 11; d.TextColor3 = Theme.SubText; d.TextXAlignment = 0
        local b = Instance.new("TextButton", card)
        b.Size = UDim2.new(0, 88, 0, 30)
        b.Position = UDim2.new(1, -98, 0.5, -15)
        b.BackgroundColor3 = Theme.Accent
        b.Text = btnText; b.Font = Enum.Font.GothamBold; b.TextSize = 12; b.TextColor3 = Color3.new(1,1,1)
        Instance.new("UICorner", b).CornerRadius = UDim.new(0, 7)
        local g = Instance.new("UIGradient", b); g.Color = ColorSequence.new(Theme.Accent, Theme.Accent2); g.Rotation = 90
        b.MouseButton1Click:Connect(function() pcall(callback) end)
    end

    -- // SAYFALAR
    local cats = {
        {id="Movement", icon="◉", name="Movement", empty=true},
        {id="Player", icon="◎", name="Player", empty=true},
        {id="Combat", icon="⬢", name="Combat", empty=true},
        {id="Misc", icon="✦", name="Misc", empty=false},
    }
    for idx, cat in ipairs(cats) do
        local tab = Instance.new("TextButton", SideBar)
        tab.Size = UDim2.new(1, 0, 0, 38)
        tab.BackgroundColor3 = (cat.id=="Misc") and Theme.Accent or Color3.fromRGB(38,38,45)
        tab.Text = ""
        tab.AutoButtonColor = false
        Instance.new("UICorner", tab).CornerRadius = UDim.new(0, 8)
        if cat.id=="Misc" then local gg=Instance.new("UIGradient", tab); gg.Color=ColorSequence.new(Theme.Accent, Theme.Accent2); gg.Rotation=90 end
        local ico = Instance.new("TextLabel", tab)
        ico.Size = UDim2.new(0,26,1,0); ico.Position=UDim2.new(0,8,0,0); ico.BackgroundTransparency=1; ico.Text=cat.icon; ico.Font=Enum.Font.GothamBold; ico.TextSize=13; ico.TextColor3=Color3.new(1,1,1)
        local lbl = Instance.new("TextLabel", tab)
        lbl.Size = UDim2.new(1,-40,1,0); lbl.Position=UDim2.new(0,34,0,0); lbl.BackgroundTransparency=1; lbl.Text=cat.name; lbl.Font=Enum.Font.GothamBold; lbl.TextSize=12; lbl.TextColor3=Color3.new(1,1,1); lbl.TextXAlignment=0
        TabBtns[cat.id]=tab

        local page = Instance.new("ScrollingFrame", PageContainer)
        page.Size = UDim2.new(1,0,1,0)
        page.Visible = (cat.id=="Misc")
        page.BackgroundTransparency = 1
        page.ScrollBarThickness = 3
        page.ScrollBarImageColor3 = Theme.Accent
        page.CanvasSize = UDim2.new(0,0,0,0)
        page.AutomaticCanvasSize = Enum.AutomaticSize.Y
        local list = Instance.new("UIListLayout", page); list.Padding=UDim.new(0,8)
        local pad = Instance.new("UIPadding", page); pad.PaddingRight=UDim.new(0,4)
        Pages[cat.id]=page

        if cat.empty then
            local empty = Instance.new("Frame", page)
            empty.Size = UDim2.new(1,0,0,80); empty.BackgroundColor3=Theme.Card; Instance.new("UICorner", empty).CornerRadius=UDim.new(0,10)
            local et=Instance.new("TextLabel", empty); et.Size=UDim2.new(1,0,1,0); et.BackgroundTransparency=1; et.Text="Henüz özellik yok\nBoş kategori - eğitim şablonu"; et.Font=Enum.Font.Gotham; et.TextSize=12; et.TextColor3=Theme.SubText
        end

        tab.MouseButton1Click:Connect(function()
            for id,p in pairs(Pages) do p.Visible=false end
            page.Visible=true
            for id,btn in pairs(TabBtns) do
                tween(btn, {BackgroundColor3 = Color3.fromRGB(38,38,45)}, 0.15)
                for _,v in pairs(btn:GetChildren()) do if v:IsA("UIGradient") then v:Destroy() end end
            end
            tween(tab, {BackgroundColor3 = Theme.Accent}, 0.15)
            local gg=Instance.new("UIGradient", tab); gg.Color=ColorSequence.new(Theme.Accent, Theme.Accent2); gg.Rotation=90
        end)
    end

    -- // MISC İÇERİK
    local oldLight = {Brightness=Lighting.Brightness, ClockTime=Lighting.ClockTime, FogEnd=Lighting.FogEnd, GlobalShadows=Lighting.GlobalShadows, Ambient=Lighting.Ambient}
    local afkConn

    createToggle(Pages.Misc, "Anti-AFK", "AFK kick engelle • Idled koruması", function(s)
        if s then
            local VU = game:FindService("VirtualUser") or game:GetService("VirtualUser")
            afkConn = LocalPlayer.Idled:Connect(function()
                pcall(function() VU:CaptureController(); VU:ClickButton2(Vector2.new(0,0)) end)
            end)
        else if afkConn then afkConn:Disconnect() end end
    end)

    createToggle(Pages.Misc, "Fullbright", "Karanlıkta görme • GlobalShadows kapalı", function(s)
        if s then
            Lighting.Brightness=2; Lighting.ClockTime=14; Lighting.FogEnd=100000; Lighting.GlobalShadows=false; Lighting.Ambient=Color3.new(1,1,1)
        else
            Lighting.Brightness=oldLight.Brightness; Lighting.ClockTime=oldLight.ClockTime; Lighting.FogEnd=oldLight.FogEnd; Lighting.GlobalShadows=oldLight.GlobalShadows; Lighting.Ambient=oldLight.Ambient
        end
    end)

    createToggle(Pages.Misc, "No Fog", "Sis ve atmosferi kaldır", function(s)
        if s then
            Lighting.FogEnd=100000; Lighting.FogStart=0
            local atm = Lighting:FindFirstChildOfClass("Atmosphere"); if atm then atm.Density=0 end
        else Lighting.FogEnd=oldLight.FogEnd end
    end)

    local lastChat=0
    createAction(Pages.Misc, "Chat Gönder", "Flood korumalı • 3sn cooldown", "Gönder", function()
        if tick()-lastChat<3 then return end; lastChat=tick()
        pcall(function()
            if game:GetService("TextChatService").ChatVersion==Enum.ChatVersion.TextChatService then
                game:GetService("TextChatService").TextChannels.RBXGeneral:SendAsync("Merhaba! (Premium Hub v2)")
            else
                ReplicatedStorage:WaitForChild("DefaultChatSystemChatEvents"):WaitForChild("SayMessageRequest"):FireServer("Merhaba! (Premium Hub v2)","All")
            end
        end)
    end)

    createAction(Pages.Misc, "Rejoin", "Aynı sunucuya yeniden bağlan", "Rejoin", function()
        TeleportService:Teleport(game.PlaceId, LocalPlayer)
    end)

    createAction(Pages.Misc, "Server Hop", "Rastgele yeni sunucu bul", "Hop", function()
        pcall(function() TeleportService:Teleport(game.PlaceId, LocalPlayer) end)
    end)

    -- // ETKİLEŞİM: Sürükle / Minimize / Kapat / Tuşlar  (1:183)
    do
        local dragging, dragInput, dragStart, startPos
        TopBar.InputBegan:Connect(function(input)
            if input.UserInputType==Enum.UserInputType.MouseButton1 then
                dragging=true; dragStart=input.Position; startPos=MainFrame.Position
                input.Changed:Connect(function() if input.UserInputState==Enum.UserInputState.End then dragging=false end end)
            end
        end)
        TopBar.InputChanged:Connect(function(input) if input.UserInputType==Enum.UserInputType.MouseMovement then dragInput=input end end)
        UserInputService.InputChanged:Connect(function(input)
            if input==dragInput and dragging then
                local delta=input.Position-dragStart
                MainFrame.Position=UDim2.new(startPos.X.Scale, startPos.X.Offset+delta.X, startPos.Y.Scale, startPos.Y.Offset+delta.Y)
            end
        end)
    end

    local minimized=false
    MinBtn.MouseButton1Click:Connect(function()
        minimized=not minimized
        tween(Body, {Size = minimized and UDim2.new(1,0,0,0) or UDim2.new(1,0,1,-52)}, 0.25)
        tween(MainFrame, {Size = minimized and UDim2.new(0,620,0,52) or UDim2.new(0,620,0,420)}, 0.25)
        Body.Visible = not minimized -- tween bitince gizle yerine anında
        if minimized then Body.Visible=false else Body.Visible=true end
    end)
    CloseBtn.MouseButton1Click:Connect(function() tween(MainFrame,{Size=UDim2.new(0,0,0,0)},0.2) task.wait(0.2) ScreenGui.Enabled=false; MainFrame.Size=UDim2.new(0,620,0,420) end)

    UserInputService.InputBegan:Connect(function(input, gp)
        if gp then return end
        if input.KeyCode==Enum.KeyCode.RightShift then
            ScreenGui.Enabled = not ScreenGui.Enabled
            if ScreenGui.Enabled then tween(MainFrame,{Size=UDim2.new(0,620,0,420)},0.2) end
        elseif input.KeyCode==Enum.KeyCode.Escape then ScreenGui.Enabled=false end
    end)

    -- Açılış animasyonu
    MainFrame.Size = UDim2.new(0,0,0,0)
    tween(MainFrame, {Size = UDim2.new(0,620,0,420)}, 0.3)
end)

if not pcallSuccess then warn("[Premium Hub v2] Hata: "..tostring(err)) end
