do  local ui =  game:GetService("CoreGui").RobloxGui.Modules.Server.ServerPlayer.DefaultServerPlayerModules:FindFirstChild("GalixUI")  if ui then ui:Destroy() end end

local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")
local LocalPlayer = game:GetService("Players").LocalPlayer
local Mouse = LocalPlayer:GetMouse()

local GalixUI = Instance.new("ScreenGui")
GalixUI.Name = "GalixUI"
GalixUI.Parent = game:GetService("CoreGui").RobloxGui.Modules.Server.ServerPlayer.DefaultServerPlayerModules
GalixUI.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

if syn then
	syn.protect_gui(game:GetService("CoreGui").RobloxGui.Modules.Server.ServerPlayer.DefaultServerPlayerModules:FindFirstChild("GalixUI"))
end

local function tablefound(ta, object)
	for i,v in pairs(ta) do
		if v == object then
			return true
		end
	end
	return false
end

local function MakeDraggable(topbarobject, object)
	local Dragging = nil
	local DragInput = nil
	local DragStart = nil
	local StartPosition = nil

	local function Update(input)
		local Delta = input.Position - DragStart
		local pos =
			UDim2.new(
				StartPosition.X.Scale,
				StartPosition.X.Offset + Delta.X,
				StartPosition.Y.Scale,
				StartPosition.Y.Offset + Delta.Y
			)
		local Tween = TweenService:Create(object, TweenInfo.new(0.2), {Position = pos})
		Tween:Play()
	end

	topbarobject.InputBegan:Connect(
		function(input)
			if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
				Dragging = true
				DragStart = input.Position
				StartPosition = object.Position

				input.Changed:Connect(
					function()
						if input.UserInputState == Enum.UserInputState.End then
							Dragging = false
						end
					end
				)
			end
		end
	)

	topbarobject.InputChanged:Connect(
		function(input)
			if
				input.UserInputType == Enum.UserInputType.MouseMovement or
				input.UserInputType == Enum.UserInputType.Touch
			then
				DragInput = input
			end
		end
	)

	UserInputService.InputChanged:Connect(
		function(input)
			if input == DragInput and Dragging then
				Update(input)
			end
		end
	)
end

local Create = {}
    function Create:CreateWindow()
        local FocusUI = false ; -- tap

        local Main = Instance.new("Frame")
        Main.Name = "Main"
        Main.Parent = GalixUI
        Main.AnchorPoint = Vector2.new(0.5, 0.5)
        Main.BackgroundColor3 = Color3.fromRGB(224, 232, 241)
        Main.BorderSizePixel = 0
        Main.Position = UDim2.new(0.5, 0, 0.5, 0)
        Main.Size = UDim2.new(0, 500, 0, 0) -- UDim2.new(0, 500, 0, 500)
        Main.ClipsDescendants = true

		local UICorner = Instance.new("UICorner")
		UICorner.CornerRadius = UDim.new(0, 10)
		UICorner.Parent = Main

        local PageTab = Instance.new("Frame")
        PageTab.Name = "PageTab"
        PageTab.Parent = Main
        PageTab.BackgroundColor3 = Color3.fromRGB(200, 208, 221)
        PageTab.BorderSizePixel = 0
        PageTab.Position = UDim2.new(0, 0, 0.879999995, 0)
        PageTab.Size = UDim2.new(0, 500, 0, 60)

		local UICorner = Instance.new("UICorner")
		UICorner.CornerRadius = UDim.new(0, 10)
		UICorner.Parent = PageTab

        local PageTab_Frame = Instance.new("Frame")
        PageTab_Frame.Name = "PageTab_Frame"
        PageTab_Frame.Parent = PageTab
        PageTab_Frame.BackgroundColor3 = Color3.fromRGB(200, 208, 221)
        PageTab_Frame.BorderSizePixel = 0
        PageTab_Frame.Position = UDim2.new(0, 0, -0.00333353668, 0)
        PageTab_Frame.Size = UDim2.new(0, 500, 0, 30)

        local Scrolling_PageTab = Instance.new("ScrollingFrame")
        Scrolling_PageTab.Parent = PageTab
        Scrolling_PageTab.Active = true
        Scrolling_PageTab.AnchorPoint = Vector2.new(0.5, 0.5)
        Scrolling_PageTab.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
        Scrolling_PageTab.BackgroundTransparency = 1.000
        Scrolling_PageTab.BorderSizePixel = 0
        Scrolling_PageTab.Position = UDim2.new(0.5, 0, 0.5, 0)
        Scrolling_PageTab.Size = UDim2.new(0, 480, 0, 30)
        Scrolling_PageTab.CanvasSize = UDim2.new(0, 0, 0, 0)
        Scrolling_PageTab.ScrollBarThickness = 0

        local UIListLayout = Instance.new("UIListLayout")
        UIListLayout.Parent = Scrolling_PageTab
        UIListLayout.FillDirection = Enum.FillDirection.Horizontal
        UIListLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
        UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
        UIListLayout.VerticalAlignment = Enum.VerticalAlignment.Center
		UIListLayout.Padding = UDim.new(0, 10)

		local UIPaddingPage = Instance.new("UIPadding")
		UIPaddingPage.Parent = Scrolling_PageTab
		UIPaddingPage.PaddingTop = UDim.new(0, 0)

        
		Scrolling_PageTab.UIListLayout:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
			Scrolling_PageTab.CanvasSize =  UDim2.new(0,UIListLayout.AbsoluteContentSize.X +10,0,0)
		end);

		Scrolling_PageTab.UIListLayout:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
			Scrolling_PageTab.CanvasSize =  UDim2.new(0,UIListLayout.AbsoluteContentSize.X +10,0,0)
		end);

		local PageOrders = -1

		local Container_Page = Instance.new("Frame",Main)
		Container_Page.Name = ""
		Container_Page.BackgroundColor3 = Color3.fromRGB(25, 25, 255)
		Container_Page.Size = UDim2.new(0, 480, 0, 420)
		Container_Page.BackgroundTransparency = 1
		Container_Page.Position = UDim2.new(0.5, 0, 0.5, 0)
		Container_Page.AnchorPoint = Vector2.new(0.5, 0.57)
		Container_Page.ClipsDescendants = true
		
		local PageFolder = Instance.new("Folder")
		PageFolder.Parent = Container_Page

		local UIPage = Instance.new('UIPageLayout',PageFolder)
		UIPage.SortOrder = Enum.SortOrder.LayoutOrder
		UIPage.EasingDirection = Enum.EasingDirection.InOut
		UIPage.EasingStyle = Enum.EasingStyle.Circular
		UIPage.Padding = UDim.new(0, 500)
		UIPage.TweenTime = 0.350

        MakeDraggable(PageTab,Main)
		local tween = game:GetService("TweenService")
		local library = {currenttab = '',toggledui = false}
		tween:Create(Main,TweenInfo.new(1,Enum.EasingStyle.Circular),{Size = UDim2.new(0, 500, 0, 500)}):Play()

		game:GetService("UserInputService").InputBegan:Connect(function(input)
			if input.KeyCode == Enum.KeyCode.RightControl then 
				if library.toggledui == false then
					library.toggledui = true  
					tween:Create(Main,TweenInfo.new(0.5,Enum.EasingStyle.Circular,Enum.EasingDirection.In),{Size = UDim2.new(0, 500, 0, 0)}):Play()
					wait(0.5) Main.Visible = false
				else 
					library.toggledui = false
					Main.Visible = true
					tween:Create(Main,TweenInfo.new(0.5,Enum.EasingStyle.Circular),{Size = UDim2.new(0, 500, 0, 500)}):Play()
				end 
			end
		end)

local Tab = {}
    function Tab:CreateTab(text,Icon)
        PageOrders = PageOrders + 1
		local name = tostring(text) or tostring(math.random(1,5000))

        if Icon == nil then
            Icon = 11482711029
        end

        local Icon_Frame = Instance.new("Frame")
        Icon_Frame.Parent = Scrolling_PageTab
        Icon_Frame.BackgroundColor3 = Color3.fromRGB(160, 170, 180)
        Icon_Frame.BorderSizePixel = 0
        Icon_Frame.Size = UDim2.new(0, 30, 0, 30)
        Icon_Frame.BackgroundTransparency = 1

		local UICorner = Instance.new("UICorner")
		UICorner.CornerRadius = UDim.new(0, 6)
		UICorner.Parent = Icon_Frame

        local Icon_Button = Instance.new("ImageButton")
        Icon_Button.Name = text .. "Server"
        Icon_Button.Parent = Icon_Frame
        Icon_Button.AnchorPoint = Vector2.new(0.5, 0.5)
        Icon_Button.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
        Icon_Button.BackgroundTransparency = 1.000
        Icon_Button.BorderSizePixel = 0
        Icon_Button.Position = UDim2.new(0.5, 0, 0.5, 0)
        Icon_Button.Size = UDim2.new(0, 26, 0, 26)
        Icon_Button.Image = "http://www.roblox.com/asset/?id="..tostring(Icon)
        Icon_Button.ImageColor3 = Color3.fromRGB(110,130,150)

        local TextLabel_Tap = Instance.new("TextLabel")
        TextLabel_Tap.Name = "TextLabel_Tap"
        TextLabel_Tap.Parent = Icon_Frame
        TextLabel_Tap.BackgroundColor3 = Color3.fromRGB(40,60,90)
        TextLabel_Tap.BackgroundTransparency = 1
        TextLabel_Tap.AnchorPoint = Vector2.new(0.5, 0.5)
        TextLabel_Tap.Position = UDim2.new(0.5, 0, 0, 0)
        TextLabel_Tap.Size = UDim2.new(0,50,0,14)
        TextLabel_Tap.Font = Enum.Font.GothamBold
        TextLabel_Tap.Text = text
        TextLabel_Tap.Size = UDim2.new(0,15+ TextLabel_Tap.TextBounds.X ,0,14)
        TextLabel_Tap.TextTransparency = 1
        TextLabel_Tap.TextColor3 = Color3.fromRGB(20,180,255)
        TextLabel_Tap.TextSize = 10

        local UIGradient = Instance.new("UIGradient")
        UIGradient.Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(165, 180, 190)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(90, 110, 130))}
        UIGradient.Rotation = 90
        UIGradient.Transparency = NumberSequence.new{NumberSequenceKeypoint.new(0.00, 0.20), NumberSequenceKeypoint.new(1.00, 0.20)}
        UIGradient.Parent = Icon_Frame

        local PageMain = Instance.new("Frame")
        PageMain.Name = name.."_PageMain"
        PageMain.Parent = PageFolder
        PageMain.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
        PageMain.BackgroundTransparency = 1
        PageMain.BorderSizePixel = 0
        PageMain.Position = UDim2.new(0.0199999996, 0, 0.0199999996, 0)
        PageMain.Size = UDim2.new(0, 480, 0, 420)
        PageMain.Visible = true
		PageMain.ClipsDescendants = true
		PageMain.LayoutOrder = PageOrders

        local Scrolling_PageMain = Instance.new("ScrollingFrame")
        Scrolling_PageMain.Name = "Scrolling_PageMain"
        Scrolling_PageMain.Parent = PageMain
        Scrolling_PageMain.Active = true
        Scrolling_PageMain.AnchorPoint = Vector2.new(0.5, 0.5)
        Scrolling_PageMain.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
        Scrolling_PageMain.BackgroundTransparency = 1
        Scrolling_PageMain.BorderSizePixel = 0
        Scrolling_PageMain.Position = UDim2.new(0.5, 0, 0.5, 0)
        Scrolling_PageMain.Size = UDim2.new(0, 480, 0, 420)
        Scrolling_PageMain.ScrollBarImageColor3 = Color3.fromRGB(70, 80, 120)
        Scrolling_PageMain.BottomImage = "rbxasset://textures/ui/Scroll/scroll-middle.png"
        Scrolling_PageMain.CanvasSize = UDim2.new(0, 0, 0, 2)
        Scrolling_PageMain.ScrollBarThickness = 0
        Scrolling_PageMain.TopImage = "rbxasset://textures/ui/Scroll/scroll-middle.png"
        Scrolling_PageMain.Visible = true

        local UIListLayout = Instance.new("UIListLayout")
        UIListLayout.Parent = Scrolling_PageMain
        UIListLayout.FillDirection = Enum.FillDirection.Horizontal
        UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
        UIListLayout.Padding = UDim.new(0, 10)

        local UIPadding = Instance.new("UIPadding")
        UIPadding.Parent = Scrolling_PageMain
        UIPadding.PaddingLeft = UDim.new(0, 0)
        UIPadding.PaddingTop = UDim.new(0, 0)

        local PageLeft = Instance.new("Frame")
        PageLeft.Parent = Scrolling_PageMain
        PageLeft.BackgroundColor3 = Color3.fromRGB(255, 25, 255)
        PageLeft.BackgroundTransparency = 1
        PageLeft.BorderSizePixel = 0
        PageLeft.Size = UDim2.new(0, 235, 0, 420)
    
        local UIListLayout_Pageleft = Instance.new("UIListLayout")
        UIListLayout_Pageleft.Parent = PageLeft
        UIListLayout_Pageleft.FillDirection = Enum.FillDirection.Vertical
        UIListLayout_Pageleft.SortOrder = Enum.SortOrder.LayoutOrder
        UIListLayout_Pageleft.Padding = UDim.new(0, 10)

        local PageRight = Instance.new("Frame")
        PageRight.Parent = Scrolling_PageMain
        PageRight.BackgroundColor3 = Color3.fromRGB(255, 255, 25)
        PageRight.BackgroundTransparency = 1
        PageRight.BorderSizePixel = 0
        PageRight.Size = UDim2.new(0, 235, 0, 420)

        local UIListLayout_Pageright = Instance.new("UIListLayout")
        UIListLayout_Pageright.Parent = PageRight
        UIListLayout_Pageright.FillDirection = Enum.FillDirection.Vertical
        UIListLayout_Pageright.SortOrder = Enum.SortOrder.LayoutOrder
        UIListLayout_Pageright.Padding = UDim.new(0, 10)

        UIListLayout_Pageleft:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
            if UIListLayout_Pageleft.AbsoluteContentSize.Y > UIListLayout_Pageright.AbsoluteContentSize.Y then
                Scrolling_PageMain.CanvasSize = UDim2.new(0, 0, 0, UIListLayout_Pageleft.AbsoluteContentSize.Y + 20)
            end
        end)
        UIListLayout_Pageright:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
            if UIListLayout_Pageright.AbsoluteContentSize.Y > UIListLayout_Pageleft.AbsoluteContentSize.Y then
                Scrolling_PageMain.CanvasSize = UDim2.new(0, 0, 0, UIListLayout_Pageright.AbsoluteContentSize.Y + 20)
            end
        end)

		Icon_Button.MouseButton1Click:connect(function()
			if PageMain.Name == text.."_PageMain" then
				UIPage:JumpToIndex(PageMain.LayoutOrder)
			end

			for i ,v in next , Scrolling_PageTab:GetChildren() do
				if v:IsA("Frame") then
                    for o,p in pairs(v:GetChildren()) do
                        if p:IsA("ImageButton") then
                            TweenService:Create(
                                v,
                                TweenInfo.new(0.25, Enum.EasingStyle.Cubic, Enum.EasingDirection.Out),
                                {BackgroundTransparency = 1}
                            ):Play()
                            TweenService:Create(
                                p,
                                TweenInfo.new(0.25, Enum.EasingStyle.Cubic, Enum.EasingDirection.Out),
                                {ImageColor3 = Color3.fromRGB(110,130,150)}
                            ):Play()
                        end
                    end
				end
                TweenService:Create(
                    Icon_Frame,
                    TweenInfo.new(0.25, Enum.EasingStyle.Cubic, Enum.EasingDirection.Out),
                    {BackgroundTransparency = 0}
                ):Play()
                TweenService:Create(
                    Icon_Button,
                    TweenInfo.new(0.25, Enum.EasingStyle.Cubic, Enum.EasingDirection.Out),
                    {ImageColor3 = Color3.fromRGB(255, 255, 255)}
                ):Play()
			end
		end)
		if FocusUI == false then
            TweenService:Create(
                Icon_Frame,
                TweenInfo.new(0.25, Enum.EasingStyle.Cubic, Enum.EasingDirection.Out),
                {BackgroundTransparency = 0}
            ):Play()
            TweenService:Create(
                Icon_Button,
                TweenInfo.new(0.25, Enum.EasingStyle.Cubic, Enum.EasingDirection.Out),
                {ImageColor3 = Color3.fromRGB(255, 255, 255)}
            ):Play()

            PageMain.Visible = true
			Icon_Button.Name = text .. "Server"
			FocusUI  = true
		end

local Page = {}
    function Page:CreatePage(Type,text)
        local function GetType(value)
            if value == 1 then
                return PageLeft
            elseif value == 2 then
                return PageRight
            else
                return PageLeft
            end
        end

        local Page = Instance.new("Frame")
        Page.Parent = GetType(Type)
        Page.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
        Page.BackgroundTransparency = 0
        Page.BorderSizePixel = 0
        Page.AnchorPoint = Vector2.new(0.5,0.5)
        Page.Position = UDim2.new(0.5, 0, 0.5, 0)
        Page.Size = UDim2.new(0, 235, 0, 210)
        Page.Visible = true
        Page.ClipsDescendants = true 

		local UICorner = Instance.new("UICorner")
		UICorner.CornerRadius = UDim.new(0, 5)
		UICorner.Parent = Page

		local UIListLayout = Instance.new("UIListLayout")
		UIListLayout.Parent = Page
		UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
		UIListLayout.Padding = UDim.new(0, 5)

		local UIPaddingPage = Instance.new("UIPadding")
		UIPaddingPage.Parent = Page
		UIPaddingPage.PaddingLeft = UDim.new(0, 5)
		UIPaddingPage.PaddingTop = UDim.new(0, 5)

        local PageFrame = Instance.new("Frame")
        PageFrame.Parent = Page
        PageFrame.BackgroundColor3 = Color3.fromRGB(30, 50, 100)
        PageFrame.BackgroundTransparency = 1
        PageFrame.BorderSizePixel = 0
        PageFrame.AnchorPoint = Vector2.new(0.5,0.5)
        PageFrame.Position = UDim2.new(0.5, 0, 0.5, 0)
        PageFrame.Size = UDim2.new(0, 225, 0, 20)
        PageFrame.Visible = true
        PageFrame.ClipsDescendants = true 

		local Name_Page = Instance.new("TextLabel")
		Name_Page.Parent = PageFrame
		Name_Page.BackgroundColor3 = Color3.fromRGB(10,140,255)
		Name_Page.BackgroundTransparency = 1
		Name_Page.BorderSizePixel = 0
		Name_Page.Size = UDim2.new(0, 250, 0, 20)
        Name_Page.AnchorPoint = Vector2.new(0.5,0.5)
		Name_Page.Position = UDim2.new(0.5, 0, 0.4, 0)
		Name_Page.Font = Enum.Font.GothamBold
		Name_Page.TextColor3 = Color3.fromRGB(90,100,110)
		Name_Page.Text = tostring(text)
		Name_Page.TextSize = 13
		Name_Page.TextXAlignment = Enum.TextXAlignment.Center

        local PageLine = Instance.new("Frame")
		PageLine.Parent = PageFrame
		PageLine.BackgroundColor3 = Color3.fromRGB(90,100,110)
		PageLine.BackgroundTransparency = 0
		PageLine.BorderSizePixel = 0
        PageLine.AnchorPoint = Vector2.new(0.5,0.5)
		PageLine.Position = UDim2.new(0.5, 0, 0.9, 0)
        PageLine.Size = UDim2.new(0, 250, 0, 2)

		UIListLayout:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
			Page.Size =  UDim2.new(0, 235, 0,UIListLayout.AbsoluteContentSize.Y + 12)
		end);

local Items = {}
    function Items:Line()
        local Line_Frame = Instance.new("Frame")
        Line_Frame.Parent = Page
        Line_Frame.BackgroundColor3 = Color3.fromRGB(255,255,255)
        Line_Frame.BackgroundTransparency = 0
        Line_Frame.BorderSizePixel = 0
        Line_Frame.AnchorPoint = Vector2.new(0.5,0.5)
        Line_Frame.Position = UDim2.new(0.5, 0, 0.5, 0)
        Line_Frame.Size = UDim2.new(0, 225, 0, 5)

        local Line_Main = Instance.new("Frame")
        Line_Main.Parent = Line_Frame
        Line_Main.BackgroundColor3 = Color3.fromRGB(220, 230, 240)
        Line_Main.BackgroundTransparency = 0
        Line_Main.BorderSizePixel = 0
        Line_Main.AnchorPoint = Vector2.new(0.5,0.5)
        Line_Main.Position = UDim2.new(0.5, 0, 0.5, 0)
        Line_Main.Size = UDim2.new(0, 225, 0, 2)
        end

    function Items:TextLabel(value,text)
        local Label_Frame = Instance.new("Frame")
        Label_Frame.Parent = Page
        Label_Frame.BackgroundColor3 = Color3.fromRGB(25,25,25)
        Label_Frame.BackgroundTransparency = 1
        Label_Frame.BorderSizePixel = 0
        Label_Frame.AnchorPoint = Vector2.new(0.5,0.5)
        Label_Frame.Position = UDim2.new(0.5, 0, 0.5, 0)
        Label_Frame.Size = UDim2.new(0, 225, 0, 15)

        if value == 1 then
            local Labelfuc1 = {}
            local Label_Main1 = Instance.new("TextLabel")
            Label_Main1.Parent = Label_Frame
            Label_Main1.BackgroundColor3 = Color3.fromRGB(10,140,255)
            Label_Main1.BackgroundTransparency = 1
            Label_Main1.BorderSizePixel = 0
            Label_Main1.AnchorPoint = Vector2.new(0.5,0.5)
            Label_Main1.Position = UDim2.new(0.5, 0, 0.5, 0)
            Label_Main1.Size = UDim2.new(0, 225, 0, 15)
            Label_Main1.Font = Enum.Font.GothamMedium
            Label_Main1.TextColor3 = Color3.fromRGB(90,110,130)
            Label_Main1.Text = tostring(text)
            Label_Main1.TextSize = 13
            Label_Main1.TextXAlignment = Enum.TextXAlignment.Left
            function  Labelfuc1:Refresh(text)
                Label_Main1.Text = tostring(text)
            end
                return Labelfuc1
            end

        if value == 2 then
            local Labelfuc2 = {}
            local Label_Main2 = Instance.new("TextLabel")
            Label_Main2.Parent = Label_Frame
            Label_Main2.BackgroundColor3 = Color3.fromRGB(10,140,255)
            Label_Main2.BackgroundTransparency = 1
            Label_Main2.BorderSizePixel = 0
            Label_Main2.AnchorPoint = Vector2.new(0.5,0.5)
            Label_Main2.Position = UDim2.new(0.5, 0, 0.5, 0)
            Label_Main2.Size = UDim2.new(0, 225, 0, 15)
            Label_Main2.Font = Enum.Font.GothamMedium
            Label_Main2.TextColor3 = Color3.fromRGB(90,110,130)
            Label_Main2.Text = tostring(text)
            Label_Main2.TextSize = 13
            Label_Main2.TextXAlignment = Enum.TextXAlignment.Center
            function  Labelfuc2:Refresh(text)
                Label_Main2.Text = tostring(text)
            end
                return Labelfuc2
            end
        end

    function Items:Button1(text,callback)
		local Button_Frame = Instance.new("TextButton")
		Button_Frame.Parent = Page
		Button_Frame.BackgroundColor3 = Color3.fromRGB(250,255,255)
		Button_Frame.BackgroundTransparency = 1
		Button_Frame.BorderSizePixel = 0
		Button_Frame.AnchorPoint = Vector2.new(0.5,0.5)
		Button_Frame.Position = UDim2.new(0.5, 0, 0.5, 0)
		Button_Frame.Size = UDim2.new(0, 225, 0, 22)
		Button_Frame.Font = Enum.Font.GothamMedium
		Button_Frame.TextColor3 = Color3.fromRGB(255,255,255)
		Button_Frame.Text = ""
		Button_Frame.TextSize = 14.000

		local Button_Main = Instance.new("TextButton")
		Button_Main.Parent = Button_Frame
		Button_Main.BackgroundColor3 = Color3.fromRGB(220, 230, 240)
		Button_Main.BackgroundTransparency = 0
		Button_Main.BorderSizePixel = 0
		Button_Main.AnchorPoint = Vector2.new(0.5,0.5)
		Button_Main.Position = UDim2.new(0.5, 0, 0.5, 0)
		Button_Main.Size = UDim2.new(0, 195, 0, 22)
		Button_Main.Font = Enum.Font.GothamMedium
		Button_Main.TextColor3 = Color3.fromRGB(90,110,130)
		Button_Main.Text = tostring(text)
		Button_Main.TextSize = 13
        Button_Main.AutoButtonColor = false

		local UICorner = Instance.new("UICorner")
		UICorner.CornerRadius = UDim.new(0, 5)
		UICorner.Name = ""
		UICorner.Parent = Button_Main

		Button_Main.MouseButton1Click:Connect(function()
			TweenService:Create(
				Button_Main,
				TweenInfo.new(0.3, Enum.EasingStyle.Back, Enum.EasingDirection.Out),
				{Size = UDim2.new(0, 180, 0, 22)}
			):Play() wait(0.1)
			TweenService:Create(
				Button_Main,
				TweenInfo.new(0.3, Enum.EasingStyle.Back, Enum.EasingDirection.In),
				{Size = UDim2.new(0, 195, 0, 22)}
			):Play()
			TweenService:Create(
				Button_Main,
				TweenInfo.new(0.2, Enum.EasingStyle.Back, Enum.EasingDirection.Out),
				{TextSize = 11}
			):Play() wait(0.1)
			TweenService:Create(
				Button_Main,
				TweenInfo.new(0.2, Enum.EasingStyle.Back, Enum.EasingDirection.Out),
				{TextSize = 13}
			):Play()
			callback()
		end)
		end
    function Items:Button2(text1,text2,text3,callback)
		local Button_Main = Instance.new("Frame")
		Button_Main.Parent = Page
		Button_Main.BackgroundColor3 = Color3.fromRGB(220, 230, 240)
		Button_Main.BackgroundTransparency = 0
		Button_Main.BorderSizePixel = 0
		Button_Main.AnchorPoint = Vector2.new(0.5,0.5)
		Button_Main.Position = UDim2.new(0.5, 0, 0.5, 0)
		Button_Main.Size = UDim2.new(0, 225, 0, 40)

		local UICorner = Instance.new("UICorner")
		UICorner.CornerRadius = UDim.new(0, 5)
		UICorner.Name = ""
		UICorner.Parent = Button_Main

		local Button_Text1 = Instance.new("TextLabel")
		Button_Text1.Parent = Button_Main
		Button_Text1.BackgroundColor3 = Color3.fromRGB(220, 230, 240)
		Button_Text1.BackgroundTransparency = 1
		Button_Text1.BorderSizePixel = 0
		Button_Text1.AnchorPoint = Vector2.new(0.5,0.5)
		Button_Text1.Position = UDim2.new(0.5, 0, 0.325, 0)
		Button_Text1.Size = UDim2.new(0, 210, 0, 40)
		Button_Text1.Font = Enum.Font.GothamBold
		Button_Text1.TextColor3 = Color3.fromRGB(90,110,130)
		Button_Text1.Text = tostring(text1)
		Button_Text1.TextSize = 13
		Button_Text1.TextXAlignment = Enum.TextXAlignment.Left

		local Button_Text2 = Instance.new("TextLabel")
		Button_Text2.Parent = Button_Main
		Button_Text2.BackgroundColor3 = Color3.fromRGB(55, 55, 55)
		Button_Text2.BackgroundTransparency = 1.000
		Button_Text2.BorderSizePixel = 0
		Button_Text2.AnchorPoint = Vector2.new(0.5,0.5)
		Button_Text2.Position = UDim2.new(0.5, 0, 0.7, 0)
		Button_Text2.Size = UDim2.new(0, 210, 0, 40)
		Button_Text2.Font = Enum.Font.GothamMedium
		Button_Text2.TextColor3 = Color3.fromRGB(90,110,130)
		Button_Text2.Text = tostring(text2)
		Button_Text2.TextSize = 12
		Button_Text2.TextXAlignment = Enum.TextXAlignment.Left

		local Button_Frame = Instance.new("TextButton")
		Button_Frame.Parent = Button_Main
		Button_Frame.BackgroundColor3 = Color3.fromRGB(190,200,210)
		Button_Frame.AnchorPoint = Vector2.new(0.5,0.5)
		Button_Frame.Position = UDim2.new(0.85, 0, 0.5, 0)
		Button_Frame.Size = UDim2.new(0, 50, 0, 20)
        Button_Frame.AutoButtonColor = false
        Button_Frame.Text = ""

		local UICorner = Instance.new("UICorner")
		UICorner.CornerRadius = UDim.new(0, 360)
		UICorner.Name = ""
		UICorner.Parent = Button_Frame

		local Button_Text3 = Instance.new("TextLabel")
		Button_Text3.Parent = Button_Frame
		Button_Text3.BackgroundColor3 = Color3.fromRGB(55, 55, 55)
		Button_Text3.BackgroundTransparency = 1.000
		Button_Text3.BorderSizePixel = 0
		Button_Text3.AnchorPoint = Vector2.new(0.5,0.5)
		Button_Text3.Position = UDim2.new(0.5, 0, 0.5, 0)
		Button_Text3.Size = UDim2.new(0, 50, 0, 20)
		Button_Text3.Font = Enum.Font.GothamMedium
		Button_Text3.TextColor3 = Color3.fromRGB(90,110,130)
		Button_Text3.Text = tostring(text3)
		Button_Text3.TextSize = 12
		Button_Text3.TextXAlignment = Enum.TextXAlignment.Center

		Button_Frame.MouseButton1Click:Connect(function()

            TweenService:Create(
				Button_Frame,
				TweenInfo.new(0.3, Enum.EasingStyle.Back, Enum.EasingDirection.Out),
				{BackgroundColor3 = Color3.fromRGB(90,110,130)}
			):Play() wait(0.1)
            TweenService:Create(
				Button_Text3,
				TweenInfo.new(0.3, Enum.EasingStyle.Back, Enum.EasingDirection.Out),
				{TextColor3 = Color3.fromRGB(255,255,255)}
			):Play() wait(0.1)
			TweenService:Create(
				Button_Frame,
				TweenInfo.new(0.3, Enum.EasingStyle.Back, Enum.EasingDirection.In),
				{BackgroundColor3 = Color3.fromRGB(190,200,210)}
			):Play()
            TweenService:Create(
				Button_Text3,
				TweenInfo.new(0.3, Enum.EasingStyle.Back, Enum.EasingDirection.In),
				{TextColor3 = Color3.fromRGB(90,110,130)}
			):Play()
			callback()
		end)
		end
    function Items:Toggle(text1,text2,Stats,callback)
		local Toggle_Main = Instance.new("Frame")
		Toggle_Main.Parent = Page
		Toggle_Main.BackgroundColor3 = Color3.fromRGB(220, 230, 240)
        Toggle_Main.BackgroundTransparency = 0
		Toggle_Main.BorderSizePixel = 0
		Toggle_Main.AnchorPoint = Vector2.new(0.5,0.5)
		Toggle_Main.Position = UDim2.new(0.5, 0, 0.5, 0)
		Toggle_Main.Size = UDim2.new(0, 225, 0, 40)

		local UICorner = Instance.new("UICorner")
		UICorner.CornerRadius = UDim.new(0, 5)
		UICorner.Name = ""
		UICorner.Parent = Toggle_Main

		local TextButton_Toggle1 = Instance.new("TextButton")
		TextButton_Toggle1.Parent = Toggle_Main
		TextButton_Toggle1.BackgroundColor3 = Color3.fromRGB(55, 55, 55)
		TextButton_Toggle1.BackgroundTransparency = 1.000
		TextButton_Toggle1.BorderSizePixel = 0
		TextButton_Toggle1.AnchorPoint = Vector2.new(0.5,0.5)
		TextButton_Toggle1.Position = UDim2.new(0.5, 0, 0.325, 0)
		TextButton_Toggle1.Size = UDim2.new(0, 210, 0, 40)
		TextButton_Toggle1.Font = Enum.Font.GothamBold
		TextButton_Toggle1.TextColor3 = Color3.fromRGB(90,110,130)
		TextButton_Toggle1.Text = tostring(text1)
		TextButton_Toggle1.TextSize = 13
		TextButton_Toggle1.TextXAlignment = Enum.TextXAlignment.Left
		
		local TextButton_Toggle2 = Instance.new("TextLabel")
		TextButton_Toggle2.Parent = Toggle_Main
		TextButton_Toggle2.BackgroundColor3 = Color3.fromRGB(55, 55, 55)
		TextButton_Toggle2.BackgroundTransparency = 1.000
		TextButton_Toggle2.BorderSizePixel = 0
		TextButton_Toggle2.AnchorPoint = Vector2.new(0.5,0.5)
		TextButton_Toggle2.Position = UDim2.new(0.5, 0, 0.7, 0)
		TextButton_Toggle2.Size = UDim2.new(0, 210, 0, 40)
		TextButton_Toggle2.Font = Enum.Font.GothamMedium
		TextButton_Toggle2.TextColor3 = Color3.fromRGB(90,110,130)
		TextButton_Toggle2.Text = tostring(text2)
		TextButton_Toggle2.TextSize = 12
		TextButton_Toggle2.TextXAlignment = Enum.TextXAlignment.Left

		local Toggle_Frame = Instance.new("Frame")
		Toggle_Frame.Parent = Toggle_Main
		Toggle_Frame.BackgroundColor3 = Color3.fromRGB(190,200,210)
		Toggle_Frame.AnchorPoint = Vector2.new(0.5,0.5)
		Toggle_Frame.Position = UDim2.new(0.9, 0, 0.5, 0)
		Toggle_Frame.Size = UDim2.new(0, 30, 0, 20)

		local UICorner = Instance.new("UICorner")
		UICorner.CornerRadius = UDim.new(0, 360)
		UICorner.Name = ""
		UICorner.Parent = Toggle_Frame

		local Toggle1 = Instance.new("Frame")
		Toggle1.Parent = Toggle_Frame
		Toggle1.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		Toggle1.AnchorPoint = Vector2.new(0.5,0.5)
		Toggle1.Position = UDim2.new(0.35, 0, 0.5, 0)
		Toggle1.Size = UDim2.new(0, 16, 0, 16)
        
		local UICorner = Instance.new("UICorner")
		UICorner.CornerRadius = UDim.new(0, 360)
		UICorner.Name = ""
		UICorner.Parent = Toggle1
		-- Lock Function
		local lockerframe = Instance.new("Frame")
		lockerframe.Name = "lockerframe"
		lockerframe.Parent = Toggle_Main
		lockerframe.BackgroundColor3 = Color3.fromRGB(20,180,255)
		lockerframe.BackgroundTransparency = 1
		lockerframe.Size = UDim2.new(0, 225, 0, 40)
		lockerframe.Position = UDim2.new(0.5, 0, 0.5, 0)
		lockerframe.AnchorPoint = Vector2.new(0.5, 0.5)

		local UICorner_Toggle = Instance.new("UICorner")
		UICorner_Toggle.CornerRadius = UDim.new(0, 5)
		UICorner_Toggle.Parent = lockerframe

		local LockerImage = Instance.new("ImageLabel")
		LockerImage.Parent = lockerframe
		LockerImage.BackgroundTransparency = 1.000
		LockerImage.BorderSizePixel = 0
		LockerImage.Position = UDim2.new(0.5, 0, 0.5, 0)
		LockerImage.AnchorPoint = Vector2.new(0.5, 0.5)
		LockerImage.Size = UDim2.new(0, 0, 0, 0)
		LockerImage.Image = "http://www.roblox.com/asset/?id=7072718362"
		LockerImage.ImageColor3 = Color3.fromRGB(255,255,255)
		--
		local check = {Toggle = false ; lock = true ; togglefunction = {}; }
		TextButton_Toggle1.MouseButton1Down:Connect(function()
			if check.Toggle == false  and check.lock == true  then ------- true
                TweenService:Create(
					Toggle1,
					TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
					{Position = UDim2.new(0.65, 0, 0.5, 0)}
				):Play()
                TweenService:Create(
					Toggle_Frame,
					TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
					{BackgroundColor3 = Color3.fromRGB(90,110,130)}
				):Play()
                TweenService:Create(
					Toggle1,
					TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
					{BackgroundColor3 = Color3.fromRGB(140,160,180)}
				):Play()
			elseif check.lock == true then
                TweenService:Create(
					Toggle1,
					TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
					{Position = UDim2.new(0.35, 0, 0.5, 0)}
				):Play()
                TweenService:Create(
					Toggle_Frame,
					TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
					{BackgroundColor3 = Color3.fromRGB(190,200,210)}
				):Play()
                TweenService:Create(
					Toggle1,
					TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
					{BackgroundColor3 = Color3.fromRGB(255,255,255)}
				):Play()
			end
			if check.lock == true then
				check.Toggle = not check.Toggle
				pcall(callback,check.Toggle)
			end
		end)

		if Stats == true then
            TweenService:Create(
                Toggle1,
                TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
                {Position = UDim2.new(0.65, 0, 0.5, 0)}
            ):Play()
            TweenService:Create(
                Toggle_Frame,
                TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
                {BackgroundColor3 = Color3.fromRGB(90,110,130)}
            ):Play()
            TweenService:Create(
                Toggle1,
                TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
                {BackgroundColor3 = Color3.fromRGB(140,160,180)}
            ):Play()
            
			check.Toggle = not check.Toggle
			pcall(callback,check.Toggle)
		end
		-- Function Lock
		function check.togglefunction:lock()
			TweenService:Create(
				lockerframe,
				TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
				{BackgroundTransparency = 0.5}
			):Play() wait(0.2)
			--
			TweenService:Create(
				LockerImage,
				TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
				{Size = UDim2.new(0, 20, 0, 20)}
			):Play()
			-- Tween Lock
			TweenService:Create(
				LockerImage,
				TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
				{Rotation = -50}
			):Play() wait(0.3)
			TweenService:Create(
				LockerImage,
				TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
				{Rotation = 50}
			):Play() wait(0.2)
			TweenService:Create(
				LockerImage,
				TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
				{Rotation = -30}
			):Play() wait(0.2)
			TweenService:Create(
				LockerImage,
				TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
				{Rotation = 30}
			):Play() wait(0.2)
			TweenService:Create(
				LockerImage,
				TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
				{Rotation = 0}
			):Play() wait(0.1)
			check.lock  = false
		end
		function check.togglefunction:unlock()
			-- Tween UnLock
			TweenService:Create(
				LockerImage,
				TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
				{Rotation = -30}
			):Play() wait(0.3)
			TweenService:Create(
				LockerImage,
				TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
				{Rotation = 30}
			):Play() wait(0.2)
			TweenService:Create(
				LockerImage,
				TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
				{Rotation = -50}
			):Play() wait(0.2)
			TweenService:Create(
				LockerImage,
				TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
				{Rotation = 50}
			):Play() wait(0.2)
			TweenService:Create(
				LockerImage,
				TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
				{Rotation = 0}
			):Play() wait(0.1)
			--
            TweenService:Create(
				LockerImage,
				TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
				{Size = UDim2.new(0, 0, 0, 0)}
			):Play() wait(0.3)
            TweenService:Create(
				lockerframe,
				TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out,0.1),
				{BackgroundTransparency = 1}
			):Play()
			check.lock  = true
		end
		-- Tween
		Toggle_Main.MouseEnter:Connect(function()
			if check.lock == false then
				TweenService:Create(
					LockerImage,
					TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
					{Rotation = -50}
				):Play() wait(0.3)
				TweenService:Create(
					LockerImage,
					TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
					{Rotation = 50}
				):Play() wait(0.3)
				TweenService:Create(
					LockerImage,
					TweenInfo.new(0.6, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
					{Rotation = -70}
				):Play() wait(0.3)
				TweenService:Create(
					LockerImage,
					TweenInfo.new(0.6, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
					{Rotation = 70}
				):Play() wait(0.3)
				TweenService:Create(
					LockerImage,
					TweenInfo.new(0.6, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
					{Rotation = -30}
				):Play() wait(0.3)
				TweenService:Create(
					LockerImage,
					TweenInfo.new(0.6, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
					{Rotation = 30}
				):Play() wait(0.3)
				TweenService:Create(
					LockerImage,
					TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
					{Rotation = 0}
				):Play()
			end
		end)
		Toggle_Main.MouseLeave:Connect(function()
			if check.lock == false then
				TweenService:Create(
					LockerImage,
					TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
					{Rotation = 50}
				):Play() wait(0.3)
				TweenService:Create(
					LockerImage,
					TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
					{Rotation = -50}
				):Play() wait(0.3)
				TweenService:Create(
					LockerImage,
					TweenInfo.new(0.6, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
					{Rotation = 70}
				):Play() wait(0.3)
				TweenService:Create(
					LockerImage,
					TweenInfo.new(0.6, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
					{Rotation = -70}
				):Play() wait(0.3)
				TweenService:Create(
					LockerImage,
					TweenInfo.new(0.6, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
					{Rotation = 30}
				):Play() wait(0.3)
				TweenService:Create(
					LockerImage,
					TweenInfo.new(0.6, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
					{Rotation = -30}
				):Play() wait(0.3)
				TweenService:Create(
					LockerImage,
					TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
					{Rotation = 0}
				):Play()
			end
			--
		end)
		    return  check.togglefunction
		end

    function Items:Dropdown(text,option,callback)
        local DropDown_Main = Instance.new("Frame")
        DropDown_Main.Name = "DropFrame"
        DropDown_Main.Parent = Page
        DropDown_Main.BackgroundColor3 = Color3.fromRGB(220,230,240)
        DropDown_Main.BackgroundTransparency = 0
        DropDown_Main.BorderSizePixel = 0
        DropDown_Main.AnchorPoint = Vector2.new(0.5, 0.5)
        DropDown_Main.Position = UDim2.new(0.5, 0, 0.5, 0)
        DropDown_Main.Size = UDim2.new(0, 225, 0, 30)
        DropDown_Main.ClipsDescendants = true

        local UICorner = Instance.new("UICorner")
        UICorner.CornerRadius = UDim.new(0, 5)
        UICorner.Name = ""
        UICorner.Parent = DropDown_Main

        local DropDown_Frame = Instance.new("Frame")
        DropDown_Frame.Name = "LabelFrameDrop"
        DropDown_Frame.Parent = DropDown_Main
        DropDown_Frame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
        DropDown_Frame.BackgroundTransparency = 1
        DropDown_Frame.Position = UDim2.new(0.05, 0, 0, 0)
        DropDown_Frame.Size = UDim2.new(0, 215, 0, 30)

        local TextLabe_DropDown = Instance.new("TextLabel")
        TextLabe_DropDown.Name = "LabelFrameDrop"
        TextLabe_DropDown.Parent = DropDown_Frame
        TextLabe_DropDown.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
        TextLabe_DropDown.BackgroundTransparency = 1
        TextLabe_DropDown.AnchorPoint = Vector2.new(0.5, 0.5)
        TextLabe_DropDown.Position = UDim2.new(0.5, 0, 0.5, 0)
        TextLabe_DropDown.Size = UDim2.new(0, 215, 0, 30)
        TextLabe_DropDown.Font = Enum.Font.GothamBold
        TextLabe_DropDown.TextColor3 = Color3.fromRGB(90,110,130)
        TextLabe_DropDown.TextSize = 13
        TextLabe_DropDown.TextWrapped = true
        TextLabe_DropDown.TextXAlignment = Enum.TextXAlignment.Left
        TextLabe_DropDown.Text = tostring(text).." :"

        local Icon = Instance.new("ImageLabel")
		Icon.Name = "Icon"
		Icon.Parent = TextLabe_DropDown
		Icon.BackgroundColor3 = Color3.fromRGB(25, 35, 60)
		Icon.BackgroundTransparency = 1
		Icon.AnchorPoint = Vector2.new(0.5,0.5)
		Icon.Position = UDim2.new(0.915, 0, 0.5, 0)
		Icon.Rotation = 0
		Icon.Size = UDim2.new(0, 20, 0, 20)
		Icon.Image = "http://www.roblox.com/asset/?id=11318419925"
		Icon.ImageColor3 = Color3.fromRGB(90,110,130)

        local Dropdown_Button = Instance.new("TextButton")
        Dropdown_Button.Name = "DropFrame"
        Dropdown_Button.Parent = DropDown_Frame
        Dropdown_Button.BackgroundColor3 = Color3.fromRGB(20,20,20)
        Dropdown_Button.BackgroundTransparency = 1
        Dropdown_Button.BorderSizePixel = 0
        Dropdown_Button.AnchorPoint = Vector2.new(0.5, 0.5)
        Dropdown_Button.Position = UDim2.new(0.5, 0, 0.5, 0)
        Dropdown_Button.Size = UDim2.new(0, 225, 0, 35)
        Dropdown_Button.Text = ""
        Dropdown_Button.AutoButtonColor = false
        Dropdown_Button.ClipsDescendants = true

		local Scrolling_Dropdown = Instance.new("ScrollingFrame")
		Scrolling_Dropdown.Name = "Scrolling_Drop"
		Scrolling_Dropdown.Parent = DropDown_Frame
		Scrolling_Dropdown.Active = true
		Scrolling_Dropdown.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		Scrolling_Dropdown.BackgroundTransparency = 1
		Scrolling_Dropdown.BorderSizePixel = 0
		Scrolling_Dropdown.AnchorPoint = Vector2.new(0.5,0.5)
		Scrolling_Dropdown.Position = UDim2.new(0.4715, 0, 3.125, 0)
		Scrolling_Dropdown.Size = UDim2.new(0, 210, 0, 125)
        Scrolling_Dropdown.BottomImage = "rbxasset://textures/ui/Scroll/scroll-middle.png"
        Scrolling_Dropdown.CanvasSize = UDim2.new(0, 0, 0, 0)
        Scrolling_Dropdown.ScrollBarThickness = 4
        Scrolling_Dropdown.TopImage = "rbxasset://textures/ui/Scroll/scroll-middle.png"
        Scrolling_Dropdown.ScrollBarImageColor3 = Color3.fromRGB(90, 110, 130)
		Scrolling_Dropdown.ScrollBarImageTransparency = 0

		local UIListLayout = Instance.new("UIListLayout")
		UIListLayout.Name = "UIListLayout"
		UIListLayout.Parent = Scrolling_Dropdown
		UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
		UIListLayout.Padding = UDim.new(0, 4)

		local UIPaddinglist = Instance.new("UIPadding")
		UIPaddinglist.Name = "UIPaddinglist"
		UIPaddinglist.Parent = Scrolling_Dropdown
		UIPaddinglist.PaddingTop = UDim.new(0, 7)
        UIPaddinglist.PaddingLeft = UDim.new(0, 0)

        local Dropdown = false
        Dropdown_Tween = true
		local FrameSize = 145
		local cout = 0
		for i , v in pairs(option) do
			cout =cout + 1
			if cout == 1 then
				FrameSize = 145
			elseif cout == 2 then
				FrameSize = 145
			elseif cout >= 3 then
				FrameSize = 145
			end

		local Button_Frame = Instance.new("Frame")
		Button_Frame.Name = "ListFrame"
		Button_Frame.Parent = Scrolling_Dropdown
		Button_Frame.BackgroundColor3 = Color3.fromRGB(15,15,15)
		Button_Frame.BackgroundTransparency = 1
		Button_Frame.BorderSizePixel = 0
		Button_Frame.AnchorPoint = Vector2.new(0.5, 0.5)
		Button_Frame.Position = UDim2.new(0.5, 0, 0.5, 0)
		Button_Frame.Size = UDim2.new(0, 210, 0, 30)
            
		local Button_DropDown = Instance.new("TextButton")
		Button_DropDown.Name = "Dropdwon_Button"
		Button_DropDown.Parent = Button_Frame
		Button_DropDown.AnchorPoint = Vector2.new(0.5, 0.5)
		Button_DropDown.BackgroundColor3 = Color3.fromRGB(200,210,220)
		Button_DropDown.BackgroundTransparency = 0
		Button_DropDown.BorderSizePixel = 0
		Button_DropDown.Position = UDim2.new(0.5, 0, 0.5, 0)
		Button_DropDown.Size = UDim2.new(0, 190, 0, 25)
		Button_DropDown.Font = Enum.Font.GothamSemibold
		Button_DropDown.TextColor3 = Color3.fromRGB(90, 110, 130)
		Button_DropDown.TextSize = 13
		Button_DropDown.TextXAlignment = Enum.TextXAlignment.Left
		Button_DropDown.Text = ""
        Button_DropDown.AutoButtonColor  = false

		local UICorner = Instance.new("UICorner")
		UICorner.CornerRadius = UDim.new(0, 5)
		UICorner.Name = ""
		UICorner.Parent = Button_DropDown

		local TextLabel_Button = Instance.new("TextLabel")
		TextLabel_Button.Name = "TextLabel_TapDro2p"
		TextLabel_Button.Parent = Button_DropDown
		TextLabel_Button.AnchorPoint = Vector2.new(0.5, 0.5)
		TextLabel_Button.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		TextLabel_Button.BackgroundTransparency = 1
		TextLabel_Button.Position = UDim2.new(0.5, 0, 0.5, 0)
		TextLabel_Button.Size = UDim2.new(0, 190, 0, 30)
		TextLabel_Button.Font = Enum.Font.GothamSemibold
		TextLabel_Button.TextColor3 = Color3.fromRGB(90,110,130)
		TextLabel_Button.TextSize = 14
		TextLabel_Button.TextXAlignment = Enum.TextXAlignment.Center
		TextLabel_Button.Text = tostring(v)

		Button_DropDown.MouseButton1Click:Connect(function()
			TweenService:Create(
				DropDown_Main,
				TweenInfo.new(0.3, Enum.EasingStyle.Linear, Enum.EasingDirection.Out),
				{Size = UDim2.new(0, 225, 0, 30)}
			):Play() wait(0.3)
			TweenService:Create(
				Icon,
				TweenInfo.new(0.3, Enum.EasingStyle.Linear, Enum.EasingDirection.Out),
				{Rotation = 0}
			):Play()
				TextLabe_DropDown.Text = tostring(text).." : "..tostring(v)
				callback(v)
				Dropdown = not Dropdown
			end)
		end
        
        Dropdown_Button.MouseButton1Click:Connect(function()
			if Dropdown == false then
				TweenService:Create(
					DropDown_Main,
					TweenInfo.new(0.3, Enum.EasingStyle.Linear, Enum.EasingDirection.Out),
					{Size = UDim2.new(0, 225, 0, FrameSize)}
				):Play()
				TweenService:Create(
					Icon,
					TweenInfo.new(0.3, Enum.EasingStyle.Linear, Enum.EasingDirection.Out),
					{Rotation = 90}
				):Play()
			    Scrolling_Dropdown.CanvasSize = UDim2.new(0,0,0,UIListLayout.AbsoluteContentSize.Y + 25 )
			else
				TweenService:Create(
					DropDown_Main,
					TweenInfo.new(0.3, Enum.EasingStyle.Linear, Enum.EasingDirection.Out),
					{Size = UDim2.new(0, 225, 0, 30)}
				):Play()
				TweenService:Create(
					Icon,
					TweenInfo.new(0.3, Enum.EasingStyle.Linear, Enum.EasingDirection.Out),
					{Rotation = 0}
				):Play()
				Scrolling_Dropdown.CanvasSize = UDim2.new(0,0,0,UIListLayout.AbsoluteContentSize.Y + 25 )
			end
			Dropdown = not Dropdown
            Dropdown_Tween = false
		end)

        Scrolling_Dropdown.CanvasSize = UDim2.new(0,0,0,UIListLayout.AbsoluteContentSize.Y + 25 )
        local dropfunc = {}

		function dropfunc:Clear()
			TextLabe_DropDown.Text = tostring(text).." :"
			TweenService:Create(
				DropDown_Main,
				TweenInfo.new(0.3, Enum.EasingStyle.Linear, Enum.EasingDirection.Out),
				{Size = UDim2.new(0, 225, 0, 30)}
			):Play()
			TweenService:Create(
				Icon,
				TweenInfo.new(0.3, Enum.EasingStyle.Linear, Enum.EasingDirection.Out),
				{Rotation = 0}
			):Play()
			Dropdown = not Dropdown
			Dropdown_Tween = true
			for i, v in next, Scrolling_Dropdown:GetChildren() do
				if v:IsA("Frame") then
					v:Destroy()
				end
			end
		end

		function dropfunc:Add(t)
            local Button_Frame = Instance.new("Frame")
            Button_Frame.Name = "ListFrame"
            Button_Frame.Parent = Scrolling_Dropdown
            Button_Frame.BackgroundColor3 = Color3.fromRGB(15,15,15)
            Button_Frame.BackgroundTransparency = 1
            Button_Frame.BorderSizePixel = 0
            Button_Frame.AnchorPoint = Vector2.new(0.5, 0.5)
            Button_Frame.Position = UDim2.new(0.5, 0, 0.5, 0)
            Button_Frame.Size = UDim2.new(0, 210, 0, 30)
                
            local Button_DropDown = Instance.new("TextButton")
            Button_DropDown.Name = "Dropdwon_Button"
            Button_DropDown.Parent = Button_Frame
            Button_DropDown.AnchorPoint = Vector2.new(0.5, 0.5)
            Button_DropDown.BackgroundColor3 = Color3.fromRGB(190,200,210)
            Button_DropDown.BackgroundTransparency = 0
            Button_DropDown.BorderSizePixel = 0
            Button_DropDown.Position = UDim2.new(0.5, 0, 0.5, 0)
            Button_DropDown.Size = UDim2.new(0, 190, 0, 25)
            Button_DropDown.Font = Enum.Font.GothamSemibold
            Button_DropDown.TextColor3 = Color3.fromRGB(90, 110, 130)
            Button_DropDown.TextSize = 13
            Button_DropDown.TextXAlignment = Enum.TextXAlignment.Left
            Button_DropDown.Text = ""
            Button_DropDown.AutoButtonColor  = false
    
            local UICorner = Instance.new("UICorner")
            UICorner.CornerRadius = UDim.new(0, 5)
            UICorner.Name = ""
            UICorner.Parent = Button_DropDown
    
            local TextLabel_Button = Instance.new("TextLabel")
            TextLabel_Button.Name = "TextLabel_TapDro2p"
            TextLabel_Button.Parent = Button_DropDown
            TextLabel_Button.AnchorPoint = Vector2.new(0.5, 0.5)
            TextLabel_Button.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
            TextLabel_Button.BackgroundTransparency = 1
            TextLabel_Button.Position = UDim2.new(0.5, 0, 0.5, 0)
            TextLabel_Button.Size = UDim2.new(0, 190, 0, 30)
            TextLabel_Button.Font = Enum.Font.GothamSemibold
            TextLabel_Button.TextColor3 = Color3.fromRGB(90,110,130)
            TextLabel_Button.TextSize = 14
            TextLabel_Button.TextXAlignment = Enum.TextXAlignment.Center
            TextLabel_Button.Text = tostring(t)
            
		Button_DropDown.MouseButton1Click:Connect(function()
			TweenService:Create(
				DropDown_Main,
				TweenInfo.new(0.3, Enum.EasingStyle.Linear, Enum.EasingDirection.Out),
				{Size = UDim2.new(0, 225, 0, 30)}
			):Play() wait(0.3)
			TweenService:Create(
				Icon,
				TweenInfo.new(0.3, Enum.EasingStyle.Linear, Enum.EasingDirection.Out),
				{Rotation = 0}
			):Play()
				TextLabe_DropDown.Text = tostring(text).." : "..tostring(t)
				callback(t)
				Dropdown = not Dropdown
                Dropdown_Tween = false
			end)
			Scrolling_Dropdown.CanvasSize = UDim2.new(0,0,0,UIListLayout.AbsoluteContentSize.Y + 25)
        end
            return dropfunc
        end

	function Items:MultiDropdown(text,option,default,callback)
		local defaultt = default or {}
		local MultiDropdownTable = {}

        local DropDown_Main = Instance.new("Frame")
        DropDown_Main.Name = "DropFrame"
        DropDown_Main.Parent = Page
        DropDown_Main.BackgroundColor3 = Color3.fromRGB(220,230,240)
        DropDown_Main.BackgroundTransparency = 0
        DropDown_Main.BorderSizePixel = 0
        DropDown_Main.AnchorPoint = Vector2.new(0.5, 0.5)
        DropDown_Main.Position = UDim2.new(0.5, 0, 0.5, 0)
        DropDown_Main.Size = UDim2.new(0, 225, 0, 30)
        DropDown_Main.ClipsDescendants = true

        local UICorner = Instance.new("UICorner")
        UICorner.CornerRadius = UDim.new(0, 5)
        UICorner.Name = ""
        UICorner.Parent = DropDown_Main

        local DropDown_Frame = Instance.new("Frame")
        DropDown_Frame.Name = "LabelFrameDrop"
        DropDown_Frame.Parent = DropDown_Main
        DropDown_Frame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
        DropDown_Frame.BackgroundTransparency = 1
        DropDown_Frame.Position = UDim2.new(0.05, 0, 0, 0)
        DropDown_Frame.Size = UDim2.new(0, 215, 0, 30)

        local TextLabe_DropDown = Instance.new("TextLabel")
        TextLabe_DropDown.Name = "LabelFrameDrop"
        TextLabe_DropDown.Parent = DropDown_Frame
        TextLabe_DropDown.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
        TextLabe_DropDown.BackgroundTransparency = 1
        TextLabe_DropDown.AnchorPoint = Vector2.new(0.5, 0.5)
        TextLabe_DropDown.Position = UDim2.new(0.5, 0, 0.5, 0)
        TextLabe_DropDown.Size = UDim2.new(0, 215, 0, 30)
        TextLabe_DropDown.Font = Enum.Font.GothamBold
        TextLabe_DropDown.TextColor3 = Color3.fromRGB(90,110,130)
        TextLabe_DropDown.TextSize = 13
        TextLabe_DropDown.TextWrapped = true
        TextLabe_DropDown.TextXAlignment = Enum.TextXAlignment.Left
        TextLabe_DropDown.Text = tostring(text).." :"

		function getpro()
			if default then
				if table.find(option, default) then
					pcall(callback, default)
					return tostring(text).." : " .. default
				else
					return text
				end
			else
				return text
			end
		end
		TextLabe_DropDown.Text = getpro()

        local Icon = Instance.new("ImageLabel")
		Icon.Name = "Icon"
		Icon.Parent = TextLabe_DropDown
		Icon.BackgroundColor3 = Color3.fromRGB(25, 35, 60)
		Icon.BackgroundTransparency = 1
		Icon.AnchorPoint = Vector2.new(0.5,0.5)
		Icon.Position = UDim2.new(0.915, 0, 0.5, 0)
		Icon.Rotation = 0
		Icon.Size = UDim2.new(0, 20, 0, 20)
		Icon.Image = "http://www.roblox.com/asset/?id=11318419925"
		Icon.ImageColor3 = Color3.fromRGB(90,110,130)

        local Dropdown_Button = Instance.new("TextButton")
        Dropdown_Button.Name = "DropFrame"
        Dropdown_Button.Parent = DropDown_Frame
        Dropdown_Button.BackgroundColor3 = Color3.fromRGB(20,20,20)
        Dropdown_Button.BackgroundTransparency = 1
        Dropdown_Button.BorderSizePixel = 0
        Dropdown_Button.AnchorPoint = Vector2.new(0.5, 0.5)
        Dropdown_Button.Position = UDim2.new(0.5, 0, 0.5, 0)
        Dropdown_Button.Size = UDim2.new(0, 225, 0, 35)
        Dropdown_Button.Text = ""
        Dropdown_Button.AutoButtonColor = false
        Dropdown_Button.ClipsDescendants = true

		local Scrolling_Dropdown = Instance.new("ScrollingFrame")
		Scrolling_Dropdown.Name = "Scrolling_Drop"
		Scrolling_Dropdown.Parent = DropDown_Frame
		Scrolling_Dropdown.Active = true
		Scrolling_Dropdown.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		Scrolling_Dropdown.BackgroundTransparency = 1
		Scrolling_Dropdown.BorderSizePixel = 0
		Scrolling_Dropdown.AnchorPoint = Vector2.new(0.5,0.5)
		Scrolling_Dropdown.Position = UDim2.new(0.4715, 0, 3.125, 0)
		Scrolling_Dropdown.Size = UDim2.new(0, 210, 0, 125)
        Scrolling_Dropdown.BottomImage = "rbxasset://textures/ui/Scroll/scroll-middle.png"
        Scrolling_Dropdown.CanvasSize = UDim2.new(0, 0, 0, 0)
        Scrolling_Dropdown.ScrollBarThickness = 4
        Scrolling_Dropdown.TopImage = "rbxasset://textures/ui/Scroll/scroll-middle.png"
        Scrolling_Dropdown.ScrollBarImageColor3 = Color3.fromRGB(90, 110, 130)
		Scrolling_Dropdown.ScrollBarImageTransparency = 0

		local UIListLayout = Instance.new("UIListLayout")
		UIListLayout.Name = "UIListLayout"
		UIListLayout.Parent = Scrolling_Dropdown
		UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
		UIListLayout.Padding = UDim.new(0, 4)

		local UIPaddinglist = Instance.new("UIPadding")
		UIPaddinglist.Name = "UIPaddinglist"
		UIPaddinglist.Parent = Scrolling_Dropdown
		UIPaddinglist.PaddingTop = UDim.new(0, 7)
        UIPaddinglist.PaddingLeft = UDim.new(0, 0)

        local Dropdown = false
        Dropdown_Tween = true
		local FrameSize = 145
		local cout = 0
		for i , v in pairs(option) do
			cout =cout + 1
			if cout == 1 then
				FrameSize = 145
			elseif cout == 2 then
				FrameSize = 145
			elseif cout >= 3 then
				FrameSize = 145
			end

		local Button_Frame = Instance.new("Frame")
		Button_Frame.Name = "ListFrame"
		Button_Frame.Parent = Scrolling_Dropdown
		Button_Frame.BackgroundColor3 = Color3.fromRGB(15,15,15)
		Button_Frame.BackgroundTransparency = 1
		Button_Frame.BorderSizePixel = 0
		Button_Frame.AnchorPoint = Vector2.new(0.5, 0.5)
		Button_Frame.Position = UDim2.new(0.5, 0, 0.5, 0)
		Button_Frame.Size = UDim2.new(0, 210, 0, 30)
            
		local Button_DropDown = Instance.new("TextButton")
		Button_DropDown.Name = "Dropdwon_Button"
		Button_DropDown.Parent = Button_Frame
		Button_DropDown.AnchorPoint = Vector2.new(0.5, 0.5)
		Button_DropDown.BackgroundColor3 = Color3.fromRGB(200,210,220)
		Button_DropDown.BackgroundTransparency = 0
		Button_DropDown.BorderSizePixel = 0
		Button_DropDown.Position = UDim2.new(0.5, 0, 0.5, 0)
		Button_DropDown.Size = UDim2.new(0, 190, 0, 25)
		Button_DropDown.Font = Enum.Font.GothamSemibold
		Button_DropDown.TextColor3 = Color3.fromRGB(90, 110, 130)
		Button_DropDown.TextSize = 13
		Button_DropDown.TextXAlignment = Enum.TextXAlignment.Left
		Button_DropDown.Text = ""
        Button_DropDown.AutoButtonColor  = false

		local UICorner = Instance.new("UICorner")
		UICorner.CornerRadius = UDim.new(0, 5)
		UICorner.Name = ""
		UICorner.Parent = Button_DropDown

		local TextLabel_Button = Instance.new("TextLabel")
		TextLabel_Button.Name = "TextLabel_TapDro2p"
		TextLabel_Button.Parent = Button_DropDown
		TextLabel_Button.AnchorPoint = Vector2.new(0.5, 0.5)
		TextLabel_Button.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		TextLabel_Button.BackgroundTransparency = 1
		TextLabel_Button.Position = UDim2.new(0.5, 0, 0.5, 0)
		TextLabel_Button.Size = UDim2.new(0, 190, 0, 30)
		TextLabel_Button.Font = Enum.Font.GothamSemibold
		TextLabel_Button.TextColor3 = Color3.fromRGB(90,110,130)
		TextLabel_Button.TextSize = 14
		TextLabel_Button.TextXAlignment = Enum.TextXAlignment.Center
		TextLabel_Button.Text = tostring(v)

		local Line_Frame = Instance.new("Frame")
		Line_Frame.Name = "ListFrame"
		Line_Frame.Parent = Button_DropDown
		Line_Frame.BackgroundColor3 = Color3.fromRGB(170,180,190)
		Line_Frame.BackgroundTransparency = 0
		Line_Frame.BorderSizePixel = 0
		Line_Frame.AnchorPoint = Vector2.new(0.5, 0.5)
		Line_Frame.Position = UDim2.new(0.915, 0, 0.5, 0)
		Line_Frame.Size = UDim2.new(0, 16, 0, 16)

		local UICorner = Instance.new("UICorner")
		UICorner.CornerRadius = UDim.new(0, 100)
		UICorner.Name = ""
		UICorner.Parent = Line_Frame

		if tablefound(defaultt,v) then 
			TextLabel_Button.TextColor3 = Color3.fromRGB(90,110,130)
			Line_Frame.BackgroundColor3 = Color3.fromRGB(90,110,130)
			Line_Frame.BackgroundTransparency = 0
			table.insert(MultiDropdownTable,v)
			TextLabe_DropDown.Text =  text.." : "..tostring(table.concat(MultiDropdownTable,","))
		end
        
		Button_DropDown.MouseButton1Click:Connect(function()
			if tablefound(MultiDropdownTable,v) == false then 
				table.insert(MultiDropdownTable,v)
                TextLabel_Button.TextColor3 = Color3.fromRGB(90,110,130)
                Line_Frame.BackgroundColor3 = Color3.fromRGB(90,110,130)
				Line_Frame.BackgroundTransparency = 0
			else 
				for ine,va in pairs(MultiDropdownTable) do
					if va == v then
						table.remove(MultiDropdownTable,ine)
					end
				end
                TextLabel_Button.TextColor3 = Color3.fromRGB(90,110,130)
                Line_Frame.BackgroundColor3 = Color3.fromRGB(170,180,190)
				Line_Frame.BackgroundTransparency = 0
			end  
				TextLabe_DropDown.Text =  text.." : "..tostring(table.concat(MultiDropdownTable,","))
				callback(tostring(table.concat(MultiDropdownTable,",")))
				droptween = false
			end)
			Scrolling_Dropdown.CanvasSize = UDim2.new(0,0,0,UIListLayout.AbsoluteContentSize.Y + 25 )
		end

        Dropdown_Button.MouseButton1Click:Connect(function()
			if Dropdown == false then
				TweenService:Create(
					DropDown_Main,
					TweenInfo.new(0.3, Enum.EasingStyle.Linear, Enum.EasingDirection.Out),
					{Size = UDim2.new(0, 225, 0, FrameSize)}
				):Play()
				TweenService:Create(
					Icon,
					TweenInfo.new(0.3, Enum.EasingStyle.Linear, Enum.EasingDirection.Out),
					{Rotation = 90}
				):Play()
			    Scrolling_Dropdown.CanvasSize = UDim2.new(0,0,0,UIListLayout.AbsoluteContentSize.Y + 25 )
			else
				TweenService:Create(
					DropDown_Main,
					TweenInfo.new(0.3, Enum.EasingStyle.Linear, Enum.EasingDirection.Out),
					{Size = UDim2.new(0, 225, 0, 30)}
				):Play()
				TweenService:Create(
					Icon,
					TweenInfo.new(0.3, Enum.EasingStyle.Linear, Enum.EasingDirection.Out),
					{Rotation = 0}
				):Play()
				Scrolling_Dropdown.CanvasSize = UDim2.new(0,0,0,UIListLayout.AbsoluteContentSize.Y + 25 )
			end
			Dropdown = not Dropdown
            Dropdown_Tween = false
		end)

        Scrolling_Dropdown.CanvasSize = UDim2.new(0,0,0,UIListLayout.AbsoluteContentSize.Y + 25 )
        local dropfunc = {}

		function dropfunc:Clear()
			TextLabe_DropDown.Text = tostring(text).." :"

			TweenService:Create(
				DropDown_Main,
				TweenInfo.new(0.3, Enum.EasingStyle.Linear, Enum.EasingDirection.Out),
				{Size = UDim2.new(0, 225, 0, 30)}
			):Play()
			TweenService:Create(
				Icon,
				TweenInfo.new(0.3, Enum.EasingStyle.Linear, Enum.EasingDirection.Out),
				{Rotation = 0}
			):Play()
			Dropdown = not Dropdown
			Dropdown_Tween = true
            MultiDropdownTable = {}
			for i, v in next, Scrolling_Dropdown:GetChildren() do
				if v:IsA("Frame") then
					v:Destroy()
				end
			end
		end

		function dropfunc:Add(t)
            local Button_Frame = Instance.new("Frame")
            Button_Frame.Name = "ListFrame"
            Button_Frame.Parent = Scrolling_Dropdown
            Button_Frame.BackgroundColor3 = Color3.fromRGB(15,15,15)
            Button_Frame.BackgroundTransparency = 1
            Button_Frame.BorderSizePixel = 0
            Button_Frame.AnchorPoint = Vector2.new(0.5, 0.5)
            Button_Frame.Position = UDim2.new(0.5, 0, 0.5, 0)
            Button_Frame.Size = UDim2.new(0, 210, 0, 30)
                
            local Button_DropDown = Instance.new("TextButton")
            Button_DropDown.Name = "Dropdwon_Button"
            Button_DropDown.Parent = Button_Frame
            Button_DropDown.AnchorPoint = Vector2.new(0.5, 0.5)
            Button_DropDown.BackgroundColor3 = Color3.fromRGB(200,210,220)
            Button_DropDown.BackgroundTransparency = 0
            Button_DropDown.BorderSizePixel = 0
            Button_DropDown.Position = UDim2.new(0.5, 0, 0.5, 0)
            Button_DropDown.Size = UDim2.new(0, 190, 0, 25)
            Button_DropDown.Font = Enum.Font.GothamSemibold
            Button_DropDown.TextColor3 = Color3.fromRGB(90, 110, 130)
            Button_DropDown.TextSize = 13
            Button_DropDown.TextXAlignment = Enum.TextXAlignment.Left
            Button_DropDown.Text = ""
            Button_DropDown.AutoButtonColor  = false
    
            local UICorner = Instance.new("UICorner")
            UICorner.CornerRadius = UDim.new(0, 5)
            UICorner.Name = ""
            UICorner.Parent = Button_DropDown
    
            local TextLabel_Button = Instance.new("TextLabel")
            TextLabel_Button.Name = "TextLabel_TapDro2p"
            TextLabel_Button.Parent = Button_DropDown
            TextLabel_Button.AnchorPoint = Vector2.new(0.5, 0.5)
            TextLabel_Button.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
            TextLabel_Button.BackgroundTransparency = 1
            TextLabel_Button.Position = UDim2.new(0.5, 0, 0.5, 0)
            TextLabel_Button.Size = UDim2.new(0, 190, 0, 30)
            TextLabel_Button.Font = Enum.Font.GothamSemibold
            TextLabel_Button.TextColor3 = Color3.fromRGB(90,110,130)
            TextLabel_Button.TextSize = 14
            TextLabel_Button.TextXAlignment = Enum.TextXAlignment.Center
            TextLabel_Button.Text = tostring(t)
    
            local Line_Frame = Instance.new("Frame")
            Line_Frame.Name = "ListFrame"
            Line_Frame.Parent = Button_DropDown
            Line_Frame.BackgroundColor3 = Color3.fromRGB(170,180,190)
            Line_Frame.BackgroundTransparency = 0
            Line_Frame.BorderSizePixel = 0
            Line_Frame.AnchorPoint = Vector2.new(0.5, 0.5)
            Line_Frame.Position = UDim2.new(0.915, 0, 0.5, 0)
            Line_Frame.Size = UDim2.new(0, 16, 0, 16)
    
            local UICorner = Instance.new("UICorner")
            UICorner.CornerRadius = UDim.new(0, 100)
            UICorner.Name = ""
            UICorner.Parent = Line_Frame    
            
		Button_DropDown.MouseButton1Click:Connect(function()

			if tablefound(MultiDropdownTable,t) == false then 
				table.insert(MultiDropdownTable,t)
                TextLabel_Button.TextColor3 = Color3.fromRGB(90,110,130)
                Line_Frame.BackgroundColor3 = Color3.fromRGB(90,110,130)
				Line_Frame.BackgroundTransparency = 0
			else 
				for ine,va in pairs(MultiDropdownTable) do
					if va == t then
						table.remove(MultiDropdownTable,ine)
					end
				end
                TextLabel_Button.TextColor3 = Color3.fromRGB(90,110,130)
                Line_Frame.BackgroundColor3 = Color3.fromRGB(170,180,190)
				Line_Frame.BackgroundTransparency = 0
			end  
				TextLabe_DropDown.Text =  text.." : "..tostring(table.concat(MultiDropdownTable,","))
				callback(tostring(table.concat(MultiDropdownTable,",")))
				droptween = false
			end)
			Scrolling_Dropdown.CanvasSize = UDim2.new(0,0,0,UIListLayout.AbsoluteContentSize.Y + 25 )
		end
			return dropfunc
		end

	function Items:Slider(text,min,max,de,callback)
		local sliderfunc = {}
		local SliderFrame = Instance.new("Frame")
		SliderFrame.Name = "SliderFrame"
		SliderFrame.Parent = Page
		SliderFrame.AnchorPoint = Vector2.new(0.5, 0.5)
		SliderFrame.BackgroundColor3 = Color3.fromRGB(220, 230, 240)
		SliderFrame.BackgroundTransparency = 0
		SliderFrame.ClipsDescendants = true
		SliderFrame.Position = UDim2.new(0.5, 0, 0.45, 0)
		SliderFrame.Size = UDim2.new(0, 225, 0, 45)

		local SliderFrame_UICorner = Instance.new("UICorner")
		SliderFrame_UICorner.Name = "SliderFrame_UICorner"
		SliderFrame_UICorner.Parent = SliderFrame
		SliderFrame_UICorner.CornerRadius = UDim.new(0, 5)

		local LabelNameSlider = Instance.new("TextLabel")
		LabelNameSlider.Name = "LabelNameSlider"
		LabelNameSlider.Parent = SliderFrame
		LabelNameSlider.AnchorPoint = Vector2.new(0.5, 0.5)
		LabelNameSlider.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		LabelNameSlider.BackgroundTransparency = 1
		LabelNameSlider.BorderSizePixel = 0
		LabelNameSlider.Position = UDim2.new(0.5, 0, 0.35, 0)
		LabelNameSlider.Size = UDim2.new(0, 215, 0, 20)
		LabelNameSlider.Font = Enum.Font.GothamBold
		LabelNameSlider.TextColor3 = Color3.fromRGB(90,110,130)
		LabelNameSlider.Text = tostring(text)
		LabelNameSlider.TextSize = 14
		LabelNameSlider.TextWrapped = true
		LabelNameSlider.TextXAlignment = Enum.TextXAlignment.Left

		local ShowValueFrame = Instance.new("Frame")
		ShowValueFrame.Name = "ShowValueFrame"
		ShowValueFrame.Parent = SliderFrame
		ShowValueFrame.AnchorPoint = Vector2.new(0.5, 0.5)
		ShowValueFrame.BackgroundColor3 = Color3.fromRGB(190,200,210)
		ShowValueFrame.BorderSizePixel = 0
		ShowValueFrame.Position = UDim2.new(0.8615, 0, 0.35, 0)
		ShowValueFrame.Size = UDim2.new(0, 50, 0, 18)

		local ShowValueFrameUICorner = Instance.new("UICorner")
		ShowValueFrameUICorner.CornerRadius = UDim.new(0, 4)
		ShowValueFrameUICorner.Name = "ShowValueFrameUICorner"
		ShowValueFrameUICorner.Parent = ShowValueFrame

		local CustomValue = Instance.new("TextBox")
		CustomValue.Name = "CustomValue"
		CustomValue.Parent = ShowValueFrame
		CustomValue.AnchorPoint = Vector2.new(0.5, 0.5)
		CustomValue.BackgroundColor3 = Color3.fromRGB(10,10,10)
		CustomValue.BackgroundTransparency = 1
		CustomValue.ClipsDescendants = true
		CustomValue.Position = UDim2.new(0.5, 0, 0.5, 0)
		CustomValue.Size = UDim2.new(0, 50, 0, 18)
		CustomValue.Font = Enum.Font.GothamMedium
		CustomValue.PlaceholderColor3 = Color3.fromRGB(90,110,130)
		CustomValue.TextSize = 12
		CustomValue.TextColor3 = Color3.fromRGB(90,110,130)
		CustomValue.Text =  tostring(de and math.floor((de / max) * (max - min) + min) or 0)

		local ValueFrame = Instance.new("Frame")
		ValueFrame.Name = "ValueFrame"
		ValueFrame.Parent = SliderFrame
		ValueFrame.AnchorPoint = Vector2.new(0.5, 0.5)
		ValueFrame.BackgroundColor3 = Color3.fromRGB(190,200,210)
		ValueFrame.BorderSizePixel = 0
		ValueFrame.Position = UDim2.new(0.5, 0, 0.8, 0)
		ValueFrame.Size = UDim2.new(0, 215, 0, 5)

		local Main_UiStroke = Instance.new("UIStroke")
		Main_UiStroke.Thickness = 1
		Main_UiStroke.Name = ""
		Main_UiStroke.Parent = ValueFrame
		Main_UiStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
		Main_UiStroke.LineJoinMode = Enum.LineJoinMode.Round
		Main_UiStroke.Color = Color3.fromRGB(190,200,210)
		Main_UiStroke.Transparency = 0

		local ValueFrameUICorner = Instance.new("UICorner")
		ValueFrameUICorner.CornerRadius = UDim.new(0, 10)
		ValueFrameUICorner.Name = "ShowValueFrameUICorner"
		ValueFrameUICorner.Parent = ValueFrame

		local PartValue = Instance.new("Frame")
		PartValue.Name = "PartValue"
		PartValue.Parent = ValueFrame
		PartValue.Active = true
		PartValue.AnchorPoint = Vector2.new(0.5, 0.5)
		PartValue.BackgroundColor3 = Color3.fromRGB(10,10,10)
		PartValue.BackgroundTransparency = 1.000
		PartValue.Position = UDim2.new(0.498982757, 0, 0.300000012, 0)
		PartValue.Size = UDim2.new(0, 215, 0, 5)

		local MainValue = Instance.new("Frame")
		MainValue.Name = "MainValue"
		MainValue.Parent = PartValue
		MainValue.BackgroundColor3 = Color3.fromRGB(90,110,130)
		MainValue.Position = UDim2.new(0.00101725257, 0, 0.200000003, 0)
		MainValue.Size = UDim2.new((de or 0) / max, 0, 0, 5)
		MainValue.BorderSizePixel = 0

		local MainValueUICorner = Instance.new("UICorner")
		MainValueUICorner.CornerRadius = UDim.new(0, 10)
		MainValueUICorner.Name = "a"
		MainValueUICorner.Parent = MainValue

		local ConneValue = Instance.new("Frame")
		ConneValue.Name = "ConneValue"
		ConneValue.Parent = PartValue
		ConneValue.AnchorPoint = Vector2.new(0.5, 0.5)
		ConneValue.BackgroundColor3 = Color3.fromRGB(10,10,10)
		ConneValue.Position = UDim2.new((de or 0)/max, 0.5, 0.6,0, 0)
		ConneValue.Size = UDim2.new(0, 0, 0, 0)
		ConneValue.BorderSizePixel = 0

		local UICorner = Instance.new("UICorner")
		UICorner.CornerRadius = UDim.new(0, 300)
		UICorner.Parent = ConneValue

		local function move(input)
			local pos =
				UDim2.new(
					math.clamp((input.Position.X - ValueFrame.AbsolutePosition.X) / ValueFrame.AbsoluteSize.X, 0, 1),
					0,
					0.6,
					0
				)
			local pos1 =
				UDim2.new(
					math.clamp((input.Position.X - ValueFrame.AbsolutePosition.X) / ValueFrame.AbsoluteSize.X, 0, 1),
					0,
					0,
					5
				)
			MainValue:TweenSize(pos1, "Out", "Sine", 0.2, true)
			ConneValue:TweenPosition(pos, "Out", "Sine", 0.2, true)
			local value = math.floor(((pos.X.Scale * max) / max) * (max - min) + min)
			CustomValue.Text = tostring(value)
			callback(value)
		end
		local dragging = false
		ConneValue.InputBegan:Connect(
			function(input)
				if input.UserInputType == Enum.UserInputType.MouseButton1 then
					dragging = true
				end
			end)
		ConneValue.InputEnded:Connect(
			function(input)
				if input.UserInputType == Enum.UserInputType.MouseButton1 then
					dragging = false
				end
			end)
		SliderFrame.InputBegan:Connect(
			function(input)
				if input.UserInputType == Enum.UserInputType.MouseButton1 then
					dragging = true
				end
			end)
		SliderFrame.InputEnded:Connect(
			function(input)
				if input.UserInputType == Enum.UserInputType.MouseButton1 then
					dragging = false
				end
			end)
		ValueFrame.InputBegan:Connect(
			function(input)
				if input.UserInputType == Enum.UserInputType.MouseButton1 then
					dragging = true
				end
			end)
		ValueFrame.InputEnded:Connect(
			function(input)
				if input.UserInputType == Enum.UserInputType.MouseButton1 then
					dragging = false
				end
			end)
		game:GetService("UserInputService").InputChanged:Connect(function(input)
			if dragging and input.UserInputType == Enum.UserInputType.MouseMovement then
				move(input)
			end
		end)
		CustomValue.FocusLost:Connect(function()
			if CustomValue.Text == "" then
				CustomValue.Text  = de
			end
			if  tonumber(CustomValue.Text) > max then
				CustomValue.Text  = max
			end
			if  tonumber(CustomValue.Text) < min then
				CustomValue.Text  = min
			end
			MainValue:TweenSize(UDim2.new((CustomValue.Text or 0) / max, 0, 0, 5), "Out", "Sine", 0.2, true)
			ConneValue:TweenPosition(UDim2.new((CustomValue.Text or 0)/max, 0,0.6, 0) , "Out", "Sine", 0.2, true)
			CustomValue.Text = tostring(CustomValue.Text and math.floor( (CustomValue.Text / max) * (max - min) + min) )
			pcall(callback, CustomValue.Text)
		end)
		
		function sliderfunc:Update(value)
			MainValue:TweenSize(UDim2.new((value or 0) / max, 0, 0, 5), "Out", "Sine", 0.2, true)
			CustomValue.Text = value
			pcall(function()
				callback(value)
			end)
		end
			return sliderfunc
		end

----- Return -----
    return Items
end
    return Page
end
    return Tab
end
    return Create
------------------
