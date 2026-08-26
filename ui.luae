-- { Services } --
if not LPH_NO_VIRTUALIZE then LPH_NO_VIRTUALIZE = function(f) return f end end
local playerService = game:GetService("Players")
local runService = game:GetService("RunService")
local tweenService = game:GetService("TweenService")
local httpService = game:GetService("HttpService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local userInputService = game:GetService("UserInputService")
local VirtualInputManager = game:GetService("VirtualInputManager")
local sessionSettings = {
    ["uiaccent"] = {218, 154, 169},
    ["watermark"] = {255,255,255},
    ["watermark2"] = false,
    ["watermarkpos"] = {},
    ["watermarktext"] = "none",
}

local lib = {}
script_key = "trial"
local uiSource = game:HttpGet("https://pastebin.com/raw/ZBBH1Wde")
-- Apply all UI modifications
uiSource = uiSource:gsub("UDim2%.new%(0, (%d+), 0, (%d+)%)", function(w, h)
		w, h = tonumber(w), tonumber(h)
		if w >= 564 and w <= 570 then
			local newW = w == 570 and 740 or w == 568 and 738 or w == 566 and 736 or 734
			local newH = h == 600 and 500 or h == 598 and 498 or h == 596 and 496 or 494
			return string.format("UDim2.new(0, %d, 0, %d)", newW, newH)
		end
		return nil
	end)
	uiSource = uiSource:gsub("[^\n]*uiSearchButton[^\n]*\n", "")
	uiSource = uiSource:gsub("UDim2%.new%(1, 0, 0, 2%)", "UDim2.new(1, 0, 0, 1)")
	uiSource = uiSource:gsub('uiNameLabel%.Position = UDim2%.new%(0%.5, %-125, 0, 0%)', 'uiNameLabel.Position = UDim2.new(0, 10, 0, 5)')
	uiSource = uiSource:gsub('uiNameLabel%.TextSize = 14%.000', 'uiNameLabel.TextSize = 24.000')
	uiSource = uiSource:gsub('uiNameLabel%.Size = UDim2%.new%(0, 250, 1, 0%)', 'uiNameLabel.Size = UDim2.new(1, -20, 1, -4)')
	uiSource = uiSource:gsub('uiNameLabel.TextColor3 = Color3%.fromRGB%(191, 191, 191%)',
		'uiNameLabel.TextColor3 = lib.accent\n\t\t\tuiNameLabel.TextXAlignment = Enum.TextXAlignment.Left\n\t\t\ttable.insert(lib.accentItems, uiNameLabel)')
	uiSource = uiSource:gsub("uiColorOutline2%.Position = UDim2%.new%(1, 23, 0, 0%)", "uiColorOutline2.Position = UDim2.new(0, -193, 0, 0)")
	uiSource = uiSource:gsub('local uiDropdownBack2 = Instance.new%("Frame"%)', 'local uiDropdownBack2 = Instance.new("ScrollingFrame")')
	uiSource = uiSource:gsub('uiDropdownBack2%.ClipsDescendants = true', 'uiDropdownBack2.ClipsDescendants = true\n\t\t\t\tuiDropdownBack2.ScrollBarThickness = 0\n\t\t\t\tuiDropdownBack2.ScrollingDirection = Enum.ScrollingDirection.Y\n\t\t\t\tuiDropdownBack2.ElasticBehavior = Enum.ElasticBehavior.Never')
	uiSource = uiSource:gsub('{Size = UDim2%.new%(1, %-2, 0, size%)}:Play%(\)', '{Size = UDim2.new(1, -2, 0, math.min(size, 170))}):Play()')
	uiSource = uiSource:gsub('\t\t\t\tdropdownLib%.set = function', '\t\t\t\tuiDropdownBack2.CanvasSize = UDim2.new(0, 0, 0, size)\n\t\t\t\tdropdownLib.set = function')
	uiSource = uiSource:gsub("uiTop.Size = UDim2%.new%(1, 0, 0, 25%)", "uiTop.Size = UDim2.new(1, 0, 0, 60)")
	uiSource = uiSource:gsub("table%.insert%(lib%.accentItems, uiTopLine\%)",
		"table.insert(lib.accentItems, uiTopLine)\n" ..
		'\tlocal uiSidebar = Instance.new("Frame")\n' ..
		'\tuiSidebar.Name = "uiSidebar"\n' ..
		'\tuiSidebar.Parent = uiBack\n' ..
		'\tuiSidebar.BackgroundColor3 = Color3.fromRGB(42, 42, 42)\n' ..
		'\tuiSidebar.BorderSizePixel = 0\n' ..
		'\tuiSidebar.Position = UDim2.new(0, 0, 0, 60)\n' ..
		'\tuiSidebar.Size = UDim2.new(0, 180, 1, -(60+50))\n' ..
		'\tlocal uiSidebarMainBtn = Instance.new("TextButton")\n' ..
		'\tuiSidebarMainBtn.Name = "uiSidebarMainBtn"\n' ..
		'\tuiSidebarMainBtn.Parent = uiSidebar\n' ..
		'\tuiSidebarMainBtn.BackgroundColor3 = Color3.fromRGB(255, 255, 255)\n' ..
		'\tuiSidebarMainBtn.BackgroundTransparency = 1.000\n' ..
		'\tuiSidebarMainBtn.BorderSizePixel = 0\n' ..
		'\tuiSidebarMainBtn.Position = UDim2.new(0, 0, 0, 0)\n' ..
		'\tuiSidebarMainBtn.Size = UDim2.new(1, 0, 0, 50)\n' ..
		'\tuiSidebarMainBtn.Text = ""\n' ..
		'\tlocal uiSidebarMainLine = Instance.new("Frame")\n' ..
		'\tuiSidebarMainLine.Name = "uiSidebarMainLine"\n' ..
		'\tuiSidebarMainLine.Parent = uiSidebarMainBtn\n' ..
		'\tuiSidebarMainLine.BackgroundColor3 = lib.accent\n' ..
		'\tuiSidebarMainLine.BorderSizePixel = 0\n' ..
		'\tuiSidebarMainLine.Position = UDim2.new(0, 0, 0, 4)\n' ..
		'\tuiSidebarMainLine.Size = UDim2.new(0, 2, 1, -8)\n' ..
		'\ttable.insert(lib.accentItems, uiSidebarMainLine)\n' ..
		'\tlocal uiSidebarMainGlow = Instance.new("Frame")\n' ..
		'\tuiSidebarMainGlow.Name = "uiSidebarMainGlow"\n' ..
		'\tuiSidebarMainGlow.Parent = uiSidebarMainBtn\n' ..
		'\tuiSidebarMainGlow.BackgroundColor3 = lib.accent\n' ..
		'\tuiSidebarMainGlow.BorderSizePixel = 0\n' ..
		'\tuiSidebarMainGlow.Position = UDim2.new(0, 2, 0, 4)\n' ..
		'\tuiSidebarMainGlow.Size = UDim2.new(0, 25, 1, -8)\n' ..
		'\tlocal glowGradient = Instance.new("UIGradient")\n' ..
		'\tglowGradient.Parent = uiSidebarMainGlow\n' ..
		'\tglowGradient.Transparency = NumberSequence.new({NumberSequenceKeypoint.new(0, 0.65), NumberSequenceKeypoint.new(1, 1)})\n' ..
		'\ttable.insert(lib.accentItems, uiSidebarMainGlow)\n' ..
		'\tlocal uiSidebarMainTitle = Instance.new("TextLabel")\n' ..
		'\tuiSidebarMainTitle.Name = "uiSidebarMainTitle"\n' ..
		'\tuiSidebarMainTitle.Parent = uiSidebarMainBtn\n' ..
		'\tuiSidebarMainTitle.BackgroundColor3 = Color3.fromRGB(255, 255, 255)\n' ..
		'\tuiSidebarMainTitle.BackgroundTransparency = 1.000\n' ..
		'\tuiSidebarMainTitle.Position = UDim2.new(0, 12, 0, 6)\n' ..
		'\tuiSidebarMainTitle.Size = UDim2.new(1, -18, 0, 20)\n' ..
		'\tuiSidebarMainTitle.Font = Enum.Font.ArialBold\n' ..
		'\tuiSidebarMainTitle.Text = "Main"\n' ..
		'\tuiSidebarMainTitle.TextColor3 = Color3.fromRGB(255, 255, 255)\n' ..
		'\tuiSidebarMainTitle.TextSize = 16.000\n' ..
		'\tuiSidebarMainTitle.TextXAlignment = Enum.TextXAlignment.Left\n' ..
		'\tlocal uiSidebarMainSub = Instance.new("TextLabel")\n' ..
		'\tuiSidebarMainSub.Name = "uiSidebarMainSub"\n' ..
		'\tuiSidebarMainSub.Parent = uiSidebarMainBtn\n' ..
		'\tuiSidebarMainSub.BackgroundColor3 = Color3.fromRGB(255, 255, 255)\n' ..
		'\tuiSidebarMainSub.BackgroundTransparency = 1.000\n' ..
		'\tuiSidebarMainSub.Position = UDim2.new(0, 12, 0, 26)\n' ..
		'\tuiSidebarMainSub.Size = UDim2.new(1, -18, 0, 16)\n' ..
		'\tuiSidebarMainSub.Font = Enum.Font.Arial\n' ..
		'\tuiSidebarMainSub.Text = "template"\n' ..
		'\tuiSidebarMainSub.TextColor3 = lib.accent\n' ..
		'\tuiSidebarMainSub.TextSize = 12.000\n' ..
		'\tuiSidebarMainSub.TextXAlignment = Enum.TextXAlignment.Left\n' ..
		'\ttable.insert(lib.accentItems, uiSidebarMainSub)\n' ..
		'\tuiSidebarMainBtn.MouseButton1Click:Connect(function()\n' ..
		'\t\tfor i,tab in pairs(lib.tabframes) do\n' ..
		'\t\t\ttab.Visible = (i == 1)\n' ..
		'\t\tend\n' ..
		'\t\tfor i,btn in pairs(lib.tabbuttons) do\n' ..
		'\t\t\tlocal line = btn:FindFirstChild("uiTabButtonLine")\n' ..
		'\t\t\tif line then\n' ..
		'\t\t\t\tline.BackgroundTransparency = (i == 1) and 0 or 1\n' ..
		'\t\t\tend\n' ..
		'\t\tend\n' ..
		'\tend)\n')		
	uiSource = uiSource:gsub('uiTab.Position = UDim2%.new%(0, 7, 0, 33%)', 'uiTab.Position = UDim2.new(0, 185, 0, 60)')
	uiSource = uiSource:gsub('uiTab.Size = UDim2%.new%(1, %-13, 1, %-93%)', 'uiTab.Size = UDim2.new(1, -(185+6), 1, -(60+56))')
	uiSource = uiSource:gsub("uiBottom.Size = UDim2%.new%(1, 0, 0, 50%)",
		"uiBottom.Size = UDim2.new(1, 0, 0, 50)\n\t\tuiBottom.ZIndex = 10")
	uiSource = uiSource:gsub("uiTabSectionLabel.TextXAlignment = Enum.TextXAlignment.Left\n\n\t\t\tuiTabSectionHolder",
		"uiTabSectionLabel.TextXAlignment = Enum.TextXAlignment.Left\n\n" ..
		'\t\t\tlocal uiSectionLine = Instance.new("Frame")\n' ..
		'\t\t\tuiSectionLine.Name = "uiSectionLine"\n' ..
		'\t\t\tuiSectionLine.Parent = uiTabSectionIn\n' ..
		'\t\t\tuiSectionLine.BackgroundColor3 = lib.accent\n' ..
		'\t\t\tuiSectionLine.BorderSizePixel = 0\n' ..
		'\t\t\tuiSectionLine.Position = UDim2.new(0, 6, 0, 23)\n' ..
		'\t\t\tuiSectionLine.Size = UDim2.new(1, -12, 0, 1)\n' ..
		'\t\t\ttable.insert(lib.accentItems, uiSectionLine)\n\n' ..
		'\t\t\tuiTabSectionHolder')
	uiSource = uiSource:gsub("uiSectionColorpicker%.Size = UDim2%.new%(1, 0, 0, 20%)",
		"uiSectionColorpicker.Size = UDim2.new(1, 0, 0, 14)")
	uiSource = uiSource:gsub("if xl == 0 then\n\t\t\t\t\tuiTabSection%.Position = UDim2%.new%(1, %-270, 0, xl%)\n\t\t\t\telse\n\t\t\t\t\tuiTabSection%.Position = UDim2%.new%(1, %-270, 0, xl %+ 5%)\n\t\t\t\tend",
		"uiTabSection.Position = UDim2.new(1, -270, 0, xl + 5)")
	uiSource = uiSource:gsub("if xr == 0 then\n\t\t\t\t\t\tuiTabSection%.Position = UDim2%.new%(0, 0, 0, xr%)\n\t\t\t\t\telse\n\t\t\t\t\t\tuiTabSection%.Position = UDim2%.new%(0, 0, 0, xr %+ 5%)\n\t\t\t\t\tend",
		"uiTabSection.Position = UDim2.new(0, 0, 0, xr + 5)")
	uiSource = uiSource:gsub("uiTabSection%.Size = UDim2%.new%(0, 270, 0, 30%)", "uiTabSection.Size = UDim2.new(0, 270, 0, 30)")
	uiSource = uiSource:gsub("uiTabSection%.Size = UDim2%.new%(uiTabSection%.Size%.X%.Scale, uiTabSection%.Size%.X%.Offset, uiTabSection%.Size%.Y%.Scale, uiTabSection%.Size%.Y%.Offset %+% 36%)", "uiTabSection.Size = UDim2.new(uiTabSection.Size.X.Scale, uiTabSection.Size.X.Offset, uiTabSection.Size.Y.Scale, uiTabSection.Size.Y.Offset + 28)")
	uiSource = uiSource:gsub("end; uiTabSection%.Size = UDim2%.new%(uiTabSection%.Size%.X%.Scale, uiTabSection%.Size%.X%.Offset, uiTabSection%.Size%.Y%.Scale, uiTabSection%.Size%.Y%.Offset %+% 36%)", "end; uiTabSection.Size = UDim2.new(uiTabSection.Size.X.Scale, uiTabSection.Size.X.Offset, uiTabSection.Size.Y.Scale, uiTabSection.Size.Y.Offset + 28)")
	uiSource = uiSource:gsub('uiSectionSlider%.Size = UDim2%.new%(1, 0, 0, 36%)', 'uiSectionSlider.Size = UDim2.new(1, 0, 0, 28)')
	uiSource = uiSource:gsub('uiSliderOutline%.Position = UDim2%.new%(0, 7, 0, 19%)', 'uiSliderOutline.Position = UDim2.new(0, 7, 0, 16)')
	uiSource = uiSource:gsub('uiSliderOutline%.Size = UDim2%.new%(1, %-10, 0, 12%)', 'uiSliderOutline.Size = UDim2.new(1, -10, 0, 8)')
	uiSource = uiSource:gsub('uiTab.ScrollBarThickness = 4', 'uiTab.ScrollBarThickness = 0\n\t\tuiTab.ScrollingEnabled = true\n\t\tuiTab.ClipsDescendants = true')
	uiSource = uiSource:gsub('local size = 0\n\t\t\tlocal closing = false', 'local size = 0\n\t\t\t_G.__cfgDropSizes = _G.__cfgDropSizes or {}\n\t\t\t_G.__cfgDropSizes[flag] = 0\n\t\t\tlocal closing = false')
	uiSource = uiSource:gsub('Size = UDim2%.new%(1, %-2, 0, size%)', 'Size = UDim2.new(1, -2, 0, _G.__cfgDropSizes and _G.__cfgDropSizes[flag] or size)')
	uiSource = uiSource:gsub('local closing = false\n\t\t\tlocal open = false', '_G.__cfgDropClosing = false\n\t\t\t_G.__cfgDropOpen = false')
	uiSource = uiSource:gsub('open = not open', '_G.__cfgDropOpen = not _G.__cfgDropOpen')
	uiSource = uiSource:gsub('\t\t\t\t\tclosing = true', '\t\t\t\t\t_G.__cfgDropClosing = true')
	uiSource = uiSource:gsub('\t\t\t\t\tclosing = false', '\t\t\t\t\t_G.__cfgDropClosing = false')
	uiSource = uiSource:gsub('if open and lib%.inDropdown then', 'if _G.__cfgDropOpen and lib.inDropdown then')
	uiSource = uiSource:gsub('if not closing then', 'if not _G.__cfgDropClosing then')
	uiSource = uiSource:gsub('if open then', 'if _G.__cfgDropOpen then')
	uiSource = uiSource:gsub('if not open then', 'if not _G.__cfgDropOpen then')
	uiSource = uiSource:gsub('elseif not open and not lib%.inDropdown then', 'elseif not _G.__cfgDropOpen and not lib.inDropdown then')
	uiSource = uiSource:gsub('return togglelib', '_G.__uiRefs = _G.__uiRefs or {}; _G.__uiRefs[flag] = togglelib\n\t\t\t\treturn togglelib')
	uiSource = uiSource:gsub('return slider', '_G.__uiRefs = _G.__uiRefs or {}; _G.__uiRefs[flag] = slider\n\t\t\t\treturn slider')
	uiSource = uiSource:gsub('return colorpickerlib', '_G.__uiRefs = _G.__uiRefs or {}; _G.__uiRefs[flag] = colorpickerlib\n\t\t\t\treturn colorpickerlib')
	uiSource = uiSource:gsub('return dropdownLib', '_G.__uiRefs = _G.__uiRefs or {}; _G.__uiRefs[flag] = dropdownLib\n\t\t\t\treturn dropdownLib')
	uiSource = uiSource:gsub('uiSectionButton%.Size = UDim2%.new%(1, 0, 0, 27%)',
		'uiSectionButton.Size = UDim2.new(1, 0, 0, 20)\n\t\t\t\tlocal uiCorner = Instance.new("UICorner",uiButtonBack); uiCorner.CornerRadius = UDim.new(0,4)\n\t\t\t\t_G.__btnStates = _G.__btnStates or {}; _G.__btnStates[#_G.__btnStates+1] = {back = uiButtonBack, label = uiButtonLabel}')
	uiSource = uiSource:gsub('uiTabButton.ZIndex = 2', 'uiTabButton.ZIndex = 11')
	uiSource = uiSource:gsub('uiTabButtonLabel.ZIndex = 2', 'uiTabButtonLabel.ZIndex = 11')
	uiSource = uiSource:gsub('uiTabButtonLine.ZIndex = 2', 'uiTabButtonLine.ZIndex = 11')
	uiSource = uiSource:gsub('uiTabButtonImage.ZIndex = 2', 'uiTabButtonImage.ZIndex = 11')
	uiSource = uiSource:gsub('uiTabButtonLabel.ZIndex = 3', 'uiTabButtonLabel.ZIndex = 12')
	uiSource = uiSource:gsub('uiColorOutline%.Size = UDim2%.new%(0, 22, 0, 14%)', 'uiColorOutline.Size = UDim2.new(0, 20, 0, 12)')
	uiSource = uiSource:gsub('uiColorOutline%.Position = UDim2%.new%(1, %-25, 0%.5, %-7%)', 'uiColorOutline.Position = UDim2.new(1, -23, 0.5, -6)')
	uiSource = uiSource:gsub('uiColorButton%.Size = UDim2%.new%(0, 20, 0, 12%)', 'uiColorButton.Size = UDim2.new(0, 18, 0, 10)')
	uiSource = uiSource:gsub('Instance.new%("UICorner",uiColorOutline%); uiCorner%.CornerRadius = UDim%.new%(0,3%)', 'Instance.new("UICorner",uiColorOutline); uiCorner.CornerRadius = UDim.new(0,6)')
	uiSource = uiSource:gsub('Instance.new%("UICorner",uiColorButton%); uiCorner%.CornerRadius = UDim%.new%(0,3%)', 'Instance.new("UICorner",uiColorButton); uiCorner.CornerRadius = UDim.new(0,5)')
_G.__cfgDropOpen = false
_G.__cfgDropClosing = false
-- Ensure the UI returns the lib table
if not uiSource:match("return%s+lib") and not uiSource:match("return%s+{") then
	uiSource = uiSource .. "\nreturn lib"
end
lib = loadstring(uiSource)()
local loadConfig;
local saveConfig; local fps;

-- { Client } --

local client = {}
client.player = playerService.LocalPlayer
client.getCharacter = function()
	return client.player.Character or client.player.CharacterAdded:Wait()
end

-- { Variables } --

local players = playerService

local watermarkui = Instance.new("ScreenGui")
local watermarkback = Instance.new("Frame")
local watermarkback2 = Instance.new("Frame")
local watermarkLabel = Instance.new("TextLabel")
local watermarkLine = Instance.new("ImageLabel")

watermarkui.Name = " "
watermarkui.Parent = game.CoreGui
watermarkui.ResetOnSpawn = false
watermarkui.Enabled = false

watermarkback.Name = "watermarkback"
watermarkback.Parent = watermarkui
watermarkback.BackgroundColor3 = Color3.fromRGB(27, 22, 20)
watermarkback.BorderSizePixel = 0
watermarkback.Size = UDim2.new(0, 190, 0, 28)
watermarkback.BackgroundTransparency = 1
Instance.new("UICorner", watermarkback).CornerRadius = UDim.new(0, 6)
watermarkback.Position = UDim2.new(1, -245, 0, -28)

watermarkback2.Name = "watermarkback2"
watermarkback2.Parent = watermarkback
watermarkback2.BackgroundColor3 = Color3.fromRGB(43, 43, 43)
watermarkback2.BorderSizePixel = 0
watermarkback2.Position = UDim2.new(0, 1, 0, 1)
watermarkback2.Size = UDim2.new(1, -2, 1, -2)
watermarkback2.BackgroundTransparency = 1
Instance.new("UICorner", watermarkback2).CornerRadius = UDim.new(0, 6)

watermarkLabel.Name = "watermarkLabel"
watermarkLabel.Parent = watermarkback2
watermarkLabel.BackgroundTransparency = 1
watermarkLabel.Position = UDim2.new(0, 0, 0, 2)
watermarkLabel.Size = UDim2.new(1, 0, 0, 20)
watermarkLabel.Font = Enum.Font.Arial
watermarkLabel.Text = ""
watermarkLabel.TextColor3 = Color3.fromRGB(218, 218, 218)
watermarkLabel.TextSize = 14
watermarkLabel.TextStrokeColor3 = Color3.fromRGB(14, 14, 14)
watermarkLabel.TextStrokeTransparency = 0.22

watermarkLine.Name = "watermarkLine"
watermarkLine.Parent = watermarkLabel
watermarkLine.BackgroundTransparency = 1
watermarkLine.BorderSizePixel = 0
watermarkLine.Position = UDim2.new(0.5, -64, 1, 0)
watermarkLine.Size = UDim2.new(0, 128, 0, 2)
watermarkLine.Image = "http://www.roblox.com/asset/?id=8753817226"
watermarkLine.ImageColor3 = Color3.fromRGB(218, 154, 169)

local dragging2, dragInput2, dragStart2, startPos2
local function update2(input)
	local delta = input.Position - dragStart2
	watermarkback.Position = UDim2.new(startPos2.X.Scale, startPos2.X.Offset + delta.X, startPos2.Y.Scale, startPos2.Y.Offset + delta.Y)
end
watermarkback.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
		dragging2 = true; dragStart2 = input.Position; startPos2 = watermarkback.Position
		input.Changed:Connect(function()
			if input.UserInputState == Enum.UserInputState.End then dragging2 = false end
		end)
	end
end)
watermarkback.InputChanged:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then dragInput2 = input end
end)
userInputService.InputChanged:Connect(function(input)
	if input == dragInput2 and dragging2 then update2(input) end
end)

local resizeR = Instance.new("Frame")
resizeR.Name = "resizeR"
resizeR.Parent = watermarkback
resizeR.BackgroundColor3 = Color3.fromRGB(255,255,255)
resizeR.BackgroundTransparency = 1
resizeR.Position = UDim2.new(1, -5, 0, 0)
resizeR.Size = UDim2.new(0, 5, 1, 0)
resizeR.ZIndex = 5
local resizeB = Instance.new("Frame")
resizeB.Name = "resizeB"
resizeB.Parent = watermarkback
resizeB.BackgroundColor3 = Color3.fromRGB(255,255,255)
resizeB.BackgroundTransparency = 1
resizeB.Position = UDim2.new(0, 0, 1, -5)
resizeB.Size = UDim2.new(1, 0, 0, 5)
resizeB.ZIndex = 5
local draggingR, dragStartR, startSizeR
local draggingB, dragStartB, startSizeB
resizeR.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 then
		draggingR = true; dragStartR = input.Position; startSizeR = watermarkback.Size
		input.Changed:Connect(function() if input.UserInputState == Enum.UserInputState.End then draggingR = false end end)
	end
end)
resizeB.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 then
		draggingB = true; dragStartB = input.Position; startSizeB = watermarkback.Size
		input.Changed:Connect(function() if input.UserInputState == Enum.UserInputState.End then draggingB = false end end)
	end
end)
userInputService.InputChanged:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseMovement then
		if draggingR and dragStartR then
			watermarkback.Size = UDim2.new(0, math.max(100, startSizeR.X.Offset + (input.Position - dragStartR).X), 0, startSizeR.Y.Offset)
		end
		if draggingB and dragStartB then
			watermarkback.Size = UDim2.new(0, startSizeB.X.Offset, 0, math.max(20, startSizeB.Y.Offset + (input.Position - dragStartB).Y))
		end
	end
end)

local kblistGui = Instance.new("ScreenGui")
kblistGui.Name = " "
kblistGui.Parent = game.CoreGui
kblistGui.ResetOnSpawn = false
kblistGui.Enabled = false

local kblistBack = Instance.new("Frame")
kblistBack.Name = "kblistBack"
kblistBack.Parent = kblistGui
kblistBack.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
kblistBack.BorderSizePixel = 0
kblistBack.Size = UDim2.new(0, 170, 0, 30)
kblistBack.Position = UDim2.new(0, 20, 0, 200)
Instance.new("UICorner", kblistBack).CornerRadius = UDim.new(0, 6)
local kblistStroke = Instance.new("UIStroke")
kblistStroke.Parent = kblistBack
kblistStroke.Color = Color3.fromRGB(15, 15, 15)
kblistStroke.Thickness = 1
_G.kblistStroke = kblistStroke
_G.kblistBack = kblistBack

local kblistTitle = Instance.new("TextLabel")
kblistTitle.Name = "kblistTitle"
kblistTitle.Parent = kblistBack
kblistTitle.BackgroundTransparency = 1
kblistTitle.Position = UDim2.new(0, 8, 0, 4)
kblistTitle.Size = UDim2.new(1, -16, 0, 18)
kblistTitle.Font = Enum.Font.Arial
kblistTitle.Text = "keybinds"
kblistTitle.TextColor3 = Color3.fromRGB(208, 208, 208)
kblistTitle.TextSize = 10
kblistTitle.TextStrokeTransparency = 0.5
kblistTitle.TextXAlignment = Enum.TextXAlignment.Left

local kblistLine = Instance.new("Frame")
kblistLine.Name = "kblistLine"
kblistLine.Parent = kblistBack
kblistLine.BackgroundColor3 = Color3.fromRGB(218, 154, 169)
kblistLine.BorderSizePixel = 0
kblistLine.Position = UDim2.new(0, 6, 0, 18)
kblistLine.Size = UDim2.new(1, -12, 0, 1)

local kblistHolder = Instance.new("Frame")
kblistHolder.Name = "kblistHolder"
kblistHolder.Parent = kblistBack
kblistHolder.BackgroundTransparency = 1
kblistHolder.Position = UDim2.new(0, 8, 0, 22)
kblistHolder.Size = UDim2.new(1, -16, 1, -26)
local kblistLayout = Instance.new("UIListLayout", kblistHolder)
kblistLayout.SortOrder = Enum.SortOrder.LayoutOrder
kblistLayout.Padding = UDim.new(0, 2)

local function createKbEntry(text)
	local entry = Instance.new("TextLabel")
	entry.Name = "kbEntry"
	entry.Parent = kblistHolder
	entry.BackgroundTransparency = 1
	entry.Size = UDim2.new(1, 0, 0, 14)
	entry.Font = Enum.Font.Arial
	entry.Text = text
	entry.TextColor3 = Color3.fromRGB(182, 182, 182)
	entry.TextSize = 11
	entry.TextStrokeTransparency = 0.35
	entry.TextXAlignment = Enum.TextXAlignment.Left
	return entry
end

local function updateKbList()
	for _, ch in pairs(kblistHolder:GetChildren()) do
		if ch:IsA("TextLabel") then ch:Destroy() end
	end
	local count = 0
	for _, ch in pairs(kblistHolder:GetChildren()) do
		if ch:IsA("TextLabel") then count = count + 1 end
	end
	kblistBack.Size = UDim2.new(0, 170, 0, math.max(30, 30 + count * 16))
end

local dragging3, dragInput3, dragStart3, startPos3
local function update3(input)
	local delta = input.Position - dragStart3
	kblistBack.Position = UDim2.new(startPos3.X.Scale, startPos3.X.Offset + delta.X, startPos3.Y.Scale, startPos3.Y.Offset + delta.Y)
end
kblistBack.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
		dragging3 = true; dragStart3 = input.Position; startPos3 = kblistBack.Position
		input.Changed:Connect(function()
			if input.UserInputState == Enum.UserInputState.End then dragging3 = false end
		end)
	end
end)
kblistBack.InputChanged:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then dragInput3 = input end
end)
userInputService.InputChanged:Connect(function(input)
	if input == dragInput3 and dragging3 then update3(input) end
end)

local radarGui = Instance.new("ScreenGui")
radarGui.Name = " "
radarGui.Parent = game.CoreGui
radarGui.ResetOnSpawn = false
radarGui.Enabled = false
local radarBack = Instance.new("Frame")
radarBack.Name = "radarBack"
radarBack.Parent = radarGui
radarBack.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
radarBack.BorderSizePixel = 0
radarBack.Size = UDim2.new(0, 200, 0, 200)
radarBack.Position = UDim2.new(0, 20, 0, 240)
Instance.new("UICorner", radarBack).CornerRadius = UDim.new(0, 6)
local radarStroke = Instance.new("UIStroke")
radarStroke.Parent = radarBack
radarStroke.Color = Color3.fromRGB(15, 15, 15)
radarStroke.Thickness = 1
local radarTitle = Instance.new("TextLabel")
radarTitle.Parent = radarBack
radarTitle.BackgroundTransparency = 1
radarTitle.Position = UDim2.new(0, 0, 0, 4)
radarTitle.Size = UDim2.new(1, 0, 0, 14)
radarTitle.Font = Enum.Font.Arial
radarTitle.Text = "Radar"
radarTitle.TextColor3 = Color3.fromRGB(208, 208, 208)
radarTitle.TextSize = 10
radarTitle.TextStrokeTransparency = 0.5
local radarLine = Instance.new("Frame")
radarLine.Parent = radarBack
radarLine.BackgroundColor3 = Color3.fromRGB(218, 154, 169)
radarLine.BorderSizePixel = 0
radarLine.Position = UDim2.new(0, 8, 0, 20)
radarLine.Size = UDim2.new(1, -16, 0, 1)
local radarContent = Instance.new("Frame")
radarContent.Name = "radarContent"
radarContent.Parent = radarBack
radarContent.BackgroundTransparency = 1
radarContent.ClipsDescendants = true
radarContent.Position = UDim2.new(0, 4, 0, 24)
radarContent.Size = UDim2.new(1, -8, 1, -28)
Instance.new("UICorner", radarContent).CornerRadius = UDim.new(0, 3)
local gridV = Instance.new("Frame")
gridV.Parent = radarContent
gridV.BackgroundColor3 = Color3.fromRGB(55, 55, 55)
gridV.BorderSizePixel = 0
gridV.AnchorPoint = Vector2.new(0.5, 0)
gridV.Position = UDim2.new(0.5, 0, 0, 0)
gridV.Size = UDim2.new(0, 1, 1, 0)
local gridH = Instance.new("Frame")
gridH.Parent = radarContent
gridH.BackgroundColor3 = Color3.fromRGB(55, 55, 55)
gridH.BorderSizePixel = 0
gridH.AnchorPoint = Vector2.new(0, 0.5)
gridH.Position = UDim2.new(0, 0, 0.5, 0)
gridH.Size = UDim2.new(1, 0, 0, 1)
local radarDots = Instance.new("Frame")
radarDots.Name = "radarDots"
radarDots.Parent = radarContent
radarDots.BackgroundTransparency = 1
radarDots.Size = UDim2.new(1, 0, 1, 0)
local radarRange = 200
local dragging4, dragInput4, dragStart4, startPos4
local function update4(input)
	local delta = input.Position - dragStart4
	radarBack.Position = UDim2.new(startPos4.X.Scale, startPos4.X.Offset + delta.X, startPos4.Y.Scale, startPos4.Y.Offset + delta.Y)
end
radarBack.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
		dragging4 = true; dragStart4 = input.Position; startPos4 = radarBack.Position
		input.Changed:Connect(function() if input.UserInputState == Enum.UserInputState.End then dragging4 = false end end)
	end
end)
radarBack.InputChanged:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then dragInput4 = input end
end)
userInputService.InputChanged:Connect(function(input)
	if input == dragInput4 and dragging4 then update4(input) end
end)
local radarDotPool = {}
local radarDotMax = 50
for i = 1, radarDotMax do
	local dot = Instance.new("Frame")
	dot.Parent = radarDots
	dot.BackgroundColor3 = Color3.fromRGB(218, 154, 169)
	dot.BorderSizePixel = 0
	dot.AnchorPoint = Vector2.new(0.5, 0.5)
	dot.Size = UDim2.new(0, 5, 0, 5)
	dot.Visible = false
	Instance.new("UICorner", dot).CornerRadius = UDim.new(1, 0)
	radarDotPool[i] = dot
end
local myDot = Instance.new("Frame")
myDot.Parent = radarDots
myDot.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
myDot.BorderSizePixel = 0
myDot.AnchorPoint = Vector2.new(0.5, 0.5)
myDot.Position = UDim2.new(0.5, 0, 0.5, 0)
myDot.Size = UDim2.new(0, 5, 0, 5)
myDot.ZIndex = 2
Instance.new("UICorner", myDot).CornerRadius = UDim.new(1, 0)
local updateRadar = LPH_NO_VIRTUALIZE(function()
	pcall(function()
		local char = client.getCharacter()
		if not char then return end
		local root = char:FindFirstChild("HumanoidRootPart")
		if not root then return end
		local myPos = root.Position
		local lookVec = root.CFrame.LookVector
		local myAngle = math.atan2(-lookVec.X, -lookVec.Z)
		local contentSize = radarContent.AbsoluteSize
		local cx = contentSize.X / 2
		local cy = contentSize.Y / 2
		local scale = math.min(cx, cy) / radarRange
		local dotIdx = 1
		for _, plr in pairs(playerService:GetPlayers()) do
			if plr ~= client.player and dotIdx <= radarDotMax then
				local pChar = plr.Character
				if pChar then
					local pRoot = pChar:FindFirstChild("HumanoidRootPart")
					local pHum = pChar:FindFirstChildOfClass("Humanoid")
					if pRoot and pHum and pHum.Health > 0 then
						local diff = pRoot.Position - myPos
						local rx = diff.X * math.cos(myAngle) + diff.Z * math.sin(myAngle)
						local rz = -diff.X * math.sin(myAngle) + diff.Z * math.cos(myAngle)
						if math.abs(rx) <= radarRange and math.abs(rz) <= radarRange then
							local dot = radarDotPool[dotIdx]
							dot.Position = UDim2.new(0, cx + rx * scale, 0, cy + rz * scale)
							dot.BackgroundColor3 = lib.accent or Color3.fromRGB(218, 154, 169)
							dot.Visible = true
							dotIdx = dotIdx + 1
						end
					end
				end
			end
		end
	for i = dotIdx, radarDotMax do
		radarDotPool[i].Visible = false
	end
	end)
end)

local keystrokeGui = Instance.new("ScreenGui")
keystrokeGui.Name = " "
keystrokeGui.Parent = game.CoreGui
keystrokeGui.ResetOnSpawn = false
keystrokeGui.Enabled = false
local ksBack = Instance.new("Frame")
ksBack.Name = "ksBack"
ksBack.Parent = keystrokeGui
ksBack.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
ksBack.BorderSizePixel = 0
ksBack.Size = UDim2.new(0, 120, 0, 90)
ksBack.Position = UDim2.new(0, 20, 0, 460)
Instance.new("UICorner", ksBack).CornerRadius = UDim.new(0, 6)
local ksStroke = Instance.new("UIStroke")
ksStroke.Parent = ksBack
ksStroke.Color = Color3.fromRGB(15, 15, 15)
ksStroke.Thickness = 1
local ksHeader = Instance.new("TextLabel")
ksHeader.Parent = ksBack
ksHeader.BackgroundTransparency = 1
ksHeader.Position = UDim2.new(0, 0, 0, 2)
ksHeader.Size = UDim2.new(1, 0, 0, 14)
ksHeader.Font = Enum.Font.Arial
ksHeader.Text = "keystrokes"
ksHeader.TextColor3 = Color3.fromRGB(208, 208, 208)
ksHeader.TextSize = 10
ksHeader.TextStrokeTransparency = 0.5
local ksLine = Instance.new("Frame")
ksLine.Parent = ksBack
ksLine.BackgroundColor3 = Color3.fromRGB(218, 154, 169)
ksLine.BorderSizePixel = 0
ksLine.Position = UDim2.new(0, 8, 0, 18)
ksLine.Size = UDim2.new(1, -16, 0, 1)
local ksKeySize = 30
local ksGap = 4
local ksStartX = (120 - (ksKeySize * 3 + ksGap * 2)) / 2
local function createKsKey(name, text, posX, posY)
	local key = Instance.new("TextButton")
	key.Name = "ksKey_" .. name
	key.Parent = ksBack
	key.BackgroundColor3 = Color3.fromRGB(55, 55, 55)
	key.BorderSizePixel = 0
	key.Position = UDim2.new(0, posX, 0, posY)
	key.Size = UDim2.new(0, ksKeySize, 0, ksKeySize)
	key.Text = text
	key.Font = Enum.Font.Arial
	key.TextColor3 = Color3.fromRGB(208, 208, 208)
	key.TextSize = 12
	key.TextStrokeTransparency = 0.5
	key.AutoButtonColor = false
	Instance.new("UICorner", key).CornerRadius = UDim.new(0, 3)
	local keyStroke = Instance.new("UIStroke")
	keyStroke.Parent = key
	keyStroke.Color = Color3.fromRGB(25, 25, 25)
	keyStroke.Thickness = 1
	return key
end
local ksKeyW = createKsKey("W", "W", ksStartX + ksKeySize + ksGap, 24)
local ksKeyA = createKsKey("A", "A", ksStartX, 24 + ksKeySize + ksGap)
local ksKeyS = createKsKey("S", "S", ksStartX + ksKeySize + ksGap, 24 + ksKeySize + ksGap)
local ksKeyD = createKsKey("D", "D", ksStartX + (ksKeySize + ksGap) * 2, 24 + ksKeySize + ksGap)
local ksKeyMap = {
	[Enum.KeyCode.W] = ksKeyW,
	[Enum.KeyCode.A] = ksKeyA,
	[Enum.KeyCode.S] = ksKeyS,
	[Enum.KeyCode.D] = ksKeyD,
}
local function setKeyState(keyCode, pressed)
	local key = ksKeyMap[keyCode]
	if not key then return end
	if pressed then
		key.BackgroundColor3 = lib.accent or Color3.fromRGB(218, 154, 169)
		key.TextColor3 = Color3.fromRGB(30, 30, 30)
	else
		key.BackgroundColor3 = Color3.fromRGB(55, 55, 55)
		key.TextColor3 = Color3.fromRGB(208, 208, 208)
	end
end
userInputService.InputBegan:Connect(function(input, gpe)
	if gpe then return end
	if ksKeyMap[input.KeyCode] then setKeyState(input.KeyCode, true) end
end)
userInputService.InputEnded:Connect(function(input)
	if ksKeyMap[input.KeyCode] then setKeyState(input.KeyCode, false) end
end)
local dragging5, dragInput5, dragStart5, startPos5
local function update5(input)
	local delta = input.Position - dragStart5
	ksBack.Position = UDim2.new(startPos5.X.Scale, startPos5.X.Offset + delta.X, startPos5.Y.Scale, startPos5.Y.Offset + delta.Y)
end
ksBack.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
		dragging5 = true; dragStart5 = input.Position; startPos5 = ksBack.Position
		input.Changed:Connect(function() if input.UserInputState == Enum.UserInputState.End then dragging5 = false end end)
	end
end)
ksBack.InputChanged:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then dragInput5 = input end
end)
userInputService.InputChanged:Connect(function(input)
	if input == dragInput5 and dragging5 then update5(input) end
end)

coroutine.wrap(function()
	local TimeFunction = runService:IsRunning() and time or os.clock
	local LastIteration, Start
	local FrameUpdateTable = {}
	local HeartbeatUpdate = LPH_NO_VIRTUALIZE(function()
		LastIteration = TimeFunction()
		for Index = #FrameUpdateTable, 1, -1 do
			FrameUpdateTable[Index + 1] = FrameUpdateTable[Index] >= LastIteration - 1 and FrameUpdateTable[Index] or nil
		end
		FrameUpdateTable[1] = LastIteration
		fps = tostring(math.floor(TimeFunction() - Start >= 1 and #FrameUpdateTable or #FrameUpdateTable / (TimeFunction() - Start)))
	end)
	Start = TimeFunction()
	runService.Heartbeat:Connect(HeartbeatUpdate)
end)()

__notifAlign = "center"
__notifActive = {}
__notifGui = nil

function notify(text)
	task.spawn(function()
		if not __notifGui or not __notifGui.Parent then
			__notifGui = Instance.new("ScreenGui")
			__notifGui.Name = " "
			__notifGui.Parent = game.CoreGui
			__notifGui.ResetOnSpawn = false
		end
		local notifBack = Instance.new("Frame")
		notifBack.Parent = __notifGui
		notifBack.BackgroundColor3 = Color3.fromRGB(27, 22, 20)
		notifBack.BorderSizePixel = 0
		notifBack.Size = UDim2.new(0, 220, 0, 36)
		notifBack.ZIndex = 9999
		Instance.new("UICorner", notifBack).CornerRadius = UDim.new(0, 8)
		local notifBack2 = Instance.new("Frame")
		notifBack2.Parent = notifBack
		notifBack2.BackgroundColor3 = Color3.fromRGB(43, 43, 43)
		notifBack2.BorderSizePixel = 0
		notifBack2.Position = UDim2.new(0, 1, 0, 1)
		notifBack2.Size = UDim2.new(1, -2, 1, -2)
		notifBack2.ZIndex = 9999
		Instance.new("UICorner", notifBack2).CornerRadius = UDim.new(0, 8)
		local notifLine = Instance.new("Frame")
		notifLine.Parent = notifBack2
		notifLine.BackgroundColor3 = lib.accent
		notifLine.BorderSizePixel = 0
		notifLine.Size = UDim2.new(1, -16, 0, 2)
		notifLine.AnchorPoint = Vector2.new(1, 0)
		notifLine.Position = UDim2.new(0.96, 0, 0, 2)
		notifLine.ZIndex = 9999
		if lib.accentItems then table.insert(lib.accentItems, notifLine) end
		local notifText = Instance.new("TextLabel")
		notifText.Parent = notifBack2
		notifText.BackgroundTransparency = 1
		notifText.Position = UDim2.new(0, 0, 0, 6)
		notifText.Size = UDim2.new(1, 0, 1, -6)
		notifText.Font = Enum.Font.Arial
		notifText.Text = text
		notifText.TextColor3 = Color3.fromRGB(218, 218, 218)
		notifText.TextSize = 14
		notifText.TextStrokeColor3 = Color3.fromRGB(14, 14, 14)
		notifText.TextStrokeTransparency = 0.22
		notifText.ZIndex = 9999
		table.insert(__notifActive, notifBack)
		local idx = #(__notifActive)
		local gap = 42
		local function getPos(i)
			local yOff = (i - 1) * gap
			if __notifAlign == "left" then
				return UDim2.new(0, 10, 0, 10 + yOff), Vector2.new(0, 0)
			elseif __notifAlign == "right" then
				return UDim2.new(1, -230, 0, 10 + yOff), Vector2.new(1, 0)
			else
				return UDim2.new(0.5, 0, 0, 10 + yOff), Vector2.new(0.5, 0)
			end
		end
		local targetPos, targetAnchor = getPos(idx)
		notifBack.AnchorPoint = targetAnchor
		local slideStart
		if __notifAlign == "right" then
			notifBack.Position = UDim2.new(targetPos.X.Scale + 0.3, targetPos.X.Offset, targetPos.Y.Scale, targetPos.Y.Offset)
		else
			notifBack.Position = UDim2.new(targetPos.X.Scale - 0.3, targetPos.X.Offset, targetPos.Y.Scale, targetPos.Y.Offset)
		end
		slideStart = notifBack.Position
		for t = 0, 1, 0.08 do
			notifBack.Position = UDim2.new(
				slideStart.X.Scale + (targetPos.X.Scale - slideStart.X.Scale) * t,
				slideStart.X.Offset + (targetPos.X.Offset - slideStart.X.Offset) * t,
				slideStart.Y.Scale + (targetPos.Y.Scale - slideStart.Y.Scale) * t,
				slideStart.Y.Offset + (targetPos.Y.Offset - slideStart.Y.Offset) * t
			)
			task.wait(0.01)
		end
		notifBack.Position = targetPos
		task.wait(1.5)
		for i = 0, 1, 0.06 do
			notifText.TextStrokeTransparency = i
			notifText.TextTransparency = i
			notifLine.BackgroundTransparency = i
			notifLine.Size = UDim2.new(1 - i, -16 * (1 - i), 0, 2)
			notifBack.BackgroundTransparency = i
			notifBack2.BackgroundTransparency = i
			task.wait(0.01)
		end
		for k, v in pairs(__notifActive) do
			if v == notifBack then
				table.remove(__notifActive, k)
				break
			end
		end
		notifBack:Destroy()
		for i, remaining in pairs(__notifActive) do
			local p, a = getPos(i)
			remaining:TweenPosition(p, "Out", "Quad", 0.25, true)
		end
	end)
end

-- { UI } --

local window = lib.init("v3nom.cc", Color3.fromRGB(218, 154, 169), Enum.KeyCode.Insert)
if lib.accentItems then table.insert(lib.accentItems, kblistLine) end
radarLine.BackgroundColor3 = Color3.fromRGB(218, 154, 169)
ksLine.BackgroundColor3 = Color3.fromRGB(218, 154, 169)

task.spawn(function()
	task.wait(0.5)
	for _, gui in pairs(game.CoreGui:GetChildren()) do
		if gui:IsA("ScreenGui") then
			for _, v in pairs(gui:GetDescendants()) do
				if v:IsA("Frame") and v.Name == "uiColorButton" then
					local gloss = Instance.new("Frame")
					gloss.Name = "glossyHighlight"
					gloss.Parent = v
					gloss.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
					gloss.BackgroundTransparency = 0.7
					gloss.BorderSizePixel = 0
					gloss.Active = false
					gloss.Size = UDim2.new(1, 0, 0.45, 0)
					gloss.ZIndex = v.ZIndex + 1
					Instance.new("UICorner", gloss).CornerRadius = UDim.new(0, 6)
					local grad = Instance.new("UIGradient")
					grad.Parent = gloss
					grad.Transparency = NumberSequence.new({
						NumberSequenceKeypoint.new(0, 0.2),
						NumberSequenceKeypoint.new(1, 1)
					})
				end
				if v:IsA("Frame") and v.Name == "uiColorOutline" then
					local shadow = Instance.new("Frame")
					shadow.Name = "uiColorShadow"
					shadow.Parent = v.Parent
					shadow.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
					shadow.BackgroundTransparency = 0.75
					shadow.BorderSizePixel = 0
					shadow.Active = false
					shadow.Size = UDim2.new(v.Size.X.Scale, v.Size.X.Offset + 3, v.Size.Y.Scale, v.Size.Y.Offset + 3)
					shadow.Position = UDim2.new(v.Position.X.Scale, v.Position.X.Offset - 1.5, v.Position.Y.Scale, v.Position.Y.Offset - 1.5)
					shadow.ZIndex = v.ZIndex - 1
					Instance.new("UICorner", shadow).CornerRadius = UDim.new(0, 8)
				end
			end
		end
	end
end)

task.spawn(function()
	task.wait(0.5)
	for _, gui in pairs(game.CoreGui:GetChildren()) do
		if gui:IsA("ScreenGui") then
			for _, v in pairs(gui:GetDescendants()) do
				if v:IsA("Frame") and v.Name == "uiSliderFill" then
					local gloss = Instance.new("Frame")
					gloss.Name = "sliderGloss"
					gloss.Parent = v
					gloss.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
					gloss.BackgroundTransparency = 0.7
					gloss.BorderSizePixel = 0
					gloss.Active = false
					gloss.Size = UDim2.new(1, 0, 0.45, 0)
					gloss.ZIndex = v.ZIndex + 1
					Instance.new("UICorner", gloss).CornerRadius = UDim.new(0, 3)
					local grad = Instance.new("UIGradient")
					grad.Parent = gloss
					grad.Transparency = NumberSequence.new({
						NumberSequenceKeypoint.new(0, 0.2),
						NumberSequenceKeypoint.new(1, 1)
					})
				end
				if v:IsA("Frame") and v.Name == "uiSliderOutline" then
					local shadow = Instance.new("Frame")
					shadow.Name = "sliderShadow"
					shadow.Parent = v.Parent
					shadow.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
					shadow.BackgroundTransparency = 0.75
					shadow.BorderSizePixel = 0
					shadow.Active = false
					shadow.Size = UDim2.new(v.Size.X.Scale, v.Size.X.Offset + 3, v.Size.Y.Scale, v.Size.Y.Offset + 3)
					shadow.Position = UDim2.new(v.Position.X.Scale, v.Position.X.Offset - 1.5, v.Position.Y.Scale, v.Position.Y.Offset - 1.5)
					shadow.ZIndex = v.ZIndex - 1
					Instance.new("UICorner", shadow).CornerRadius = UDim.new(0, 5)
				end
			end
		end
	end
end)

local ragebot = window.createTab("ragebot", "rbxassetid://8667132506")
	local forcehit = ragebot.createSection("forcehit")
		local fhToggle = forcehit.createToggle("enabled", false, "fh_enabled", function(state)
			notify(state and "forcehit enabled" or "forcehit disabled")
			if not state and lib.flags["kb_connection"] then
				lib.flags["kb_connection"] = false
				if _G.__uiRefs and _G.__uiRefs["kb_connection"] then
					pcall(function() _G.__uiRefs["kb_connection"].set(false) end)
				end
			end
		end)
		task.spawn(function()
			task.wait(0.5)
			for _, tf in pairs(lib.tabframes or {}) do
				for _, v in pairs(tf:GetDescendants()) do
					if v:IsA("TextLabel") and v.Name == "uiButtonLabel" and v.Text == "enabled" then
						local row = v.Parent
						if row and row.Name == "uiSectionButton" then
							local fhPill = Instance.new("Frame")
							fhPill.Name = "fhKeybindPill"
							fhPill.Parent = row
							fhPill.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
							fhPill.BorderSizePixel = 0
							fhPill.Position = UDim2.new(0, 21, 0.5, -5)
							fhPill.Size = UDim2.new(0, 18, 0, 10)
							Instance.new("UICorner", fhPill).CornerRadius = UDim.new(0, 4)
							local fhPillStroke = Instance.new("UIStroke", fhPill)
							fhPillStroke.Color = Color3.fromRGB(53, 53, 53)
							fhPillStroke.Thickness = 1
							local fhPillLabel = Instance.new("TextLabel")
							fhPillLabel.Name = "fhPillLabel"
							fhPillLabel.Parent = fhPill
							fhPillLabel.BackgroundTransparency = 1
							fhPillLabel.Size = UDim2.new(1, 0, 1, 0)
							fhPillLabel.Font = Enum.Font.Arial
							fhPillLabel.Text = "none"
							fhPillLabel.TextColor3 = Color3.fromRGB(130, 130, 130)
							fhPillLabel.TextSize = 10
							fhPillLabel.TextStrokeTransparency = 0.5
							fhPill.InputBegan:Connect(function(input)
								if input.UserInputType == Enum.UserInputType.MouseButton1 then
									fhPillLabel.Text = "..."
									fhPillLabel.TextColor3 = lib.accent or Color3.fromRGB(218, 154, 169)
									local con
									con = userInputService.InputBegan:Connect(function(inp)
										if inp.UserInputType == Enum.UserInputType.Keyboard then
											_G.__forcehitKey = inp.KeyCode
											fhPillLabel.Text = inp.KeyCode.Name
											fhPillLabel.TextColor3 = Color3.fromRGB(208, 208, 208)
											con:Disconnect()
										end
									end)
								end
							end)
							_G.__fhToggleCon = userInputService.InputBegan:Connect(function(input)
								if input.UserInputType == Enum.UserInputType.Keyboard and _G.__forcehitKey and input.KeyCode == _G.__forcehitKey then
									if not lib.inDropdown and not lib.inColorPicker and not _G.__cfgTyping then
										lib.flags["fh_enabled"] = not lib.flags["fh_enabled"]
										if _G.__uiRefs and _G.__uiRefs["fh_enabled"] and _G.__uiRefs["fh_enabled"].set then
											pcall(function() _G.__uiRefs["fh_enabled"].set(lib.flags["fh_enabled"]) end)
										end
										notify(lib.flags["fh_enabled"] and "forcehit enabled" or "forcehit disabled")
									end
								end
							end)
							v.Position = UDim2.new(0, 42, 0, 0)
							v.Text = "enabled"
							break
						end
					end
				end
			end
		end)
		forcehit.createDropdown("hit part", {"Head", "HumanoidRootPart", "UpperTorso", "LowerTorso", "RightUpperArm", "RightLowerArm", "RightHand", "LeftUpperArm", "LeftLowerArm", "LeftHand", "RightUpperLeg", "RightLowerLeg", "RightFoot", "LeftUpperLeg", "LeftLowerLeg", "LeftFoot"}, "fh_hitpart", function() end)
		forcehit.createDropdown("checks", {"team check", "visible check", "ko check"}, "fh_checks", function() end)
	_G.__fhChecks = {["team check"] = false, ["visible check"] = false, ["ko check"] = false}
	lib.flags["fh_hitpart"] = "Head"
	lib.flags["fh_fillcolor"] = Color3.fromRGB(0, 0, 0)
	lib.flags["fh_outlinecolor"] = Color3.fromRGB(255, 255, 255)
	lib.flags["fh_filltrans"] = 50
	lib.flags["fh_outlinetrans"] = 0
		task.spawn(function()
			task.wait(0.5)
			for _, tf in pairs(lib.tabframes or {}) do
				for _, v in pairs(tf:GetDescendants()) do
					if v:IsA("TextLabel") and v.Name == "uiDropdownLabel" and v.Text == "checks" then
						local dropBack2 = v.Parent and v.Parent:FindFirstChild("uiDropdownOutline")
						dropBack2 = dropBack2 and dropBack2:FindFirstChild("uiDropdownBack")
						dropBack2 = dropBack2 and dropBack2:FindFirstChild("uiDropdownBack2")
						if dropBack2 then
							local selLabel = dropBack2.Parent and dropBack2.Parent:FindFirstChild("uiSliderSelectionsLabel")
							local allLabels = {}
							for _, opt in pairs(dropBack2:GetChildren()) do
								if opt:IsA("TextLabel") and opt.Name == "uiSliderSelection" then
									table.insert(allLabels, opt)
								end
							end
							for _, opt in pairs(allLabels) do
								opt.InputBegan:Connect(function(input)
									if input.UserInputType == Enum.UserInputType.MouseButton1 then
										local name = opt.Text
										_G.__fhChecks[name] = not _G.__fhChecks[name]
										for _, lbl in pairs(allLabels) do
											if _G.__fhChecks[lbl.Text] then
												game:GetService("TweenService"):Create(lbl, TweenInfo.new(0.33, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {TextColor3 = lib.accent or Color3.fromRGB(218, 154, 169)}):Play()
											else
												game:GetService("TweenService"):Create(lbl, TweenInfo.new(0.33, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {TextColor3 = Color3.fromRGB(208, 208, 208)}):Play()
											end
										end
										local active = {}
										for ck, cv in pairs(_G.__fhChecks) do
											if cv then table.insert(active, ck) end
										end
										if selLabel then
											selLabel.Text = #active > 0 and table.concat(active, ", ") or "none"
										end
									end
								end)
							end
						end
						break
					end
				end
			end
		end)
		forcehit.createToggle("autofire", false, "fh_autofire", function(state)
			notify(state and "autofire enabled" or "autofire disabled")
			for _, row in pairs(_G.__fhFoldRows or {}) do
				row.Visible = state
			end
		end)
		local fhCooldown = forcehit.createSlider("fire cooldown", 1, 0.1, 5, "s", "fh_cooldown", function() end)
		local fhFirerate = forcehit.createSlider("firerate", 30, 1, 100, "", "fh_firerate", function() end)
		forcehit.createToggle("sticky aim", false, "fh_sticky", function(state)
			notify(state and "sticky aim enabled" or "sticky aim disabled")
		end)
		forcehit.createToggle("autostomp", false, "fh_autostomp", function(state)
			notify(state and "autostomp enabled" or "autostomp disabled")
		end)
		forcehit.createToggle("highlight", false, "fh_highlight", function(state)
			notify(state and "highlight enabled" or "highlight disabled")
		end)
		forcehit.createColorpicker("fill color", Color3.fromRGB(0, 0, 0), false, "fh_fillcolor", function(clr)
			fhHighlight.FillColor = clr
		end)
		forcehit.createColorpicker("outline color", Color3.fromRGB(255, 255, 255), false, "fh_outlinecolor", function(clr)
			fhHighlight.OutlineColor = clr
		end)
		forcehit.createSlider("fill trans", 50, 0, 100, "%", "fh_filltrans", function(val)
			fhHighlight.FillTransparency = val / 100
		end)
		forcehit.createSlider("outline trans", 0, 0, 100, "%", "fh_outlinetrans", function(val)
			fhHighlight.OutlineTransparency = val / 100
		end)
		forcehit.createToggle("tracer", false, "fh_tracer", function(state)
			notify(state and "tracer enabled" or "tracer disabled")
			if not state then
				fhLine.Visible = false
				fhLineOutline.Visible = false
			end
			for _, row in pairs(_G.__fhTracerRows or {}) do
				row.Visible = state
			end
		end)
		forcehit.createColorpicker("tracer color", Color3.fromRGB(0, 120, 255), false, "fh_tracercolor", function(clr)
			fhLine.Color = clr
		end)
		forcehit.createColorpicker("tracer outline", Color3.fromRGB(0, 0, 0), false, "fh_traceroutline", function(clr)
			fhLineOutline.Color = clr
		end)
		task.spawn(function()
			task.wait(0.5)
			local tracerBtnA, tracerBtnB, tracerToggleRow
			for _, tf in pairs(lib.tabframes or {}) do
				for _, v in pairs(tf:GetDescendants()) do
					if v:IsA("TextLabel") and v.Name == "uiColorLabel" and v.Text == "tracer color" then
						local row = v.Parent
						if row and row.Visible then
							tracerBtnA = row:FindFirstChild("uiColorOutline")
							row.Visible = false
						end
					end
					if v:IsA("TextLabel") and v.Name == "uiColorLabel" and v.Text == "tracer outline" then
						local row = v.Parent
						if row and row.Visible then
							tracerBtnB = row:FindFirstChild("uiColorOutline")
							row.Visible = false
						end
					end
					if v:IsA("TextLabel") and v.Name == "uiButtonLabel" and v.Text == "tracer" then
						local row = v.Parent
						if row and row.Name == "uiSectionButton" then
							tracerToggleRow = row
						end
					end
				end
			end
			if tracerToggleRow and tracerBtnA and tracerBtnB then
				tracerBtnA.Size = UDim2.new(0, 10, 0, 10)
				tracerBtnA.Position = UDim2.new(1, -50, 0.5, -5)
				tracerBtnA.Parent = tracerToggleRow
				local cornerA = tracerBtnA:FindFirstChildOfClass("UICorner")
				if cornerA then cornerA.CornerRadius = UDim.new(0, 4) end
				tracerBtnB.Size = UDim2.new(0, 10, 0, 10)
				tracerBtnB.Position = UDim2.new(1, -30, 0.5, -5)
				tracerBtnB.Parent = tracerToggleRow
				local cornerB = tracerBtnB:FindFirstChildOfClass("UICorner")
				if cornerB then cornerB.CornerRadius = UDim.new(0, 4) end
			end
		end)
		forcehit.createSlider("thickness", 2, 1, 10, "", "fh_thickness", function(val)
			fhLine.Thickness = val
			fhLineOutline.Thickness = val + 1.5
		end)
		local extra = ragebot.createSection("extra")
		extra.createToggle("target strafe", false, "fh_strafe", function(state)
			notify(state and "target strafe enabled" or "target strafe disabled")
			for _, row in pairs(_G.__fhStrafeRows or {}) do
				row.Visible = state
			end
		end)
			extra.createDropdown("method", {"orbit", "random"}, "fh_strafemethod", function() end)
			lib.flags["fh_strafemethod"] = "orbit"
			extra.createSlider("strafe speed", 5, 1, 20, "", "fh_strafespeed", function() end)
			extra.createSlider("strafe height", 3, 0, 10, "", "fh_strafeheight", function() end)
			extra.createSlider("strafe range", 5, 1, 15, "", "fh_swaferange", function() end)
			task.defer(function()
				_G.__fhStrafeRows = {}
				local toggleFrame
				for _, v in pairs(game.CoreGui:GetDescendants()) do
					if v:IsA("TextLabel") and v.Text == "target strafe" then
						toggleFrame = v.Parent
						break
					end
				end
				if toggleFrame and toggleFrame.Parent then
					local children = toggleFrame.Parent:GetChildren()
					local foundToggle = false
					for _, child in pairs(children) do
						if child == toggleFrame then
							foundToggle = true
						elseif foundToggle then
							if child.Name == "uiSectionButton" then
								break
							elseif child.Name == "uiSectionDropdown" or child.Name == "uiSectionSlider" then
								table.insert(_G.__fhStrafeRows, child)
							end
						end
					end
					for _, row in pairs(_G.__fhStrafeRows) do
						row.Visible = false
					end
				end
			end)
			extra.createToggle("face target", false, "fh_facetarget", function(state)
				notify(state and "face target enabled" or "face target disabled")
			end)
			extra.createToggle("spectate", false, "fh_spectate", function(state)
				notify(state and "spectate enabled" or "spectate disabled")
				if not state then
					local cam = workspace.CurrentCamera
					cam.CameraType = Enum.CameraType.Custom
					cam.CameraSubject = client.player.Character and client.player.Character:FindFirstChildOfClass("Humanoid")
				end
			end)
			extra.createToggle("hitbox expander", false, "fh_hitboxexpand", function(state)
				notify(state and "hitbox expander enabled" or "hitbox expander disabled")
			end)
			extra.createToggle("visualizer", false, "fh_visualizer", function(state)
			notify(state and "visualizer enabled" or "visualizer disabled")
			end)
			extra.createColorpicker("fill color", Color3.fromRGB(0, 120, 255), false, "fh_visfillcolor", function() end)
			extra.createColorpicker("outline color", Color3.fromRGB(0, 0, 0), false, "fh_visoutlinecolor", function() end)
			lib.flags["fh_visfillcolor"] = Color3.fromRGB(0, 120, 255)
			lib.flags["fh_visoutlinecolor"] = Color3.new(0, 0, 0)
			extra.createToggle("target notifs", false, "fh_targetnotifs", function(state)
				notify(state and "target notifs enabled" or "target notifs disabled")
			end)
		task.spawn(function()
			task.wait(0.5)
			_G.__fhVisRows = {}
			-- visualizer: grab the remaining VISIBLE fill/outline color buttons (highlight's are already hidden)
			local visBtnA, visBtnB
			for _, tf in pairs(lib.tabframes or {}) do
				for _, v in pairs(tf:GetDescendants()) do
					if v:IsA("TextLabel") and v.Name == "uiColorLabel" and v.Text == "fill color" then
						local row = v.Parent
						if row and row.Visible then
							visBtnA = row:FindFirstChild("uiColorOutline")
							row.Visible = false
						end
					end
					if v:IsA("TextLabel") and v.Name == "uiColorLabel" and v.Text == "outline color" then
						local row = v.Parent
						if row and row.Visible then
							visBtnB = row:FindFirstChild("uiColorOutline")
							row.Visible = false
						end
					end
				end
			end
			local visToggleRow
			if visBtnA then
				for _, tf in pairs(lib.tabframes or {}) do
					for _, v in pairs(tf:GetDescendants()) do
						if v:IsA("TextLabel") and v.Name == "uiButtonLabel" and v.Text == "visualizer" then
							visToggleRow = v.Parent
							break
						end
					end
					if visToggleRow then break end
				end
			end
			if visToggleRow and visBtnA and visBtnB then
				visBtnA.Size = UDim2.new(0, 10, 0, 10)
				visBtnA.Position = UDim2.new(1, -50, 0.5, -5)
				visBtnA.Parent = visToggleRow
				local cornerA = visBtnA:FindFirstChildOfClass("UICorner")
				if cornerA then cornerA.CornerRadius = UDim.new(0, 3) end
				visBtnB.Size = UDim2.new(0, 10, 0, 10)
				visBtnB.Position = UDim2.new(1, -30, 0.5, -5)
				visBtnB.Parent = visToggleRow
				local cornerB = visBtnB:FindFirstChildOfClass("UICorner")
				if cornerB then cornerB.CornerRadius = UDim.new(0, 3) end
			end
			for _, tf in pairs(lib.tabframes or {}) do
				for _, v in pairs(tf:GetDescendants()) do
					if v:IsA("TextLabel") and v.Name == "uiSliderLabel" and v.Text:find("fill transparency") then
						local row = v.Parent
						if row then
							table.insert(_G.__fhVisRows, row)
							if not lib.flags["fh_visualizer"] then row.Visible = false end
						end
					end
				end
			end
		end)

local knifebotTab = window.createTab("knifebot", "rbxassetid://8595329857")
	local kbSection = knifebotTab.createSection("knifebot")
		local kbConnRef = nil
		local kbConnToggle = kbSection.createToggle("connection", false, "kb_connection", function(state)
			notify(state and "knifebot connected" or "knifebot disconnected")
		end)
		kbConnRef = kbConnToggle
		task.spawn(function()
			task.wait(0.5)
			-- find the knifebot tab frame (contains "attach position" unique to knifebot)
			local kbTabFrame
			for _, tf in pairs(lib.tabframes or {}) do
				for _, v in pairs(tf:GetDescendants()) do
					if v:IsA("TextLabel") and v.Name == "uiDropdownLabel" and v.Text == "attach position" then
						kbTabFrame = tf
						break
					end
				end
				if kbTabFrame then break end
			end
			-- search only within the knifebot tab for "connection"
			if kbTabFrame then
				for _, v in pairs(kbTabFrame:GetDescendants()) do
					if v:IsA("TextLabel") and v.Name == "uiButtonLabel" and v.Text == "connection" then
						local row = v.Parent
						if row and row.Name == "uiSectionButton" then
							local kbPill = Instance.new("Frame")
							kbPill.Name = "kbKeybindPill"
							kbPill.Parent = row
							kbPill.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
							kbPill.BorderSizePixel = 0
							kbPill.Position = UDim2.new(0, 21, 0.5, -5)
							kbPill.Size = UDim2.new(0, 18, 0, 10)
							Instance.new("UICorner", kbPill).CornerRadius = UDim.new(0, 4)
							local kbPillStroke = Instance.new("UIStroke", kbPill)
							kbPillStroke.Color = Color3.fromRGB(53, 53, 53)
							kbPillStroke.Thickness = 1
							local kbPillLabel = Instance.new("TextLabel")
							kbPillLabel.Name = "kbPillLabel"
							kbPillLabel.Parent = kbPill
							kbPillLabel.BackgroundTransparency = 1
							kbPillLabel.Size = UDim2.new(1, 0, 1, 0)
							kbPillLabel.Font = Enum.Font.Arial
							kbPillLabel.Text = "Q"
							kbPillLabel.TextColor3 = Color3.fromRGB(130, 130, 130)
							kbPillLabel.TextSize = 10
							kbPillLabel.TextStrokeTransparency = 0.5
							local kbChangingKey = false
							kbPill.InputBegan:Connect(function(input)
								if input.UserInputType == Enum.UserInputType.MouseButton1 then
									kbChangingKey = true
									kbPillLabel.Text = "..."
									kbPillLabel.TextColor3 = lib.accent or Color3.fromRGB(218, 154, 169)
									local con
									con = userInputService.InputBegan:Connect(function(inp)
										if inp.UserInputType == Enum.UserInputType.Keyboard then
											_G.__kbLockKey = inp.KeyCode
											kbPillLabel.Text = inp.KeyCode.Name
											kbPillLabel.TextColor3 = Color3.fromRGB(208, 208, 208)
											kbChangingKey = false
											con:Disconnect()
										end
									end)
								end
							end)
							if _G.__kbKeyToggleCon then pcall(function() _G.__kbKeyToggleCon:Disconnect() end) end
							_G.__kbKeyToggleCon = userInputService.InputBegan:Connect(function(input)
								if kbChangingKey then return end
								if input.UserInputType == Enum.UserInputType.Keyboard and input.KeyCode == _G.__kbLockKey then
									if not lib.inDropdown and not lib.inColorPicker and not _G.__cfgTyping then
										lib.flags["kb_connection"] = not lib.flags["kb_connection"]
										notify(lib.flags["kb_connection"] and "knifebot connected" or "knifebot disconnected")
										if kbConnRef and kbConnRef.set then
											pcall(function() kbConnRef.set(lib.flags["kb_connection"]) end)
										end
									end
								end
							end)
							v.Position = UDim2.new(0, 42, 0, 0)
							v.Text = "connection"
							break
						end
					end
				end
			end
		end)
		kbSection.createDropdown("attach position", {"HumanoidRootPart", "UpperTorso", "LowerTorso", "Head", "Torso"}, "kb_attachpart", function() end)
		lib.flags["kb_attachpart"] = "HumanoidRootPart"
		kbSection.createToggle("distance check", false, "kb_distancecheck", function(state)
			for _, row in pairs(_G.__kbDistRows or {}) do
				row.Visible = state
			end
		end)
		kbSection.createSlider("max distance", 100, 1, 500, "m", "kb_maxdistance", function() end)
		kbSection.createToggle("auto stomp", false, "kb_autostomp", function(state)
			notify(state and "kb auto stomp enabled" or "kb auto stomp disabled")
		end)
		kbSection.createToggle("hitbox expander", false, "kb_hitboxexpand", function(state)
			notify(state and "kb hitbox expander enabled" or "kb hitbox expander disabled")
		end)
		kbSection.createToggle("target line", false, "kb_tracer", function(state)
			notify(state and "kb tracer enabled" or "kb tracer disabled")
			if not state then
				if _G.__kbLine then _G.__kbLine.Visible = false end
				if _G.__kbLineOutline then _G.__kbLineOutline.Visible = false end
			end
		end)
		kbSection.createSlider("tracer thickness", 2, 1, 10, "", "kb_tracerthickness", function() end)
		kbSection.createToggle("resolver", false, "kb_resolver", function(state)
			notify(state and "kb resolver enabled" or "kb resolver disabled")
		end)
		kbSection.createToggle("auto swing", false, "kb_autoswing", function(state)
			notify(state and "kb auto swing enabled" or "kb auto swing disabled")
			for _, row in pairs(_G.__kbSwingRows or {}) do
				row.Visible = state
			end
		end)
		kbSection.createSlider("swing delay", 0, 0, 1, "s", "kb_swingdelay", function() end)
		kbSection.createToggle("auto knife", false, "kb_autoknife", function(state)
			notify(state and "auto knife enabled" or "auto knife disabled")
			if state then
				local plr = playerService.LocalPlayer
				local function findKnife()
					local backpack = plr:FindFirstChild("Backpack")
					if not backpack then return nil end
					for _, tool in ipairs(backpack:GetChildren()) do
						if tool:IsA("Tool") and tool.Name:lower():find("knife") then
							return tool
						end
					end
				end
				local function equipKnife(character)
					local h = character:FindFirstChildOfClass("Humanoid")
					if not h then return end
					for _ = 1, 100 do
						local knife = findKnife()
						if knife then
							h:EquipTool(knife)
							return
						end
						for _, tool in ipairs(character:GetChildren()) do
							if tool:IsA("Tool") and tool.Name:lower():find("knife") then
								return
							end
						end
						task.wait(0.1)
					end
				end
				if _G.__autoKnifeCon then pcall(function() _G.__autoKnifeCon:Disconnect() end) end
				_G.__autoKnifeCon = plr.CharacterAdded:Connect(function(character)
					character:WaitForChild("Humanoid")
					task.wait(0.1)
					equipKnife(character)
				end)
				if plr.Character then
					task.spawn(function() equipKnife(plr.Character) end)
				end
			else
				if _G.__autoKnifeCon then pcall(function() _G.__autoKnifeCon:Disconnect() end); _G.__autoKnifeCon = nil end
			end
		end)
	_G.__kbLockKey = Enum.KeyCode.Q
	task.spawn(function()
		task.wait(0.5)
		_G.__kbTracerRows = {}
		_G.__kbSwingRows = {}
		_G.__kbDistRows = {}
		for _, tf in pairs(lib.tabframes or {}) do
			local isKBTab = false
			for _, v in pairs(tf:GetDescendants()) do
				if v:IsA("TextLabel") and v.Name == "uiDropdownLabel" and v.Text == "attach position" then
					isKBTab = true
					break
				end
			end
			if isKBTab then
			for _, v in pairs(tf:GetDescendants()) do
				if v:IsA("TextLabel") and v.Name == "uiSliderLabel" and v.Text:find("tracer thickness") then
					local row = v.Parent
					if row then
						table.insert(_G.__kbTracerRows, row)
						if not lib.flags["kb_tracer"] then row.Visible = false end
					end
				end
				if v:IsA("TextLabel") and v.Name == "uiSliderLabel" and v.Text:find("swing delay") then
					local row = v.Parent
					if row then
						table.insert(_G.__kbSwingRows, row)
						if not lib.flags["kb_autoswing"] then row.Visible = false end
					end
				end
				if v:IsA("TextLabel") and v.Name == "uiSliderLabel" and v.Text:find("max distance") then
					local row = v.Parent
					if row then
						table.insert(_G.__kbDistRows, row)
						if not lib.flags["kb_distancecheck"] then row.Visible = false end
					end
				end
			end
			end
		end
	end)

local rage = window.createTab("rage", "rbxassetid://8595329857")
	local rageMain = rage.createSection("main")
		rageMain.createToggle("anti void", false, "antivoid", function(state)
			notify(state and "anti void enabled" or "anti void disabled")
		end)
		rageMain.createToggle("anti stomp", false, "antistomp", function(state)
			notify(state and "anti stomp enabled" or "anti stomp disabled")
			for _, row in pairs(_G.__kbAntiStompRows or {}) do
				row.Visible = state
			end
		end)
		rageMain.createSlider("threshold", 29, 1, 100, "", "antisthreshold", function() end)
		rageMain.createToggle("auto reload", true, "autoreload", function(state)
			notify(state and "auto reload enabled" or "auto reload disabled")
		end)
		rageMain.createToggle("rolex", false, "rolex", function(state)
			notify(state and "rolex enabled" or "rolex disabled")
		end)
		rageMain.createToggle("no recoil", false, "norecoil", function(state)
			notify(state and "no recoil enabled" or "no recoil disabled")
			for _, row in pairs(_G.__nrRows or {}) do row.Visible = state end
		end)
		rageMain.createSlider("strength", 10, 1, 50, "", "nr_strength", function() end)
		rageMain.createToggle("wings", false, "wings", function(state)
			notify(state and "wings enabled" or "wings disabled")
			for _, row in pairs(_G.__wingRows or {}) do row.Visible = state end
		end)
		rageMain.createDropdown("wing type", {"1", "2", "3", "4"}, "wing_type", function() end)
		lib.flags["wing_type"] = "1"
		rageMain.createColorpicker("wing color", Color3.fromRGB(255, 255, 255), false, "wing_color", function(clr)
			local char = client.player.Character
			if char then
				for _, d in pairs(char:GetDescendants()) do
					if d:IsA("Model") and d.Name == "Angel Wings" then
						for _, bp in pairs(d:GetDescendants()) do
							if bp:IsA("BasePart") then
								bp.Color = clr
								for _, dec in pairs(bp:GetDescendants()) do
									if dec:IsA("Decal") then dec.Color3 = clr end
								end
							end
						end
					end
				end
			end
		end)
		rageMain.createToggle("rapid fire", false, "rapidfire", function(state)
			notify(state and "rapid fire enabled" or "rapid fire disabled")
		end)
		rageMain.createToggle("tool giver", false, "toolgiver", function(state)
			notify(state and "tool giver enabled" or "tool giver disabled")
		end)
		rageMain.createToggle("fly", false, "fly", function(state)
			notify(state and "fly enabled" or "fly disabled")
			for _, row in pairs(_G.__flyRows or {}) do row.Visible = state end
		end)
		rageMain.createSlider("speed", 50, 1, 500, "", "fly_speed", function() end)
		task.spawn(function()
			task.wait(0.5)
			for _, tf in pairs(lib.tabframes or {}) do
				for _, v in pairs(tf:GetDescendants()) do
					if v:IsA("TextLabel") and v.Name == "uiButtonLabel" and v.Text == "fly" then
						local row = v.Parent
						if row and row.Name == "uiSectionButton" then
							local flPill = Instance.new("Frame")
							flPill.Name = "flyKeybindPill"
							flPill.Parent = row
							flPill.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
							flPill.BorderSizePixel = 0
							flPill.Position = UDim2.new(0, 21, 0.5, -5)
							flPill.Size = UDim2.new(0, 18, 0, 10)
							Instance.new("UICorner", flPill).CornerRadius = UDim.new(0, 4)
							local flPillStroke = Instance.new("UIStroke", flPill)
							flPillStroke.Color = Color3.fromRGB(53, 53, 53)
							flPillStroke.Thickness = 1
							local flPillLabel = Instance.new("TextLabel")
							flPillLabel.Name = "flPillLabel"
							flPillLabel.Parent = flPill
							flPillLabel.BackgroundTransparency = 1
							flPillLabel.Size = UDim2.new(1, 0, 1, 0)
							flPillLabel.Font = Enum.Font.Arial
							flPillLabel.Text = "none"
							flPillLabel.TextColor3 = Color3.fromRGB(130, 130, 130)
							flPillLabel.TextSize = 10
							flPillLabel.TextStrokeTransparency = 0.5
							flPill.InputBegan:Connect(function(input)
								if input.UserInputType == Enum.UserInputType.MouseButton1 then
									flPillLabel.Text = "..."
									flPillLabel.TextColor3 = lib.accent or Color3.fromRGB(218, 154, 169)
									local con
									con = userInputService.InputBegan:Connect(function(inp)
										if inp.UserInputType == Enum.UserInputType.Keyboard then
											_G.__flyKey = inp.KeyCode
											flPillLabel.Text = inp.KeyCode.Name
											flPillLabel.TextColor3 = Color3.fromRGB(208, 208, 208)
											con:Disconnect()
										end
									end)
								end
							end)
							_G.__flyKeyCon = userInputService.InputBegan:Connect(function(input)
								if input.UserInputType == Enum.UserInputType.Keyboard and _G.__flyKey and input.KeyCode == _G.__flyKey then
									if not lib.inDropdown and not lib.inColorPicker and not _G.__cfgTyping then
										lib.flags["fly"] = not lib.flags["fly"]
										if _G.__uiRefs and _G.__uiRefs["fly"] and _G.__uiRefs["fly"].set then
											pcall(function() _G.__uiRefs["fly"].set(lib.flags["fly"]) end)
										end
										notify(lib.flags["fly"] and "fly enabled" or "fly disabled")
										for _, row in pairs(_G.__flyRows or {}) do row.Visible = lib.flags["fly"] end
									end
								end
							end)
							v.Position = UDim2.new(0, 42, 0, 0)
							v.Text = "fly"
							break
						end
					end
				end
			end
		end)

		_G.__flyRows = {}
		task.spawn(function()
			task.wait(0.5)
			for _, tf in pairs(lib.tabframes or {}) do
				for _, v in pairs(tf:GetDescendants()) do
					if v:IsA("TextLabel") and v.Name == "uiSliderLabel" and v.Text:find("speed") then
						local row = v.Parent
						if row then
							table.insert(_G.__flyRows, row)
							if not lib.flags["fly"] then row.Visible = false end
						end
					end
				end
			end
		end)

		task.spawn(function()
			task.wait(0.5)
			_G.__nrRows = {}
			_G.__wingRows = {}
			for _, tf in pairs(lib.tabframes or {}) do
				for _, v in pairs(tf:GetDescendants()) do
					if v:IsA("TextLabel") and v.Name == "uiSliderLabel" and v.Text:find("strength") then
						local row = v.Parent
						if row then
							table.insert(_G.__nrRows, row)
							if not lib.flags["norecoil"] then row.Visible = false end
						end
					end
					if v:IsA("TextLabel") and ((v.Name == "uiDropdownLabel" and v.Text:find("wing")) or (v.Name == "uiColorLabel" and v.Text:find("wing"))) then
						local row = v.Parent
						if row then
							table.insert(_G.__wingRows, row)
							if not lib.flags["wings"] then row.Visible = false end
						end
					end
				end
			end
		end)


	local rolexConn, rolexCharConn
	local function rolexCleanup()
		if rolexConn then rolexConn:Disconnect() rolexConn = nil end
	end
	local function rolexApply()
		if not lib.flags["rolex"] then return end
		local char = client.player.Character
		if not char then return end
		local rh = char:FindFirstChild("RightHand") or char:FindFirstChild("Right Arm")
		if not rh then return end
		rolexCleanup()
		local ok, rolexModel = pcall(function()
			return game:GetService("ReplicatedStorage"):WaitForChild("PlatinumRolex"):Clone()
		end)
		if not ok or not rolexModel then return end
		rolexModel.Parent = char
		for _, part in ipairs(rolexModel:GetDescendants()) do
			if part:IsA("BasePart") then
				part.Anchored = true
				part.CanCollide = false
			end
		end
		local offset = CFrame.new(0, 0.3, 0) * CFrame.Angles(0, math.rad(50), 0)
		rolexConn = runService.RenderStepped:Connect(LPH_NO_VIRTUALIZE(function()
			if lib.flags["rolex"] and rh and rh.Parent and rolexModel.PrimaryPart then
				pcall(function() rolexModel:SetPrimaryPartCFrame(rh.CFrame * offset) end)
			end
		end))
	end
	rolexCharConn = client.player.CharacterAdded:Connect(function()
		if lib.flags["rolex"] then task.wait(0.25) rolexApply() end
	end)
	task.spawn(LPH_NO_VIRTUALIZE(function()
		while true do
			task.wait(0.5)
			if lib.flags["rolex"] and not rolexConn then
				pcall(rolexApply)
			elseif not lib.flags["rolex"] and rolexConn then
				rolexCleanup()
				local char = client.player.Character
				if char then
					for _, d in pairs(char:GetDescendants()) do
						if d:IsA("Model") and d.Name == "PlatinumRolex" then d:Destroy() end
					end
				end
			end
		end
	end))
	local nrConn
	local function noRecoilApply()
		if not lib.flags["norecoil"] then return end
		local char = client.player.Character
		if not char then return end
		local be = char:FindFirstChild("BodyEffects")
		if not be then return end
		local gc = be:FindFirstChild("GunChanges")
		if not gc then return end
		if gc:IsA("NumberValue") or gc:IsA("IntValue") then
			gc.Value = (lib.flags["nr_strength"] or 10) * 1000
		end
	end
	local function noRecoilCleanup()
		if nrConn then nrConn:Disconnect() nrConn = nil end
	end
	client.player.CharacterAdded:Connect(function(char)
		if lib.flags["norecoil"] then
			task.wait(0.25)
			noRecoilApply()
			local be = char:WaitForChild("BodyEffects", 5)
			if be then
				local gc = be:WaitForChild("GunChanges", 5)
				if gc then
					nrConn = gc.Changed:Connect(LPH_NO_VIRTUALIZE(function()
						if lib.flags["norecoil"] then
							gc.Value = (lib.flags["nr_strength"] or 10) * 1000
						end
					end))
				end
			end
		end
	end)
	if client.player.Character then
		pcall(function()
			local be = client.player.Character:WaitForChild("BodyEffects", 5)
			if be then
				local gc = be:WaitForChild("GunChanges", 5)
				if gc and (gc:IsA("NumberValue") or gc:IsA("IntValue")) then
					nrConn = gc.Changed:Connect(LPH_NO_VIRTUALIZE(function()
						if lib.flags["norecoil"] then
							gc.Value = (lib.flags["nr_strength"] or 10) * 1000
						end
					end))
				end
			end
		end)
	end

	local wingConn, wingCharConn
	local function wingCleanup()
		if wingConn then wingConn:Disconnect() wingConn = nil end
	end
	local function wingApply()
		if not lib.flags["wings"] then return end
		local char = client.player.Character
		if not char then return end
		local torso = char:FindFirstChild("UpperTorso")
		local hrp = char:FindFirstChild("HumanoidRootPart")
		if not torso or not hrp then return end
		wingCleanup()
		for _, d in pairs(char:GetDescendants()) do
			if d:IsA("Model") and d.Name == "Angel Wings" then d:Destroy() end
		end
		local ok, wing = pcall(function()
			return game:GetService("ReplicatedStorage"):WaitForChild("EquipableItem"):WaitForChild("Angel Wings"):Clone()
		end)
		if not ok or not wing then return end
		wing.Parent = char
		local handle = wing:FindFirstChild("Handle")
		if not handle then return end
		handle.Anchored = false
		handle.CanCollide = false
		local wc = lib.flags["wing_color"]
		if wc and typeof(wc) == "Color3" then
			for _, p in pairs(wing:GetDescendants()) do
				if p:IsA("BasePart") then
					for _, dec in pairs(p:GetDescendants()) do
						if dec:IsA("SurfaceAppearance") then pcall(function() dec:Destroy() end) end
						if dec:IsA("Decal") then dec.Color3 = wc end
					end
					p.Color = wc
				end
			end
		end
		local m = Instance.new("Motor6D")
		m.Part0 = torso
		m.Part1 = handle
		m.C0 = CFrame.new()
		m.Parent = torso
		local t = 0
		local wtype = lib.flags["wing_type"] or "1"
		wingConn = runService.RenderStepped:Connect(LPH_NO_VIRTUALIZE(function(dt)
			if not lib.flags["wings"] or not m or not m.Parent then return end
			t = t + dt * 0.8
			local speed = math.clamp(hrp.Velocity.Magnitude / 10, 0, 1)
			if wtype == "1" then
				local flap = math.sin(t * 1.5) * math.rad(10) * (0.5 + speed)
				local twist = math.sin(t * 1.8) * math.rad(3)
				m.C0 = CFrame.new() * CFrame.Angles(flap, 0, twist)
			elseif wtype == "2" then
				local flap = math.sin(t * 1.5) * math.rad(10) * (0.5 + speed)
				local twist = math.sin(t * 1.8) * math.rad(3)
				m.C0 = CFrame.new() * CFrame.Angles(flap, 0, twist)
			elseif wtype == "3" then
				local sway = math.sin(t * 2) * 0.05
				m.C0 = CFrame.new() * CFrame.Angles(0, 0, sway)
			else
				local sway = math.sin(t * 2) * 0.05
				m.C0 = CFrame.new() * CFrame.Angles(0, 0, sway)
			end
		end))
	end
	wingCharConn = client.player.CharacterAdded:Connect(function()
		if lib.flags["wings"] then task.wait(0.25) wingApply() end
	end)
	task.spawn(LPH_NO_VIRTUALIZE(function()
		while true do
			task.wait(0.5)
			if lib.flags["wings"] and not wingConn then
				pcall(wingApply)
			elseif not lib.flags["wings"] and wingConn then
				wingCleanup()
				local char = client.player.Character
				if char then
					for _, d in pairs(char:GetDescendants()) do
						if d:IsA("Model") and d.Name == "Angel Wings" then d:Destroy() end
					end
				end
			end
		end
	end))
	local toolNames = {"[Flintlock]"}
	local function rfPatchTool(t)
		if t and t:FindFirstChild("GunData") then
			local ok, m = pcall(require, t.GunData)
			if ok and m then
				m["slowdown_time"] = -math.huge
				m["cooldown"] = -math.huge
			end
		end
	end
	local function rfApply()
		if not lib.flags["rapidfire"] then return end
		pcall(function()
			local c = client.player.Character or client.player.CharacterAdded:Wait()
			local b = client.player:WaitForChild("Backpack")
			for _, t in ipairs(c:GetChildren()) do if t:IsA("Tool") then rfPatchTool(t) end end
			for _, t in ipairs(b:GetChildren()) do if t:IsA("Tool") then rfPatchTool(t) end end
			for _, n in ipairs(toolNames) do
				local g = c:FindFirstChild(n)
				if g and g:FindFirstChild("Script") and g.Script:FindFirstChild("Ammo") and g.Script.Ammo:FindFirstChild("CLIENT") then
					g.Script.Ammo.CLIENT.Value = math.huge
				end
			end
		end)
	end
	client.player.CharacterAdded:Connect(LPH_NO_VIRTUALIZE(function(c)
		if not lib.flags["rapidfire"] then return end
		task.wait(0.5)
		pcall(function()
			local b = client.player:WaitForChild("Backpack")
			for _, t in ipairs(c:GetChildren()) do if t:IsA("Tool") then rfPatchTool(t) end end
			for _, t in ipairs(b:GetChildren()) do if t:IsA("Tool") then rfPatchTool(t) end end
			for _, n in ipairs(toolNames) do
				local g = c:FindFirstChild(n)
				if g and g:FindFirstChild("Script") and g.Script:FindFirstChild("Ammo") and g.Script.Ammo:FindFirstChild("CLIENT") then
					g.Script.Ammo.CLIENT.Value = math.huge
				end
			end
		end)
	end))
task.spawn(LPH_NO_VIRTUALIZE(function()
	while true do
			task.wait(1)
			if lib.flags["rapidfire"] then pcall(rfApply) end
		end
	end))

	local tgConn, tgDescConn
	local tgTools = {
		["[Flintlock]"] = true,
		["[Heart Balloon]"] = true,
	}
	local tgAcquired = {}
	local function tgCleanup()
		if tgConn then tgConn:Disconnect() tgConn = nil end
		if tgDescConn then tgDescConn:Disconnect() tgDescConn = nil end
		table.clear(tgAcquired)
	end
	local function tgOwns(name)
		local ok, res = pcall(function()
			local b = client.player:FindFirstChild("Backpack")
			local c = client.player.Character
			return (b and b:FindFirstChild(name)) or (c and c:FindFirstChild(name))
		end)
		return ok and res or false
	end
	local function tgGrab(obj)
		if not lib.flags["toolgiver"] then return end
		if not obj or not obj:IsA("Tool") then return end
		if not tgTools[obj.Name] then return end
		if tgOwns(obj.Name) or tgAcquired[obj.Name] then return end
		tgAcquired[obj.Name] = true
		pcall(function()
			local bp = client.player:FindFirstChild("Backpack")
			if bp then
				local copy = obj:Clone()
				task.wait(0.1)
				copy.Parent = bp
			end
		end)
	end
	local function tgSweep(container)
		if not container then return end
		pcall(function()
			for _, obj in ipairs(container:GetDescendants()) do
				if obj:IsA("Tool") and tgTools[obj.Name] and not tgOwns(obj.Name) and not tgAcquired[obj.Name] then
					tgGrab(obj)
				end
			end
		end)
	end
	local function tgLoop()
		tgSweep(workspace)
		for _, pl in ipairs(playerService:GetPlayers()) do
			if pl ~= client.player then
				if pl.Character then tgSweep(pl.Character) end
				local b = pl:FindFirstChild("Backpack")
				if b then tgSweep(b) end
			end
		end
	end
	tgDescConn = workspace.DescendantAdded:Connect(LPH_NO_VIRTUALIZE(function(obj)
		if not lib.flags["toolgiver"] then return end
		if obj:IsA("Tool") and tgTools[obj.Name] then
			task.wait(0.1)
			pcall(tgGrab, obj)
		end
	end))
	task.spawn(LPH_NO_VIRTUALIZE(function()
		while true do
			task.wait(0.5)
			if lib.flags["toolgiver"] then
				tgLoop()
			end
		end
	end))
	client.player.CharacterAdded:Connect(function(ch)
		if not lib.flags["toolgiver"] then return end
		task.wait(1)
		tgSweep(ch)
	end)

	local flyConn
	local function flyStart()
		local char = client.player.Character
		if not char then return end
		local hrp = char:FindFirstChild("HumanoidRootPart")
		local hum = char:FindFirstChildOfClass("Humanoid")
		if not hrp or not hum then return end
		flyConn = runService.Heartbeat:Connect(LPH_NO_VIRTUALIZE(function()
			if not lib.flags["fly"] then return end
			local cam = workspace.CurrentCamera
			if not cam then return end
			local sp = (lib.flags["fly_speed"] or 50) / 10
			local dir = Vector3.new()
			if userInputService:IsKeyDown(Enum.KeyCode.W) then dir = dir + cam.CFrame.LookVector end
			if userInputService:IsKeyDown(Enum.KeyCode.S) then dir = dir - cam.CFrame.LookVector end
			if userInputService:IsKeyDown(Enum.KeyCode.A) then dir = dir - cam.CFrame.RightVector end
			if userInputService:IsKeyDown(Enum.KeyCode.D) then dir = dir + cam.CFrame.RightVector end
			if userInputService:IsKeyDown(Enum.KeyCode.Space) then dir = dir + Vector3.new(0, 1, 0) end
			if userInputService:IsKeyDown(Enum.KeyCode.LeftControl) then dir = dir - Vector3.new(0, 1, 0) end
			if dir.Magnitude > 0 then dir = dir.Unit end
			hrp.Velocity = Vector3.new(0, 0, 0)
			hrp.CFrame = hrp.CFrame + dir * sp
		end))
	end
	local function flyStop()
		if flyConn then flyConn:Disconnect() flyConn = nil end
	end
	task.spawn(LPH_NO_VIRTUALIZE(function()
		while true do
			task.wait(0.2)
			if lib.flags["fly"] and not flyConn then
				pcall(flyStart)
			elseif not lib.flags["fly"] and flyConn then
				flyStop()
			end
		end
	end))
	client.player.CharacterAdded:Connect(function()
		if lib.flags["fly"] then
			flyStop()
			task.wait(0.25)
			pcall(flyStart)
		end
	end)

	local hitNotifPlayers = {}
	local function hookTargetHealth(plr)
		if plr == client.player then return end
		local function hook(char)
			if not char then return end
			local hum = char:FindFirstChildOfClass("Humanoid")
			if not hum then return end
			local lastHp = hum.Health
			local conn
			conn = hum.HealthChanged:Connect(LPH_NO_VIRTUALIZE(function(hp)
				if not conn then return end
				if not lib.flags["hitnotifs"] then return end
				if not _G.__fhTarget or _G.__fhTarget ~= plr then return end
				if hp < lastHp then
					local dmg = math.floor((lastHp - hp) * 10 + 0.5) / 10
					if dmg > 0 then
						notify("damaged " .. plr.Name .. " for " .. tostring(dmg))
					end
				end
				lastHp = hp
			end))
			hitNotifPlayers[plr] = hitNotifPlayers[plr] or {}
			if hitNotifPlayers[plr].conn then hitNotifPlayers[plr].conn:Disconnect() end
			hitNotifPlayers[plr].conn = conn
			hitNotifPlayers[plr].hum = hum
		end
		if plr.Character then hook(plr.Character) end
		plr.CharacterAdded:Connect(function(ch)
			hitNotifPlayers[plr] = hitNotifPlayers[plr] or {}
			if hitNotifPlayers[plr].conn then hitNotifPlayers[plr].conn:Disconnect() end
			task.wait(0.5)
			hook(ch)
		end)
	end
	for _, plr in ipairs(playerService:GetPlayers()) do
		pcall(hookTargetHealth, plr)
	end
	playerService.PlayerAdded:Connect(function(plr)
		pcall(hookTargetHealth, plr)
	end)

	local hitSoundMap = {
		["Rust Headshot"]      = "rbxassetid://138750331387064",
		["Neverlose"]          = "rbxassetid://110168723447153",
		["Bubble"]             = "rbxassetid://6534947588",
		["Laser"]              = "rbxassetid://7837461331",
		["Steve"]              = "rbxassetid://4965083997",
		["Call of Duty"]       = "rbxassetid://5952120301",
		["Bat"]                = "rbxassetid://3333907347",
		["TF2 Critical"]       = "rbxassetid://296102734",
		["Saber"]              = "rbxassetid://8415678813",
		["Bameware"]           = "rbxassetid://3124331820",
		["Money"]              = "rbxassetid://13956013041",
		["Notif"]              = "rbxassetid://6696469190",
		["Shutter"]            = "rbxassetid://10066921516",
		["RIFK7"]              = "rbxassetid://9102080552",
		["LazerBeam"]          = "rbxassetid://130791043",
		["WindowsXPError"]     = "rbxassetid://160715357",
		["TF2Hitsound"]        = "rbxassetid://3455144981",
		["TF2Bat"]             = "rbxassetid://3333907347",
		["BowHit"]             = "rbxassetid://1053296915",
		["Bow"]                = "rbxassetid://3442683707",
		["OSU"]                = "rbxassetid://7147454322",
		["OneNN"]              = "rbxassetid://7349055654",
		["Rust"]               = "rbxassetid://6565371338",
		["TF2Pan"]             = "rbxassetid://3431749479",
		["Mario"]              = "rbxassetid://5709456554",
		["Bell"]               = "rbxassetid://6534947240",
		["Pick"]               = "rbxassetid://1347140027",
		["Pop"]                = "rbxassetid://198598793",
		["Sans"]               = "rbxassetid://3188795283",
		["Fart"]               = "rbxassetid://130833677",
		["Big"]                = "rbxassetid://5332005053",
		["Vine"]               = "rbxassetid://5332680810",
		["Bruh"]               = "rbxassetid://4578740568",
		["Skeet"]              = "rbxassetid://5633695679",
		["Fatality"]           = "rbxassetid://6534947869",
		["Bonk"]               = "rbxassetid://5766898159",
		["Minecraft"]          = "rbxassetid://5869422451",
		["Gamesense"]          = "rbxassetid://4817809188",
		["Bamboo"]             = "rbxassetid://3769434519",
		["Crowbar"]            = "rbxassetid://546410481",
		["Weeb"]               = "rbxassetid://6442965016",
		["Beep"]               = "rbxassetid://8177256015",
		["Bambi"]              = "rbxassetid://8437203821",
		["Stone"]              = "rbxassetid://3581383408",
		["Old Fatality"]       = "rbxassetid://6607142036",
		["Click"]              = "rbxassetid://8053704437",
		["Ding"]               = "rbxassetid://7149516994",
		["Snow"]               = "rbxassetid://6455527632",
		["Osu"]                = "rbxassetid://7149255551",
		["TF2"]                = "rbxassetid://2868331684",
		["Slime"]              = "rbxassetid://6916371803",
		["Among Us"]           = "rbxassetid://5700183626",
		["One"]                = "rbxassetid://7380502345",
		["BulletDeflect"]      = "rbxassetid://1657157666",
		["Default"]            = "rbxassetid://330595293",
		["UwU"]                = "rbxassetid://8679659744",
		["Cod"]                = "rbxassetid://160432334",
		["Blood SFX"]          = "rbxassetid://8164951181",
		["Blood Burst"]        = "rbxassetid://3781479909",
		["Blood Hit"]          = "rbxassetid://429400881",
	}

	local hsSound = Instance.new("Sound")
	hsSound.Volume = 1
	hsSound.Parent = game:GetService("SoundService")

	local hsNames = {}
	for name in pairs(hitSoundMap) do hsNames[#hsNames + 1] = name end
	table.sort(hsNames)

	local rageSounds = rage.createSection("extra")
		rageSounds.createToggle("hit sounds", false, "hs_enabled", function(state)
			notify(state and "hit sounds enabled" or "hit sounds disabled")
		end)
		rageSounds.createDropdown("sound", hsNames, "hs_sound", function() end)
		lib.flags["hs_sound"] = hsNames[1] or "Rust"
		rageSounds.createSlider("volume", 1, 1, 10, "", "hs_volume", function() end)
		rageSounds.createButton("test", function()
			local id = hitSoundMap[lib.flags["hs_sound"]] or hitSoundMap["Rust"]
			hsSound.SoundId = id
			hsSound.Volume = (lib.flags["hs_volume"] or 1) / 10
			hsSound:Play()
		end)
		rageSounds.createToggle("hit notifs", false, "hitnotifs", function(state)
			notify(state and "hit notifs enabled" or "hit notifs disabled")
			for _, row in pairs(_G.__hnRows or {}) do row.Visible = state end
		end)
		rageSounds.createSlider("lifetime", 2, 1, 10, "s", "hitnotif_lifetime", function() end)
		task.spawn(function()
			task.wait(0.5)
			_G.__hnRows = {}
			for _, tf in pairs(lib.tabframes or {}) do
				for _, v in pairs(tf:GetDescendants()) do
					if v:IsA("TextLabel") and v.Name == "uiSliderLabel" and v.Text:find("lifetime") then
						local row = v.Parent
						if row then
							table.insert(_G.__hnRows, row)
							if not lib.flags["hitnotifs"] then row.Visible = false end
						end
					end
				end
			end
		end)
		rageSounds.createToggle("underground", false, "underground", function(state)
			notify(state and "underground enabled" or "underground disabled")
			if _G.__ugToggle then _G.__ugToggle(state) end
		end)
		task.spawn(function()
			task.wait(0.5)
			for _, tf in pairs(lib.tabframes or {}) do
				for _, v in pairs(tf:GetDescendants()) do
					if v:IsA("TextLabel") and v.Name == "uiButtonLabel" and v.Text == "underground" then
						local row = v.Parent
						if row and row.Name == "uiSectionButton" then
							local ugPill = Instance.new("Frame")
							ugPill.Name = "ugKeybindPill"
							ugPill.Parent = row
							ugPill.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
							ugPill.BorderSizePixel = 0
							ugPill.Position = UDim2.new(0, 21, 0.5, -5)
							ugPill.Size = UDim2.new(0, 18, 0, 10)
							Instance.new("UICorner", ugPill).CornerRadius = UDim.new(0, 4)
							local ugPillStroke = Instance.new("UIStroke", ugPill)
							ugPillStroke.Color = Color3.fromRGB(53, 53, 53)
							ugPillStroke.Thickness = 1
							local ugPillLabel = Instance.new("TextLabel")
							ugPillLabel.Name = "ugPillLabel"
							ugPillLabel.Parent = ugPill
							ugPillLabel.BackgroundTransparency = 1
							ugPillLabel.Size = UDim2.new(1, 0, 1, 0)
							ugPillLabel.Font = Enum.Font.Arial
							ugPillLabel.Text = "none"
							ugPillLabel.TextColor3 = Color3.fromRGB(130, 130, 130)
							ugPillLabel.TextSize = 10
							ugPillLabel.TextStrokeTransparency = 0.5
							ugPill.InputBegan:Connect(function(input)
								if input.UserInputType == Enum.UserInputType.MouseButton1 then
									ugPillLabel.Text = "..."
									ugPillLabel.TextColor3 = lib.accent or Color3.fromRGB(218, 154, 169)
									local con
									con = userInputService.InputBegan:Connect(function(inp)
										if inp.UserInputType == Enum.UserInputType.Keyboard then
											_G.__ugKey = inp.KeyCode
											ugPillLabel.Text = inp.KeyCode.Name
											ugPillLabel.TextColor3 = Color3.fromRGB(208, 208, 208)
											con:Disconnect()
										end
									end)
								end
							end)
							_G.__ugKeyCon = userInputService.InputBegan:Connect(function(input)
								if input.UserInputType == Enum.UserInputType.Keyboard and _G.__ugKey and input.KeyCode == _G.__ugKey then
									if not lib.inDropdown and not lib.inColorPicker and not _G.__cfgTyping then
										lib.flags["underground"] = not lib.flags["underground"]
										if _G.__uiRefs and _G.__uiRefs["underground"] and _G.__uiRefs["underground"].set then
											pcall(function() _G.__uiRefs["underground"].set(lib.flags["underground"]) end)
										end
										notify(lib.flags["underground"] and "underground enabled" or "underground disabled")
										if _G.__ugToggle then _G.__ugToggle(lib.flags["underground"]) end
									end
								end
							end)
						end
					end
				end
			end
		end)

	local function playHitSound()
		if not lib.flags["hs_enabled"] then return end
		local id = hitSoundMap[lib.flags["hs_sound"]] or hitSoundMap["Rust"]
		if not id then return end
		hsSound.SoundId = id
		hsSound.Volume = (lib.flags["hs_volume"] or 1) / 10
		hsSound:Play()
	end
	_G.playHitSound = playHitSound

	local ugConn
	_G.__ugToggle = function(state)
		if state and not ugConn then
			ugConn = runService.RenderStepped:Connect(function()
				if not lib.flags["underground"] then
					ugConn:Disconnect()
					ugConn = nil
					return
				end
				local myChar = client.player.Character
				if myChar then
					local hrp = myChar:FindFirstChild("HumanoidRootPart")
					if hrp then
						local o = hrp.CFrame * CFrame.new(0, -11, 0) * CFrame.Angles(math.rad(90), 0, 0)
						local na = hrp.CFrame
						hrp.CFrame = o
						runService.RenderStepped:Wait()
						hrp.CFrame = na
					end
				end
			end)
		elseif not state and ugConn then
			ugConn:Disconnect()
			ugConn = nil
		end
	end

	task.spawn(function()
		task.wait(0.5)
		_G.__kbAntiStompRows = {}
		for _, tf in pairs(lib.tabframes or {}) do
			for _, v in pairs(tf:GetDescendants()) do
				if v:IsA("TextLabel") and v.Name == "uiSliderLabel" and v.Text:find("threshold") then
					local row = v.Parent
					if row then
						table.insert(_G.__kbAntiStompRows, row)
						if not lib.flags["antistomp"] then row.Visible = false end
					end
				end
			end
		end
	end)

	rageSounds.createToggle("spinbot", false, "spinbot", function(state)
		notify(state and "spinbot enabled" or "spinbot disabled")
		for _, row in pairs(_G.__spinbotRows or {}) do
			row.Visible = state
		end
	end)
	task.spawn(function()
		task.wait(0.5)
		for _, tf in pairs(lib.tabframes or {}) do
			for _, v in pairs(tf:GetDescendants()) do
				if v:IsA("TextLabel") and v.Name == "uiButtonLabel" and v.Text == "spinbot" then
					local row = v.Parent
					if row and row.Name == "uiSectionButton" then
						local sbPill = Instance.new("Frame")
						sbPill.Name = "spinbotKeybindPill"
						sbPill.Parent = row
						sbPill.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
						sbPill.BorderSizePixel = 0
						sbPill.Position = UDim2.new(0, 21, 0.5, -5)
						sbPill.Size = UDim2.new(0, 18, 0, 10)
						Instance.new("UICorner", sbPill).CornerRadius = UDim.new(0, 4)
						local sbPillStroke = Instance.new("UIStroke", sbPill)
						sbPillStroke.Color = Color3.fromRGB(53, 53, 53)
						sbPillStroke.Thickness = 1
						local sbPillLabel = Instance.new("TextLabel")
						sbPillLabel.Name = "sbPillLabel"
						sbPillLabel.Parent = sbPill
						sbPillLabel.BackgroundTransparency = 1
						sbPillLabel.Size = UDim2.new(1, 0, 1, 0)
						sbPillLabel.Font = Enum.Font.Arial
						sbPillLabel.Text = "none"
						sbPillLabel.TextColor3 = Color3.fromRGB(130, 130, 130)
						sbPillLabel.TextSize = 10
						sbPillLabel.TextStrokeTransparency = 0.5
						sbPill.InputBegan:Connect(function(input)
							if input.UserInputType == Enum.UserInputType.MouseButton1 then
								sbPillLabel.Text = "..."
								sbPillLabel.TextColor3 = lib.accent or Color3.fromRGB(218, 154, 169)
								local con
								con = userInputService.InputBegan:Connect(function(inp)
									if inp.UserInputType == Enum.UserInputType.Keyboard then
										_G.__spinbotKey = inp.KeyCode
										sbPillLabel.Text = inp.KeyCode.Name
										sbPillLabel.TextColor3 = Color3.fromRGB(208, 208, 208)
										con:Disconnect()
									end
								end)
							end
						end)
						_G.__spinbotKeyCon = userInputService.InputBegan:Connect(function(input)
							if input.UserInputType == Enum.UserInputType.Keyboard and _G.__spinbotKey and input.KeyCode == _G.__spinbotKey then
								if not lib.inDropdown and not lib.inColorPicker and not _G.__cfgTyping then
									lib.flags["spinbot"] = not lib.flags["spinbot"]
									if _G.__uiRefs and _G.__uiRefs["spinbot"] and _G.__uiRefs["spinbot"].set then
										pcall(function() _G.__uiRefs["spinbot"].set(lib.flags["spinbot"]) end)
									end
									notify(lib.flags["spinbot"] and "spinbot enabled" or "spinbot disabled")
									for _, row in pairs(_G.__spinbotRows or {}) do
										row.Visible = lib.flags["spinbot"]
									end
								end
							end
						end)
						v.Position = UDim2.new(0, 42, 0, 0)
						v.Text = "spinbot"
						break
					end
				end
			end
		end
	end)
	rageSounds.createSlider("intensity", 50, 1, 200, "", "spin_intensity", function() end)
	rageSounds.createDropdown("method", {"anti aim", "jitter", "spin"}, "spin_method", function() end)
	lib.flags["spin_method"] = "spin"
	task.defer(function()
		_G.__spinbotRows = {}
		local toggleFrame
		for _, v in pairs(game.CoreGui:GetDescendants()) do
			if v:IsA("TextLabel") and v.Text == "spinbot" then
				toggleFrame = v.Parent
				break
			end
		end
		if toggleFrame and toggleFrame.Parent then
			local children = toggleFrame.Parent:GetChildren()
			local foundToggle = false
			for _, child in pairs(children) do
				if child == toggleFrame then
					foundToggle = true
				elseif foundToggle then
					if child.Name == "uiSectionButton" then
						break
					elseif child.Name == "uiSectionDropdown" or child.Name == "uiSectionSlider" then
						table.insert(_G.__spinbotRows, child)
					end
				end
			end
			for _, row in pairs(_G.__spinbotRows) do
				row.Visible = false
			end
		end
	end)

local settings = window.createTab("settings", "rbxassetid://8595329857")
	local ui = settings.createSection("ui")
		local watermark = ui.createColorpicker("watermark", Color3.fromRGB(255,255,255), true, "watermark", function(clr3, trans, bool)
			watermarkui.Enabled = bool
			sessionSettings["watermark"] = {clr3.r*255, clr3.g*255, clr3.b*255}
			lib.flags["watermark"] = {clr3.r*255, clr3.g*255, clr3.b*255}
			sessionSettings["watermark2"] = bool
			if type(lib.flags["watermark"]) == "table" then
				watermarkLabel.TextColor3 = Color3.fromRGB(unpack(lib.flags["watermark"]))
			else
				watermarkLabel.TextColor3 = lib.flags["watermark"]
			end
		end)
		local watermarktext = ui.createDropdown("watermark name", {"v3nom.cc"}, "watermarktext", function(str)
			sessionSettings["watermarktext"] = str
			if lib.flags["watermarktext"] ~= "none" then
				watermarkLabel.Text = lib.flags["watermarktext"].." | "..fps.." fps | "..tostring(math.floor(client.player:GetNetworkPing()*2000)).." ping"
			else
				watermarkLabel.Text = fps.." fps | "..tostring(math.floor(client.player:GetNetworkPing()*2000)).." ping"
			end
		end)
		ui.createButton(lib.togglekey.Name, function()
			if _G.__keyCon then _G.__keyCon:Disconnect() end
			local oldKeyName = lib.togglekey.Name
			_G.__keyCon = userInputService.InputBegan:Connect(function(input)
				if input.UserInputType == Enum.UserInputType.Keyboard then
					lib.setToggleKey(input.KeyCode)
					for _, tf in pairs(lib.tabframes or {}) do
						for _, v in pairs(tf:GetDescendants()) do
							if v:IsA("TextLabel") and v.Name == "uiButtonLabel" and v.Text == oldKeyName then
								v.Text = input.KeyCode.Name
							end
						end
					end
					_G.__keyCon:Disconnect(); _G.__keyCon = nil
				end
			end)
		end)
		ui.createDropdown("position", {"left", "right", "middle"}, "ui_position", function(str)
			if str == "left" then
				__notifAlign = "left"
			elseif str == "right" then
				__notifAlign = "right"
			elseif str == "middle" then
				__notifAlign = "center"
			end
			notify(str .. " selected")
		end)
		ui.createButton("unload", function()
			_G.__auraCon = _G.__auraCon and pcall(function() _G.__auraCon:Disconnect() end)
			_G.__keyCon = _G.__keyCon and pcall(function() _G.__keyCon:Disconnect() end)
			_G.__fhConn = _G.__fhConn and pcall(function() _G.__fhConn:Disconnect() end)
			_G.__auraRunning = false
			_G.__fhTarget = nil
			if _G.__fhHighlight then pcall(function() _G.__fhHighlight:Destroy() end) end
			if _G.__fhLine then pcall(function() _G.__fhLine:Remove() end) end
			if fhLineOutline then pcall(function() fhLineOutline:Remove() end) end
			if _G.__fhToggleCon then pcall(function() _G.__fhToggleCon:Disconnect() end) end
			for _, gui in pairs(game.CoreGui:GetChildren()) do
				if gui:IsA("ScreenGui") then
					for _, v in pairs(gui:GetDescendants()) do
						if v:IsA("Frame") and v.Name == "uiBack" then
							gui:Destroy()
							break
						end
					end
				end
			end
			if __notifGui then pcall(function() __notifGui:Destroy() end) end
			if kblistGui then pcall(function() kblistGui:Destroy() end) end
			if radarGui then pcall(function() radarGui:Destroy() end) end
			if keystrokeGui then pcall(function() keystrokeGui:Destroy() end) end
			if _G.__autoKnifeCon then pcall(function() _G.__autoKnifeCon:Disconnect() end) end
			if _G.spyGui then pcall(function() _G.spyGui:Destroy() end) end
		end)
	local extra = settings.createSection("extra")
		extra.createToggle("keybind list", false, "kbl_enabled", function(state)
			notify(state and "keybind list enabled" or "keybind list disabled")
		end)
		extra.createToggle("radar", false, "radar_enabled", function(state)
			radarGui.Enabled = state
			notify(state and "radar enabled" or "radar disabled")
		end)
		extra.createToggle("keystrokes", false, "ks_enabled", function(state)
			keystrokeGui.Enabled = state
			notify(state and "keystrokes enabled" or "keystrokes disabled")
		end)
		extra.createToggle("chat spy", false, "chatspy_enabled", function(state)
			notify(state and "chat spy enabled" or "chat spy disabled")
		end)
	local theme = settings.createSection("theme")
		local uiaccent = theme.createColorpicker("ui accent", Color3.fromRGB(218, 154, 169), false, "uiaccent", function(clr3, trans)
			sessionSettings["uiaccent"] = {clr3.r*255, clr3.g*255, clr3.b*255}
			watermarkLine.ImageColor3 = Color3.fromRGB(unpack({clr3.r*255, clr3.g*255, clr3.b*255}))
			lib.setAccent(Color3.fromRGB(unpack({clr3.r*255, clr3.g*255, clr3.b*255})))
			local clr = Color3.fromRGB(math.floor(clr3.R*255), math.floor(clr3.G*255), math.floor(clr3.B*255))
			radarLine.BackgroundColor3 = clr
			ksLine.BackgroundColor3 = clr
			if _G.spyLine then _G.spyLine.BackgroundColor3 = clr end
			if kblistLine then kblistLine.BackgroundColor3 = clr end
			if _G.__fhSetActive then
				if mainGlow.BackgroundTransparency < 1 then _G.__fhSetActive(mainSub, mainLine, mainGlow, mainTitle, mainSubLbl, true) end
				if themeGlow.BackgroundTransparency < 1 then _G.__fhSetActive(themeSub, themeLine, themeGlow, themeTitle, themeSubLbl, true) end
			end
		end)
		theme.createColorpicker("page background", Color3.fromRGB(35, 35, 35), false, "theme_bg", function(clr)
			sessionSettings["theme_bg"] = {clr.R*255, clr.G*255, clr.B*255}
			for _, gui in pairs(game.CoreGui:GetChildren()) do
				if gui:IsA("ScreenGui") then
					local back = gui:FindFirstChild("uiBack", true)
					if back then back.BackgroundColor3 = clr; break end
				end
			end
			if _G.kblistBack then _G.kblistBack.BackgroundColor3 = clr end
			if radarBack then radarBack.BackgroundColor3 = clr end
			if _G.spyBack then _G.spyBack.BackgroundColor3 = clr end
		end)
		theme.createColorpicker("section background", Color3.fromRGB(43, 43, 43), false, "theme_sec", function(clr)
			sessionSettings["theme_sec"] = {clr.R*255, clr.G*255, clr.B*255}
			for _, gui in pairs(game.CoreGui:GetChildren()) do
				if gui:IsA("ScreenGui") then
					local found = false
					for _, s in pairs(gui:GetDescendants()) do
						if s:IsA("Frame") and s.Name == "uiTabSectionIn" then s.BackgroundColor3 = clr; found = true end
					end
					if found then break end
				end
			end
		end)
		theme.createColorpicker("text", Color3.fromRGB(208, 208, 208), false, "theme_text", function(clr)
			sessionSettings["theme_text"] = {clr.R*255, clr.G*255, clr.B*255}
			for _, gui in pairs(game.CoreGui:GetChildren()) do
				if gui:IsA("ScreenGui") then
					local found = false
					for _, s in pairs(gui:GetDescendants()) do
						if s:IsA("TextLabel") and (s.Name == "uiButtonLabel" or s.Name == "uiSliderLabel" or s.Name == "uiDropdownLabel" or s.Name == "uiColorLabel" or s.Name == "uiSliderSelectionsLabel") then s.TextColor3 = clr; found = true end
					end
					if found then break end
				end
			end
			if _G.kblistTitle then _G.kblistTitle.TextColor3 = clr end
			if _G.spyTitle then _G.spyTitle.TextColor3 = clr end
			if _G.spyHolder then
				for _, ch in pairs(_G.spyHolder:GetChildren()) do
					if ch:IsA("TextLabel") then ch.TextColor3 = clr end
				end
			end
		end)
		theme.createColorpicker("outline text", Color3.fromRGB(14, 14, 14), false, "theme_otext", function(clr)
			sessionSettings["theme_otext"] = {clr.R*255, clr.G*255, clr.B*255}
			for _, gui in pairs(game.CoreGui:GetChildren()) do
				if gui:IsA("ScreenGui") then
					local found = false
					for _, s in pairs(gui:GetDescendants()) do
						if s:IsA("TextLabel") and (s.Name == "uiButtonLabel" or s.Name == "uiSliderLabel" or s.Name == "uiDropdownLabel" or s.Name == "uiColorLabel" or s.Name == "uiSliderSelectionsLabel") then s.TextStrokeColor3 = clr; found = true end
					end
					if found then break end
				end
			end
			if _G.kblistTitle then _G.kblistTitle.TextStrokeColor3 = clr end
			if _G.spyTitle then _G.spyTitle.TextStrokeColor3 = clr end
		end)
		theme.createColorpicker("outline", Color3.fromRGB(27, 22, 20), false, "theme_outline", function(clr)
			sessionSettings["theme_outline"] = {clr.R*255, clr.G*255, clr.B*255}
			if radarStroke then radarStroke.Color = clr end
			if _G.kblistStroke then _G.kblistStroke.Color = clr end
			if _G.spyStroke then _G.spyStroke.Color = clr end
			if ksStroke then ksStroke.Color = clr end
			for _, gui in pairs(game.CoreGui:GetChildren()) do
				if gui:IsA("ScreenGui") then
					for _, s in pairs(gui:GetDescendants()) do
						if s:IsA("Frame") and s.Name == "uiTabSection" then s.BackgroundColor3 = clr end
						if s:IsA("Frame") and s.Name == "uiBorder1" then s.BackgroundColor3 = clr end
					end
				end
			end
		end)
		theme.createColorpicker("top bar", Color3.fromRGB(53, 52, 51), false, "theme_topbar", function(clr)
			sessionSettings["theme_topbar"] = {clr.R*255, clr.G*255, clr.B*255}
			for _, gui in pairs(game.CoreGui:GetChildren()) do
				if gui:IsA("ScreenGui") then
					local tb = gui:FindFirstChild("uiTop", true)
					if tb then tb.BackgroundColor3 = clr; break end
				end
			end
		end)
		theme.createColorpicker("bottom bar", Color3.fromRGB(53, 52, 51), false, "theme_botbar", function(clr)
			sessionSettings["theme_botbar"] = {clr.R*255, clr.G*255, clr.B*255}
			for _, gui in pairs(game.CoreGui:GetChildren()) do
				if gui:IsA("ScreenGui") then
					local bb = gui:FindFirstChild("uiBottom", true)
					if bb then bb.BackgroundColor3 = clr; break end
				end
			end
		end)
		theme.createColorpicker("sidebar", Color3.fromRGB(42, 42, 42), false, "theme_sidebar", function(clr)
			sessionSettings["theme_sidebar"] = {clr.R*255, clr.G*255, clr.B*255}
			for _, gui in pairs(game.CoreGui:GetChildren()) do
				if gui:IsA("ScreenGui") then
					local sb = gui:FindFirstChild("uiSidebar", true)
					if sb then sb.BackgroundColor3 = clr; break end
				end
			end
		end)
	local configs = settings.createSection("configs")
		configs.createDropdown("configs", {}, "cfg_select", function() end)
		local cfgTextbox = configs.createButton("config name", function() end)
		_G.__cfgNameInput = _G.__cfgNameInput or ""
		_G.__cfgTyping = _G.__cfgTyping or false
		_G.__cfgBtnRef = _G.__cfgBtnRef or nil
		_G.__cfgClicked = _G.__cfgClicked or false
		local cfgFolder = "v3nom.cc"
		if not isfolder(cfgFolder) then pcall(makefolder, cfgFolder) end
		configs.createButton("save", function()
			local cfgName = _G.__cfgNameInput ~= "" and _G.__cfgNameInput or (lib.flags["cfg_select"] or "")
			if cfgName == "" or cfgName == "none" then notify("type a config name first") return end
			local data = {}
			data.flags = {}
			for k, v in pairs(lib.flags) do
				if typeof(v) == "Color3" then
					data.flags[k] = {math.floor(v.R*255), math.floor(v.G*255), math.floor(v.B*255), "c3"}
				elseif typeof(v) == "EnumItem" then
					data.flags[k] = {v.Name, v.EnumType.Name, "enum"}
				elseif type(v) == "table" then
					data.flags[k] = {v, "tbl"}
				elseif type(v) == "boolean" or type(v) == "number" or type(v) == "string" then
					data.flags[k] = {v, "raw"}
				end
			end
			if lib.accent then data.accent = {lib.accent.R*255, lib.accent.G*255, lib.accent.B*255} end
			data.togglekey = lib.togglekey and lib.togglekey.Name or "Insert"
			data.keybinds = {}
			if _G.__forcehitKey then data.keybinds.fh_key = _G.__forcehitKey.Name end
			if _G.__godmodeKey then data.keybinds.gm_key = _G.__godmodeKey.Name end
			if _G.__flyKey then data.keybinds.fly_key = _G.__flyKey.Name end
			if _G.__ugKey then data.keybinds.ug_key = _G.__ugKey.Name end
			local encOk, encoded = pcall(httpService.JSONEncode, httpService, data)
			if not encOk then notify("config encode failed") return end
			if not isfolder(cfgFolder) then pcall(makefolder, cfgFolder) end
			writefile(cfgFolder .. "/" .. cfgName .. ".cfg", encoded)
			lib.flags["cfg_select"] = cfgName
			refreshCfgList()
			notify("config saved")
		end)
		configs.createButton("load", function()
			local cfgName = lib.flags["cfg_select"] or ""
			if cfgName == "" or cfgName == "none" then return end
			local filePath = cfgFolder .. "/" .. cfgName .. ".cfg"
			if not isfile(filePath) then notify("config file not found") return end
			local readOk, readResult = pcall(readfile, filePath)
			if not readOk or not readResult then notify("failed to read config") return end
			local ok, data = pcall(httpService.JSONDecode, httpService, readResult)
			if not ok or not data then notify("config decode failed") return end
			if data.accent then
				pcall(function() lib.setAccent(Color3.fromRGB(unpack(data.accent))) end)
			end
			if data.togglekey then
				pcall(function() lib.setToggleKey(Enum.KeyCode[data.togglekey]) end)
			end
			if data.keybinds then
			if data.keybinds.fh_key then pcall(function() _G.__forcehitKey = Enum.KeyCode[data.keybinds.fh_key] end) end
			if data.keybinds.gm_key then pcall(function() _G.__godmodeKey = Enum.KeyCode[data.keybinds.gm_key] end) end
			if data.keybinds.fly_key then pcall(function() _G.__flyKey = Enum.KeyCode[data.keybinds.fly_key] end) end
			if data.keybinds.ug_key then pcall(function() _G.__ugKey = Enum.KeyCode[data.keybinds.ug_key] end) end
			end
			if data.flags then
				for k, v in pairs(data.flags) do
					if type(v) == "table" and #v >= 2 then
						local typ = v[#v]
						if typ == "c3" then
							lib.flags[k] = Color3.fromRGB(v[1], v[2], v[3])
						elseif typ == "enum" then
							pcall(function() lib.flags[k] = Enum[v[2]][v[1]] end)
						elseif typ == "tbl" then
							lib.flags[k] = v[1]
						elseif typ == "raw" then
							lib.flags[k] = v[1]
						end
						if _G.__uiRefs and _G.__uiRefs[k] and _G.__uiRefs[k].set then
							pcall(function()
								if typ == "c3" then
									_G.__uiRefs[k].set({v[1], v[2], v[3]}, -1, false)
								elseif typ == "raw" then
									_G.__uiRefs[k].set(v[1])
								end
							end)
						end
					end
				end
			end
			if data.flags then
				for _, gui in pairs(game.CoreGui:GetChildren()) do
					if gui:IsA("ScreenGui") then
						local back = gui:FindFirstChild("uiBack", true)
						if back then
							if data.flags["theme_bg"] and type(data.flags["theme_bg"]) == "table" and data.flags["theme_bg"][#data.flags["theme_bg"]] == "c3" then
								pcall(function() back.BackgroundColor3 = Color3.fromRGB(unpack(data.flags["theme_bg"])) end)
							end
							if data.flags["theme_sec"] and type(data.flags["theme_sec"]) == "table" and data.flags["theme_sec"][#data.flags["theme_sec"]] == "c3" then
								for _, s in pairs(gui:GetDescendants()) do
									if s:IsA("Frame") and s.Name == "uiTabSectionIn" then pcall(function() s.BackgroundColor3 = Color3.fromRGB(unpack(data.flags["theme_sec"])) end) end
								end
							end
							if data.flags["theme_text"] and type(data.flags["theme_text"]) == "table" and data.flags["theme_text"][#data.flags["theme_text"]] == "c3" then
								for _, s in pairs(gui:GetDescendants()) do
									if s:IsA("TextLabel") and (s.Name == "uiButtonLabel" or s.Name == "uiSliderLabel" or s.Name == "uiDropdownLabel" or s.Name == "uiColorLabel" or s.Name == "uiSliderSelectionsLabel") then pcall(function() s.TextColor3 = Color3.fromRGB(unpack(data.flags["theme_text"])) end) end
								end
							end
							if data.flags["theme_otext"] and type(data.flags["theme_otext"]) == "table" and data.flags["theme_otext"][#data.flags["theme_otext"]] == "c3" then
								for _, s in pairs(gui:GetDescendants()) do
									if s:IsA("TextLabel") and (s.Name == "uiButtonLabel" or s.Name == "uiSliderLabel" or s.Name == "uiDropdownLabel" or s.Name == "uiColorLabel" or s.Name == "uiSliderSelectionsLabel") then pcall(function() s.TextStrokeColor3 = Color3.fromRGB(unpack(data.flags["theme_otext"])) end) end
								end
							end
							if data.flags["theme_topbar"] and type(data.flags["theme_topbar"]) == "table" and data.flags["theme_topbar"][#data.flags["theme_topbar"]] == "c3" then
								local tb = gui:FindFirstChild("uiTop", true)
								if tb then pcall(function() tb.BackgroundColor3 = Color3.fromRGB(unpack(data.flags["theme_topbar"])) end) end
							end
							if data.flags["theme_botbar"] and type(data.flags["theme_botbar"]) == "table" and data.flags["theme_botbar"][#data.flags["theme_botbar"]] == "c3" then
								local bb = gui:FindFirstChild("uiBottom", true)
								if bb then pcall(function() bb.BackgroundColor3 = Color3.fromRGB(unpack(data.flags["theme_botbar"])) end) end
							end
							if data.flags["theme_sidebar"] and type(data.flags["theme_sidebar"]) == "table" and data.flags["theme_sidebar"][#data.flags["theme_sidebar"]] == "c3" then
								local sb = gui:FindFirstChild("uiSidebar", true)
								if sb then pcall(function() sb.BackgroundColor3 = Color3.fromRGB(unpack(data.flags["theme_sidebar"])) end) end
							end
							break
						end
					end
				end
			end
			lib.flags["cfg_select"] = cfgName
			notify("config loaded")
		end)
		configs.createButton("delete", function()
			local cfgName = lib.flags["cfg_select"] or ""
			if cfgName == "" or cfgName == "none" then return end
			local filePath = cfgFolder .. "/" .. cfgName .. ".cfg"
			if isfile(filePath) then pcall(delfile, filePath) end
			lib.flags["cfg_select"] = "none"
			refreshCfgList()
			notify("config deleted")
		end)

task.spawn(function()
	task.wait(0.5)
	for _, tf in pairs(lib.tabframes or {}) do
		for _, v in pairs(tf:GetDescendants()) do
			if v:IsA("TextLabel") and v.Name == "uiButtonLabel" and v.Text == "config name" then
				_G.__cfgBtnRef = v
				v.Text = "click to type name"
				v.TextColor3 = Color3.fromRGB(130, 130, 130)
				v.InputBegan:Connect(function(input)
					if input.UserInputType == Enum.UserInputType.MouseButton1 and not _G.__cfgClicked then
						_G.__cfgClicked = true
						_G.__cfgTyping = true
						_G.__cfgNameInput = ""
						v.Text = "|"
						v.TextColor3 = Color3.fromRGB(208, 208, 208)
					end
				end)
				break
			end
		end
	end
end)
userInputService.InputBegan:Connect(function(input, gpe)
	if gpe or not _G.__cfgTyping or not _G.__cfgBtnRef then return end
	if input.UserInputType == Enum.UserInputType.Keyboard then
		local key = input.KeyCode
		if key == Enum.KeyCode.Return or key == Enum.KeyCode.KeypadEnter then
			_G.__cfgTyping = false
			_G.__cfgClicked = false
			if _G.__cfgNameInput == "" then
				_G.__cfgBtnRef.Text = "click to type name"
				_G.__cfgBtnRef.TextColor3 = Color3.fromRGB(130, 130, 130)
			else
				_G.__cfgBtnRef.Text = _G.__cfgNameInput
			end
		elseif key == Enum.KeyCode.Escape then
			_G.__cfgTyping = false
			_G.__cfgClicked = false
			_G.__cfgNameInput = ""
			_G.__cfgBtnRef.Text = "click to type name"
			_G.__cfgBtnRef.TextColor3 = Color3.fromRGB(130, 130, 130)
		elseif key == Enum.KeyCode.Backspace then
			_G.__cfgNameInput = string.sub(_G.__cfgNameInput, 1, -2)
			_G.__cfgBtnRef.Text = _G.__cfgNameInput .. "|"
		else
			local ok, char = pcall(string.char, input.KeyCode.Value)
			if ok and char and char:match("[%w_%-%. ]") then
				_G.__cfgNameInput = _G.__cfgNameInput .. char
				_G.__cfgBtnRef.Text = _G.__cfgNameInput .. "|"
			end
		end
	end
end)

function refreshCfgList()
	local names = {}
	local ok, files = pcall(listfiles, "v3nom.cc")
	if ok and type(files) == "table" then
		for _, f in pairs(files) do
			local fname = tostring(f)
			local base = fname:match("([^\\/]+)$") or fname
			if base:sub(-4) == ".cfg" then
				table.insert(names, base:sub(1, -5))
			end
		end
	end
	if #names == 0 then table.insert(names, "none") end
	for _, tf in pairs(lib.tabframes or {}) do
		for _, v in pairs(tf:GetDescendants()) do
			if v:IsA("TextLabel") and v.Text == "configs" and v.Name == "uiDropdownLabel" then
				local dropOutline = v.Parent and v.Parent:FindFirstChild("uiDropdownOutline")
				local dropBack = dropOutline and dropOutline:FindFirstChild("uiDropdownBack")
				if dropBack then
					local sel = dropBack:FindFirstChild("uiSliderSelectionsLabel")
					if sel then sel.Text = lib.flags["cfg_select"] or "none" end
					local drop2 = dropBack:FindFirstChild("uiDropdownBack2")
					if drop2 then
						for _, ch in pairs(drop2:GetChildren()) do
							if ch:IsA("TextLabel") then ch:Destroy() end
						end
						local sz = 0
						for i, name in pairs(names) do
							sz = sz + 17
							local lbl = Instance.new("TextLabel")
							lbl.Name = "uiSliderSelection"
							lbl.Parent = drop2
							lbl.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
							lbl.BackgroundTransparency = 1
							lbl.Position = UDim2.new(0, 4, 0, 0)
							lbl.Size = UDim2.new(1, -8, 0, 17)
							lbl.ZIndex = 5
							lbl.Font = Enum.Font.Arial
							lbl.Text = name
							lbl.TextColor3 = Color3.fromRGB(208, 208, 208)
							lbl.TextSize = 11
							lbl.TextStrokeTransparency = 0.35
							lbl.TextWrapped = true
							lbl.TextXAlignment = Enum.TextXAlignment.Left
							if lib.accentItems then table.insert(lib.accentItems, lbl) end
							lbl.InputBegan:Connect(function(inp)
								if inp.UserInputType == Enum.UserInputType.MouseButton1 then
									lib.flags["cfg_select"] = name
									sel.Text = name
									for _, other in pairs(drop2:GetChildren()) do
										if other:IsA("TextLabel") then
											if other == lbl then
												other.TextColor3 = lib.accent
											else
												other.TextColor3 = Color3.fromRGB(208, 208, 208)
											end
										end
									end
									drop2.Visible = false
									_G.__cfgDropOpen = false
									_G.__cfgDropClosing = false
									lib.inDropdown = false
								end
							end)
						end
						drop2.Size = UDim2.new(1, -2, 0, sz)
						_G.__cfgDropSizes = _G.__cfgDropSizes or {}
						_G.__cfgDropSizes["cfg_select"] = sz
					end
				end
				break
			end
		end
	end
end

task.spawn(function() task.wait(1); refreshCfgList() end)

task.spawn(function()
	task.wait(0.5)
	local function recalcAllTabs()
		for _, tab in pairs(lib.tabframes or {}) do
			local maxY = 0
			for _, s in pairs(tab:GetDescendants()) do
				if s:IsA("Frame") and s.Visible then
					local absPos = s.AbsolutePosition.Y
					local absSize = s.AbsoluteSize.Y
					local tabAbsPos = tab.AbsolutePosition.Y
					local relBottom = (absPos - tabAbsPos) + absSize + tab.CanvasPosition.Y
					if relBottom > maxY then maxY = relBottom end
				end
			end
			local minCanvas = tab.AbsoluteSize.Y + 50
			if maxY < minCanvas then maxY = minCanvas end
			tab.CanvasSize = UDim2.new(0, 0, 0, maxY + 40)
			tab.ClipsDescendants = true
		end
	end
	recalcAllTabs()
	task.spawn(LPH_NO_VIRTUALIZE(function()
		while true do
			task.wait(0.5)
			pcall(recalcAllTabs)
		end
	end))
	task.spawn(function()
		for _, plr in pairs(game.CoreGui:GetChildren()) do
			if plr:IsA("ScreenGui") then
				for _, v in pairs(plr:GetDescendants()) do
					if v:IsA("Frame") and v.Name == "uiBottom" then
						v.ZIndex = 10
					end
				end
			end
		end
	end)
	task.spawn(function()
		task.wait(1)
		local uiSidebar = nil
		for _, gui in pairs(game.CoreGui:GetChildren()) do
			if gui:IsA("ScreenGui") then
				uiSidebar = gui:FindFirstChild("uiSidebar", true)
				if uiSidebar then break end
			end
		end
		if not uiSidebar then return end

		local mainBtn = uiSidebar:FindFirstChild("uiSidebarMainBtn")

		local sbY = 0

		local function makeSidebarBtn(name, title, subtitle, posY, parent)
			local btn = Instance.new("TextButton")
			btn.Name = name
			btn.Parent = parent
			btn.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			btn.BackgroundTransparency = 1
			btn.BorderSizePixel = 0
			btn.Position = UDim2.new(0, 0, 0, posY)
			btn.Size = UDim2.new(1, 0, 0, 50)
			btn.Text = ""
			btn.ZIndex = 10

			local line = Instance.new("Frame")
			line.Name = "navLine"
			line.Parent = btn
			line.BackgroundColor3 = lib.accent or Color3.fromRGB(218, 154, 169)
			line.BorderSizePixel = 0
			line.Position = UDim2.new(0, 0, 0, 4)
			line.Size = UDim2.new(0, 2, 1, -8)
			line.BackgroundTransparency = 1
			line.ZIndex = 11

			local glow = Instance.new("Frame")
			glow.Name = "navGlow"
			glow.Parent = btn
			glow.BackgroundColor3 = lib.accent or Color3.fromRGB(218, 154, 169)
			glow.BorderSizePixel = 0
			glow.Position = UDim2.new(0, 2, 0, 4)
			glow.Size = UDim2.new(0, 25, 1, -8)
			glow.BackgroundTransparency = 1
			glow.ZIndex = 11
			local grad = Instance.new("UIGradient")
			grad.Parent = glow
			grad.Transparency = NumberSequence.new({NumberSequenceKeypoint.new(0, 0.65), NumberSequenceKeypoint.new(1, 1)})

			local titleLabel = Instance.new("TextLabel")
			titleLabel.Name = "navTitle"
			titleLabel.Parent = btn
			titleLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			titleLabel.BackgroundTransparency = 1
			titleLabel.Position = UDim2.new(0, 12, 0, 6)
			titleLabel.Size = UDim2.new(1, -18, 0, 20)
			titleLabel.Font = Enum.Font.ArialBold
			titleLabel.Text = title
			titleLabel.TextColor3 = Color3.fromRGB(182, 182, 182)
			titleLabel.TextSize = 16
			titleLabel.TextXAlignment = Enum.TextXAlignment.Left
			titleLabel.ZIndex = 11

			local subLabel = Instance.new("TextLabel")
			subLabel.Name = "navSub"
			subLabel.Parent = btn
			subLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			subLabel.BackgroundTransparency = 1
			subLabel.Position = UDim2.new(0, 12, 0, 26)
			subLabel.Size = UDim2.new(1, -18, 0, 16)
			subLabel.Font = Enum.Font.Arial
			subLabel.Text = subtitle
			subLabel.TextColor3 = Color3.fromRGB(182, 182, 182)
			subLabel.TextSize = 12
			subLabel.TextXAlignment = Enum.TextXAlignment.Left
			subLabel.ZIndex = 11

			return btn, line, glow, titleLabel, subLabel
		end

		local navDivider = Instance.new("Frame")
		navDivider.Parent = uiSidebar
		navDivider.Size = UDim2.new(1, -20, 0, 1)
		navDivider.Position = UDim2.new(0, 10, 0, sbY + 2)
		navDivider.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
		navDivider.BorderSizePixel = 0
		navDivider.ZIndex = 10
		navDivider.Visible = false

		local mainSub, mainLine, mainGlow, mainTitle, mainSubLbl = makeSidebarBtn("settingsMainBtn", "Main", "settings", sbY + 8, uiSidebar)
		local themeSub, themeLine, themeGlow, themeTitle, themeSubLbl = makeSidebarBtn("settingsThemeBtn", "Theme", "colors", sbY + 58, uiSidebar)
		mainSub.Visible = false
		themeSub.Visible = false

		local function setActive(btn, line, glow, titleLabel, subLabel, accent)
			local c = lib.accent or Color3.fromRGB(218, 154, 169)
			if accent then
				line.BackgroundTransparency = 0
				line.BackgroundColor3 = c
				glow.BackgroundTransparency = 0
				glow.BackgroundColor3 = c
				titleLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
				subLabel.TextColor3 = c
			else
				line.BackgroundTransparency = 1
				glow.BackgroundTransparency = 1
				titleLabel.TextColor3 = Color3.fromRGB(182, 182, 182)
				subLabel.TextColor3 = Color3.fromRGB(182, 182, 182)
			end
		end

		_G.__fhSetActive = setActive
		_G.__fhMainNav = {mainLine, mainGlow, mainTitle, mainSubLbl}
		_G.__fhThemeNav = {themeLine, themeGlow, themeTitle, themeSubLbl}

		local settingsTab = lib.tabframes and lib.tabframes[#lib.tabframes]
		if not settingsTab then return end

		local sections = {}
		for _, child in pairs(settingsTab:GetChildren()) do
			if child:IsA("Frame") and child.Name == "uiTabSection" then
				table.insert(sections, child)
			end
		end

		local function recalcCanvas()
			local maxY = 0
			for _, s in pairs(settingsTab:GetChildren()) do
				if s:IsA("Frame") and s.Name == "uiTabSection" and s.Visible then
					local bottom = s.Position.Y.Offset + s.Size.Y.Offset
					if bottom > maxY then maxY = bottom end
				end
			end
			settingsTab.CanvasSize = UDim2.new(0, 0, 0, maxY + 20)
		end

		local function showMain()
			local sH = 182
			if sections[1] then
				sections[1].Visible = true
				sections[1].Size = UDim2.new(0, sH, 0, sections[1].Size.Y.Offset)
				sections[1].Position = UDim2.new(0, 5, 0, 5)
			end
			if sections[2] then
				sections[2].Visible = true
				sections[2].Size = UDim2.new(0, sH, 0, sections[2].Size.Y.Offset)
				sections[2].Position = UDim2.new(0, sH + 10, 0, 5)
			end
			if sections[3] then sections[3].Visible = false end
			if sections[4] then
				sections[4].Visible = true
				sections[4].Size = UDim2.new(0, sH, 0, sections[4].Size.Y.Offset)
				if sections[2] then
					sections[4].Position = UDim2.new(0, sH + 10, 0, sections[2].Position.Y.Offset + sections[2].Size.Y.Offset + 5)
				else
					sections[4].Position = UDim2.new(0, sH + 10, 0, 5)
				end
			end
			setActive(mainSub, mainLine, mainGlow, mainTitle, mainSubLbl, true)
			setActive(themeSub, themeLine, themeGlow, themeTitle, themeSubLbl, false)
			recalcCanvas()
		end

		local function showTheme()
			if sections[1] then sections[1].Visible = false end
			if sections[2] then sections[2].Visible = false end
			if sections[3] then sections[3].Visible = true; sections[3].Position = UDim2.new(0, 0, 0, 5) end
			if sections[4] then sections[4].Visible = false end
			setActive(themeSub, themeLine, themeGlow, themeTitle, themeSubLbl, true)
			setActive(mainSub, mainLine, mainGlow, mainTitle, mainSubLbl, false)
			recalcCanvas()
		end

		mainSub.MouseButton1Click:Connect(showMain)
		themeSub.MouseButton1Click:Connect(showTheme)

		settingsTab:GetPropertyChangedSignal("Visible"):Connect(function()
			local vis = settingsTab.Visible
			mainSub.Visible = vis
			themeSub.Visible = vis
			navDivider.Visible = vis
			if mainBtn then mainBtn.Visible = not vis end
		end)

		showMain()
	end)
end)

-- { Main Loop } --

coroutine.wrap(LPH_NO_VIRTUALIZE(function()
	while true do
		task.wait(0.1)
		kblistGui.Enabled = lib.flags["kbl_enabled"] or false
		if lib.flags["kbl_enabled"] then
			updateKbList()
		end
		watermarkback.Visible = lib.flags["watermark2"] or false
		if lib.flags["watermark2"] then
			if lib.flags["watermarktext"] ~= "none" then
				watermarkLabel.Text = lib.flags["watermarktext"].." | "..fps.." fps | "..tostring(math.floor(client.player:GetNetworkPing()*2000)).." ping"
			else
				watermarkLabel.Text = fps.." fps | "..tostring(math.floor(client.player:GetNetworkPing()*2000)).." ping"
			end
			if type(lib.flags["watermark"]) == "table" then
				watermarkLabel.TextColor3 = Color3.fromRGB(unpack(lib.flags["watermark"]))
			elseif lib.flags["watermark"] then
				watermarkLabel.TextColor3 = lib.flags["watermark"]
			end
		end
		radarGui.Enabled = lib.flags["radar_enabled"] or false
		if lib.flags["radar_enabled"] then
			updateRadar()
		end
	end
end))()

-- { Forcehit Logic } --

local mainEvent = ReplicatedStorage:WaitForChild("MainEvent", 5)
local fhHighlight = Instance.new("Highlight")
fhHighlight.FillColor = Color3.new(0,0,0)
fhHighlight.OutlineColor = Color3.new(1,1,1)
fhHighlight.FillTransparency = 0.5
fhHighlight.OutlineTransparency = 0
fhHighlight.Enabled = false
fhHighlight.Parent = game.CoreGui

local fhLineOutline = Drawing.new("Line")
fhLineOutline.Visible = false
fhLineOutline.Color = Color3.new(0,0,0)
fhLineOutline.Thickness = 3.5
fhLineOutline.Transparency = 1

local fhLine = Drawing.new("Line")
fhLine.Visible = false
fhLine.Color = Color3.new(1,0,0)
fhLine.Thickness = 2
fhLine.Transparency = 1

local fhVisFill = Instance.new("Part")
fhVisFill.Name = "fhVisFill"
fhVisFill.Anchored = true
fhVisFill.CanCollide = false
fhVisFill.CastShadow = false
fhVisFill.Material = Enum.Material.Neon
fhVisFill.Size = Vector3.new(6, 0.15, 6)
fhVisFill.Transparency = 0.4
fhVisFill.Color = Color3.fromRGB(0, 120, 255)
fhVisFill.Parent = workspace
local fhVisFillMesh = Instance.new("SpecialMesh")
fhVisFillMesh.MeshType = Enum.MeshType.Sphere
fhVisFillMesh.Scale = Vector3.new(1, 0.025, 1)
fhVisFillMesh.Parent = fhVisFill
fhVisFill:GetPropertyChangedSignal("Color"):Connect(function() end)

local fhVisOutline = Instance.new("Part")
fhVisOutline.Name = "fhVisOutline"
fhVisOutline.Anchored = true
fhVisOutline.CanCollide = false
fhVisOutline.CastShadow = false
fhVisOutline.Material = Enum.Material.Neon
fhVisOutline.Size = Vector3.new(6.6, 0.15, 6.6)
fhVisOutline.Transparency = 0
fhVisOutline.Color = Color3.new(0, 0, 0)
fhVisOutline.Parent = workspace
local fhVisOutlineMesh = Instance.new("SpecialMesh")
fhVisOutlineMesh.MeshType = Enum.MeshType.Sphere
fhVisOutlineMesh.Scale = Vector3.new(1, 0.025, 1)
fhVisOutlineMesh.Parent = fhVisOutline

_G.__fhTarget = nil
_G.__fhLastFire = 0
_G.__fhLastHealth = {}
_G.__fhStomping = false
_G.__fhArgs = {{},{},Vector3.zero,Vector3.zero,0}
for i = 1, 5 do
	_G.__fhArgs[1][i] = {Normal = Vector3.zero, Instance = nil, Position = Vector3.zero}
	_G.__fhArgs[2][i] = {thePart = nil, theOffset = Vector3.zero}
end

local fhRayParams = RaycastParams.new()
fhRayParams.FilterType = Enum.RaycastFilterType.Exclude

local fhRaycast = LPH_NO_VIRTUALIZE(function(origin, direction, filterList)
	fhRayParams.FilterDescendantsInstances = filterList
	return workspace:Raycast(origin, direction, fhRayParams)
end)

local fhIsKO = LPH_NO_VIRTUALIZE(function(p)
	local c = p.Character
	if not c then return false end
	local b = c:FindFirstChild("BodyEffects")
	return b and b:FindFirstChild("K.O") and b["K.O"].Value
end)

local fhShoot = LPH_NO_VIRTUALIZE(function(target)
	local c = target.Character
	if not c or c:FindFirstChildOfClass("ForceField") then return end
	local hitPart = c:FindFirstChild(lib.flags["fh_hitpart"] or "Head")
	local myChar = client.player.Character
	if not myChar then return end
	local myRoot = myChar:FindFirstChild("HumanoidRootPart")
	if not hitPart or not myRoot then return end
	for i = 1, 5 do
		_G.__fhArgs[1][i].Normal = hitPart.Position
		_G.__fhArgs[1][i].Instance = hitPart
		_G.__fhArgs[1][i].Position = hitPart.Position
		_G.__fhArgs[2][i].thePart = hitPart
		_G.__fhArgs[2][i].theOffset = Vector3.zero
	end
	_G.__fhArgs[3] = myRoot.Position
	_G.__fhArgs[4] = myRoot.Position
	_G.__fhArgs[5] = workspace:GetServerTimeNow()
	if mainEvent then mainEvent:FireServer("Shoot", _G.__fhArgs) end
end)

local function fhStomp(target)
	if _G.__fhStomping then return end
	_G.__fhStomping = true
	task.spawn(function()
		local myChar = client.player.Character
		local myRoot = myChar and myChar:FindFirstChild("HumanoidRootPart")
		local myHum = myChar and myChar:FindFirstChildOfClass("Humanoid")
		if not myRoot or not myHum then _G.__fhStomping = false return end
		local savedCF = myRoot.CFrame
		while lib.flags["fh_autostomp"] and target do
			local tc = target.Character
			if not tc then break end
			local b = tc:FindFirstChild("BodyEffects")
			local ko = b and b:FindFirstChild("K.O") and b["K.O"].Value
			local dead = b and b:FindFirstChild("Dead") and b["Dead"].Value
			if ko and not dead then
				local ut = tc:FindFirstChild("UpperTorso")
				if ut then
					pcall(function()
						myHum.Sit = false
						myHum.PlatformStand = false
						myHum:ChangeState(Enum.HumanoidStateType.GettingUp)
						myRoot.Velocity = Vector3.zero
						myRoot.CFrame = CFrame.new(ut.Position + Vector3.new(0, 3.5, 0))
					end)
					runService.RenderStepped:Wait()
					for i = 1, 5 do task.spawn(function() if mainEvent then mainEvent:FireServer("Stomp") end end) end
				end
			else break end
			task.wait()
		end
		pcall(function()
			local r = client.player.Character and client.player.Character:FindFirstChild("HumanoidRootPart")
			if r then r.CFrame = savedCF end
		end)
		_G.__fhStomping = false
	end)
end

local fhGetClosest = LPH_NO_VIRTUALIZE(function()
	local best, bestDist = nil, math.huge
	local mouse = userInputService:GetMouseLocation()
	local cam = workspace.CurrentCamera
	local checks = _G.__fhChecks or {}
	local myTeam = client.player.Team
	local myChar = client.player.Character
	local myRoot = myChar and myChar:FindFirstChild("HumanoidRootPart")
	local camPos = cam.CFrame.Position
	for _, p in pairs(playerService:GetPlayers()) do
		if p ~= client.player then
			local c = p.Character
			if c then
				local hum = c:FindFirstChildOfClass("Humanoid")
				if hum and hum.Health > 0 then
					local skip = false
					if checks["team check"] and myTeam and p.Team == myTeam then skip = true end
					if not skip and checks["ko check"] and fhIsKO(p) then skip = true end
					if not skip then
						local part = c:FindFirstChild(lib.flags["fh_hitpart"] or "Head")
						if part then
							if checks["visible check"] and myRoot then
								local dir = part.Position - camPos
								local result = fhRaycast(camPos, dir, {myChar})
								if result and not result.Instance:IsDescendantOf(c) then skip = true end
							end
							if not skip then
								local pos, vis = cam:WorldToViewportPoint(part.Position)
								if vis and pos.Z > 0 then
									local d = (Vector2.new(pos.X, pos.Y) - mouse).Magnitude
									if d < bestDist then bestDist, best = d, p end
								end
							end
						end
					end
				end
			end
		end
	end
	return best
end)

local fhGetCooldown = LPH_NO_VIRTUALIZE(function()
	local cd = lib.flags["fh_cooldown"] or 1
	if cd <= 0.15 then return 0 end
	return cd
end)

local fhGetInterval = LPH_NO_VIRTUALIZE(function()
	local rate = lib.flags["fh_firerate"] or 30
	if rate >= 100 then return 0 end
	return 1 / rate
end)

local fhNextFire = 0

local fhStrafeAngle = 0

local function fhExpandHitbox(char)
	if not lib.flags["fh_hitboxexpand"] then return end
	if not char then return end
	local knife = char:FindFirstChild("[Knife]")
	if not knife then
		for _, t in pairs(client.player:FindFirstChildOfClass("Backpack"):GetChildren()) do
			if t:IsA("Tool") and t.Name == "[Knife]" then knife = t break end
		end
	end
	if knife then
		local handle = knife:FindFirstChild("Handle")
		if handle then
			local hitbox = handle:FindFirstChild("HITBOX_PART")
			if hitbox then
				hitbox.Size = Vector3.new(35, 35, 35)
			end
		end
	end
end

local function fhExpandHitboxAll()
	pcall(function()
		local char = client.player.Character
		if char then fhExpandHitbox(char) end
		local bp = client.player:FindFirstChildOfClass("Backpack")
		if bp then
			for _, t in pairs(bp:GetChildren()) do
				if t:IsA("Tool") and t.Name == "[Knife]" then
					local handle = t:FindFirstChild("Handle")
					if handle then
						local hitbox = handle:FindFirstChild("HITBOX_PART")
						if hitbox then hitbox.Size = Vector3.new(35, 35, 35) end
					end
				end
			end
		end
	end)
end

client.player.CharacterAdded:Connect(function(char)
	fhExpandHitbox(char)
	char:WaitForChild("[Knife]", 10)
	fhExpandHitbox(char)
end)

task.spawn(LPH_NO_VIRTUALIZE(function()
	while true do
		task.wait(0.5)
		if lib.flags["fh_hitboxexpand"] then
			pcall(fhExpandHitboxAll)
		end
	end
end))

local fhConn
fhConn = runService.RenderStepped:Connect(LPH_NO_VIRTUALIZE(function()
	if not lib.flags["fh_enabled"] then
		fhHighlight.Enabled = false
		fhLine.Visible = false
		fhLineOutline.Visible = false
		fhVisFill.Transparency = 1
		fhVisOutline.Transparency = 1
		if _G.__fhTarget then
			if lib.flags["fh_targetnotifs"] then notify("ragebot unlocked " .. _G.__fhTarget.Name) end
			_G.__fhTarget = nil
		end
		if lib.flags["fh_spectate"] then
			local cam = workspace.CurrentCamera
			cam.CameraType = Enum.CameraType.Custom
			cam.CameraSubject = client.player.Character and client.player.Character:FindFirstChildOfClass("Humanoid")
		end
		return
	end

	local myChar = client.player.Character
	local myRoot = myChar and myChar:FindFirstChild("HumanoidRootPart")
	if not myRoot then fhHighlight.Enabled = false; fhLine.Visible = false; fhLineOutline.Visible = false; fhVisFill.Transparency = 1; fhVisOutline.Transparency = 1; return end

	local target = _G.__fhTarget

	if target and lib.flags["fh_sticky"] then
		-- retarget on respawn: if target left, clear
		if not target.Parent or not target.Character then
			-- check if they respawned
			local found = false
			for _, p in pairs(playerService:GetPlayers()) do
				if p == target then found = true break end
			end
			if not found then
				_G.__fhTarget = nil
				fhHighlight.Enabled = false
				fhLine.Visible = false
				fhLineOutline.Visible = false
				fhVisFill.Transparency = 1
				fhVisOutline.Transparency = 1
				return
			end
			-- target still in game but no character yet (respawning), keep targeting
			fhHighlight.Enabled = false
			fhLine.Visible = false
			fhLineOutline.Visible = false
			fhVisFill.Transparency = 1
			fhVisOutline.Transparency = 1
			return
		end
		local tc = target.Character
		if tc then
			local th = tc:FindFirstChildOfClass("Humanoid")
			local tp = tc:FindFirstChild(lib.flags["fh_hitpart"] or "Head")
			local ko = fhIsKO(target)
			if not th or th.Health <= 0 or not tp or ko then
				if lib.flags["fh_autostomp"] and ko then
					fhHighlight.Enabled = false
					fhLine.Visible = false
					fhLineOutline.Visible = false
					fhVisFill.Transparency = 1
					fhVisOutline.Transparency = 1
					fhStomp(target)
					return
				else
					fhHighlight.Enabled = false
					fhLine.Visible = false
					fhLineOutline.Visible = false
					fhVisFill.Transparency = 1
					fhVisOutline.Transparency = 1
					_G.__fhTarget = nil
					return
				end
			end
		else
			fhHighlight.Enabled = false
			fhLine.Visible = false
			fhLineOutline.Visible = false
			fhVisFill.Transparency = 1
			fhVisOutline.Transparency = 1
			_G.__fhTarget = nil
			return
		end
		-- sticky target valid, keep it
		local sChar = target.Character
		local sRoot = sChar and sChar:FindFirstChild("HumanoidRootPart")
		if sChar and lib.flags["fh_highlight"] then
			fhHighlight.Adornee = sChar
			fhHighlight.Enabled = true
		else
			fhHighlight.Enabled = false
		end
		if sRoot then
			local cam = workspace.CurrentCamera
			local pos, vis = cam:WorldToViewportPoint(sRoot.Position)
			if vis and pos.Z > 0 then
				local mouse = userInputService:GetMouseLocation()
				fhLine.Color = lib.flags["fh_tracercolor"] or Color3.fromRGB(0, 120, 255)
				fhLine.Thickness = lib.flags["fh_thickness"] or 2
				fhLineOutline.Color = lib.flags["fh_traceroutline"] or Color3.new(0, 0, 0)
				fhLineOutline.Thickness = (lib.flags["fh_thickness"] or 2) + 1.5
				fhLine.From = mouse
				fhLine.To = Vector2.new(pos.X, pos.Y)
				fhLineOutline.From = mouse
				fhLineOutline.To = Vector2.new(pos.X, pos.Y)
				fhLine.Visible = lib.flags["fh_tracer"]
				fhLineOutline.Visible = lib.flags["fh_tracer"]
			else
				fhLine.Visible = false
				fhLineOutline.Visible = false
			end
		end
		-- target strafe
		if lib.flags["fh_strafe"] and not _G.__fhStomping and sRoot then
				local method = lib.flags["fh_strafemethod"] or "orbit"
			local speed = lib.flags["fh_strafespeed"] or 5
			local height = lib.flags["fh_strafeheight"] or 3
			local range = lib.flags["fh_swaferange"] or 5
			pcall(function()
				if method == "orbit" then
					fhStrafeAngle = fhStrafeAngle + (speed * 0.03)
					local offset = Vector3.new(math.cos(fhStrafeAngle) * range, height, math.sin(fhStrafeAngle) * range)
					local targetPos = sRoot.Position + offset
					myRoot.AssemblyLinearVelocity = Vector3.zero
					myRoot.CFrame = CFrame.new(targetPos, sRoot.Position)
				elseif method == "random" then
					local rAngle = math.random() * math.pi * 2
					local rRange = math.random() * range
					local offset = Vector3.new(math.cos(rAngle) * rRange, math.random() * height, math.sin(rAngle) * rRange)
					local targetPos = sRoot.Position + offset
					myRoot.AssemblyLinearVelocity = Vector3.zero
					myRoot.CFrame = CFrame.new(targetPos, sRoot.Position)
				end
			end)
		end
		-- face target
		if lib.flags["fh_facetarget"] and sRoot and myRoot then
			pcall(function()
				myRoot.CFrame = CFrame.new(myRoot.Position, Vector3.new(sRoot.Position.X, myRoot.Position.Y, sRoot.Position.Z))
			end)
		end
		-- spectate
		if lib.flags["fh_spectate"] and sChar then
			local sHum = sChar:FindFirstChildOfClass("Humanoid")
			if sHum then
				local cam = workspace.CurrentCamera
				if cam.CameraSubject ~= sHum then
					cam.CameraType = Enum.CameraType.Custom
					cam.CameraSubject = sHum
				end
			end
		end
		-- visualizer (sticky)
		if lib.flags["fh_visualizer"] and sRoot then
			local range = lib.flags["fh_swaferange"] or 5
			local fillC = lib.flags["fh_visfillcolor"] or Color3.fromRGB(0, 120, 255)
			local outlineC = lib.flags["fh_visoutlinecolor"] or Color3.new(0, 0, 0)
			local sTorso = sChar and (sChar:FindFirstChild("UpperTorso") or sChar:FindFirstChild("Torso"))
			local torPos = sTorso and sTorso.Position or sRoot.Position
			local sz = range * 0.8
			fhVisFill.Size = Vector3.new(sz, 0.15, sz)
			fhVisFill.Position = Vector3.new(torPos.X, torPos.Y, torPos.Z)
			fhVisFill.Color = fillC
			fhVisFill.Transparency = 0.4
			fhVisOutline.Size = Vector3.new(sz + 0.3, 0.15, sz + 0.3)
			fhVisOutline.Position = Vector3.new(torPos.X, torPos.Y - 0.02, torPos.Z)
			fhVisOutline.Color = outlineC
			fhVisOutline.Transparency = 0
		else
			fhVisFill.Transparency = 1
			fhVisOutline.Transparency = 1
		end
		if lib.flags["fh_autofire"] and not _G.__fhStomping then
			local now = tick()
			local interval = fhGetInterval()
			local cooldown = fhGetCooldown()
			if now >= fhNextFire then
				fhShoot(target)
				fhNextFire = now + math.max(interval, cooldown)
			end
		end
		-- hit sound (sticky)
		if sChar then
			local sHum2 = sChar:FindFirstChildOfClass("Humanoid")
			if sHum2 then
				local sprev = _G.__fhLastHealth[target]
				local scur = sHum2.Health
				if sprev and scur < sprev then
					if _G.playHitSound then _G.playHitSound() end
				end
				_G.__fhLastHealth[target] = scur
			end
		end
		return
	end

	local closest = fhGetClosest()

	if not closest then
		if _G.__fhTarget then
			if lib.flags["fh_targetnotifs"] then notify("ragebot unlocked " .. _G.__fhTarget.Name) end
			_G.__fhTarget = nil
		end
		fhHighlight.Enabled = false
		fhLine.Visible = false
		fhLineOutline.Visible = false
		fhVisFill.Transparency = 1
		fhVisOutline.Transparency = 1
		return
	end

	if _G.__fhTarget ~= closest then
		if lib.flags["fh_targetnotifs"] then
			if closest then
				notify("ragebot locked on to " .. closest.Name)
			elseif _G.__fhTarget then
				notify("ragebot unlocked " .. _G.__fhTarget.Name)
			end
		end
		_G.__fhTarget = closest
		_G.__fhLastHealth[closest] = nil
	end

	local eChar = closest.Character
	if eChar and lib.flags["fh_highlight"] then
		fhHighlight.Adornee = eChar
		fhHighlight.Enabled = true
	elseif eChar then
		fhHighlight.Enabled = false
	else
		fhHighlight.Enabled = false
	end

	if lib.flags["fh_autofire"] and not _G.__fhStomping then
		local now = tick()
		local interval = fhGetInterval()
		local cooldown = fhGetCooldown()
		if now >= fhNextFire then
			fhShoot(closest)
			fhNextFire = now + math.max(interval, cooldown)
		end
	end

	-- target strafe (non-sticky)
	if lib.flags["fh_strafe"] and not _G.__fhStomping and eChar then
		local ko = fhIsKO(closest)
		if ko and lib.flags["fh_autostomp"] then
			fhStomp(closest)
		elseif not ko then
			local eRoot = eChar:FindFirstChild("HumanoidRootPart")
			if eRoot and myRoot then
			local method = lib.flags["fh_strafemethod"] or "orbit"
			local speed = lib.flags["fh_strafespeed"] or 5
			local height = lib.flags["fh_strafeheight"] or 3
			local range = lib.flags["fh_swaferange"] or 5
			pcall(function()
				if method == "orbit" then
					fhStrafeAngle = fhStrafeAngle + (speed * 0.03)
					local offset = Vector3.new(math.cos(fhStrafeAngle) * range, height, math.sin(fhStrafeAngle) * range)
					local targetPos = eRoot.Position + offset
					myRoot.AssemblyLinearVelocity = Vector3.zero
					myRoot.CFrame = CFrame.new(targetPos, eRoot.Position)
				elseif method == "random" then
					local rAngle = math.random() * math.pi * 2
					local rRange = math.random() * range
					local offset = Vector3.new(math.cos(rAngle) * rRange, math.random() * height, math.sin(rAngle) * rRange)
					local targetPos = eRoot.Position + offset
					myRoot.AssemblyLinearVelocity = Vector3.zero
					myRoot.CFrame = CFrame.new(targetPos, eRoot.Position)
				end
			end)
		end
		end
	end
	-- face target (non-sticky)
	if lib.flags["fh_facetarget"] and eChar and myRoot then
		local eRoot = eChar:FindFirstChild("HumanoidRootPart")
		if eRoot then
			pcall(function()
				myRoot.CFrame = CFrame.new(myRoot.Position, Vector3.new(eRoot.Position.X, myRoot.Position.Y, eRoot.Position.Z))
			end)
		end
	end
	-- spectate (non-sticky)
	if lib.flags["fh_spectate"] and eChar then
		local eHum = eChar:FindFirstChildOfClass("Humanoid")
		if eHum then
			local cam = workspace.CurrentCamera
			if cam.CameraSubject ~= eHum then
				cam.CameraType = Enum.CameraType.Custom
				cam.CameraSubject = eHum
			end
		end
	end
	-- visualizer (non-sticky)
	if lib.flags["fh_visualizer"] and eChar then
		local eRoot2 = eChar:FindFirstChild("HumanoidRootPart")
		if eRoot2 then
			local range = lib.flags["fh_swaferange"] or 5
			local fillC = lib.flags["fh_visfillcolor"] or Color3.fromRGB(0, 120, 255)
			local outlineC = lib.flags["fh_visoutlinecolor"] or Color3.new(0, 0, 0)
			local eTorso = eChar:FindFirstChild("UpperTorso") or eChar:FindFirstChild("Torso")
			local torPos = eTorso and eTorso.Position or eRoot2.Position
			local sz = range * 0.8
			fhVisFill.Size = Vector3.new(sz, 0.15, sz)
			fhVisFill.Position = Vector3.new(torPos.X, torPos.Y, torPos.Z)
			fhVisFill.Color = fillC
			fhVisFill.Transparency = 0.4
			fhVisOutline.Size = Vector3.new(sz + 0.3, 0.15, sz + 0.3)
			fhVisOutline.Position = Vector3.new(torPos.X, torPos.Y - 0.02, torPos.Z)
			fhVisOutline.Color = outlineC
			fhVisOutline.Transparency = 0
		else
			fhVisFill.Transparency = 1
			fhVisOutline.Transparency = 1
		end
	else
		fhVisFill.Transparency = 1
		fhVisOutline.Transparency = 1
	end

	if eChar then
		local eHum = eChar:FindFirstChildOfClass("Humanoid")
		if eHum then
			local prev = _G.__fhLastHealth[closest]
			local cur = eHum.Health
			if prev and cur < prev then
				if _G.playHitSound then _G.playHitSound() end
				fhLine.Visible = false
				fhLineOutline.Visible = false
			end
			_G.__fhLastHealth[closest] = cur
		end
		local eRoot = eChar:FindFirstChild("HumanoidRootPart")
		if eRoot then
			local cam = workspace.CurrentCamera
			local pos, vis = cam:WorldToViewportPoint(eRoot.Position)
			if vis and pos.Z > 0 then
				local mouse = userInputService:GetMouseLocation()
				fhLine.Color = lib.flags["fh_tracercolor"] or Color3.fromRGB(0, 120, 255)
				fhLine.Thickness = lib.flags["fh_thickness"] or 2
				fhLineOutline.Color = lib.flags["fh_traceroutline"] or Color3.new(0, 0, 0)
				fhLineOutline.Thickness = (lib.flags["fh_thickness"] or 2) + 1.5
				fhLine.From = mouse
				fhLine.To = Vector2.new(pos.X, pos.Y)
				fhLineOutline.From = mouse
				fhLineOutline.To = Vector2.new(pos.X, pos.Y)
				fhLine.Visible = lib.flags["fh_tracer"]
				fhLineOutline.Visible = lib.flags["fh_tracer"]
			else
				fhLine.Visible = false
				fhLineOutline.Visible = false
			end
		end
	else
		fhLine.Visible = false
		fhLineOutline.Visible = false
	end
end))

_G.__fhHighlight = fhHighlight
_G.__fhLine = fhLine
_G.__fhConn = fhConn

-- { Knifebot Logic } --
local kbLine = nil
local kbLineOutline = nil
pcall(function()
	kbLine = Drawing.new("Line")
	kbLine.Visible = false
	kbLine.Thickness = 2
	kbLine.Color = Color3.fromRGB(0, 120, 255)
	kbLine.From = Vector2.new(0, 0)
	kbLine.To = Vector2.new(0, 0)
	kbLine.ZIndex = 2
end)
pcall(function()
	kbLineOutline = Drawing.new("Line")
	kbLineOutline.Visible = false
	kbLineOutline.Thickness = 3.5
	kbLineOutline.Color = Color3.new(0, 0, 0)
	kbLineOutline.From = Vector2.new(0, 0)
	kbLineOutline.To = Vector2.new(0, 0)
	kbLineOutline.ZIndex = 1
end)
_G.__kbLine = kbLine
_G.__kbLineOutline = kbLineOutline

local kbTarget = nil

local kbGetClosest = LPH_NO_VIRTUALIZE(function()
	local cam = workspace.CurrentCamera
	local mouse = userInputService:GetMouseLocation()
	local myChar = client.player.Character
	local myRoot = myChar and myChar:FindFirstChild("HumanoidRootPart")
	local useDistCheck = lib.flags["kb_distancecheck"]
	local maxDist = lib.flags["kb_maxdistance"] or 100
	local best, bestDist = nil, math.huge
	for _, p in pairs(playerService:GetPlayers()) do
		if p ~= client.player and p.Character then
			local eRoot = p.Character:FindFirstChild("HumanoidRootPart")
			local eHum = p.Character:FindFirstChildOfClass("Humanoid")
			if eRoot and eHum and eHum.Health > 0 then
				local d3 = nil
				if useDistCheck and myRoot then
					d3 = (myRoot.Position - eRoot.Position).Magnitude
				end
				if not useDistCheck or not d3 or d3 <= maxDist then
				local pos, vis = cam:WorldToViewportPoint(eRoot.Position)
				if vis and pos.Z > 0 then
					local d = (Vector2.new(pos.X, pos.Y) - mouse).Magnitude
					if d < bestDist then
						bestDist = d
						best = p
					end
				end
				end
			end
		end
	end
	return best
end)

coroutine.wrap(LPH_NO_VIRTUALIZE(function()
while true do
	task.wait()
	if lib.flags["kb_connection"] then
		local myChar = client.player.Character
		if myChar then
			local myRoot = myChar:FindFirstChild("HumanoidRootPart")
			if myRoot then
				-- use forcehit target if available, otherwise find closest
				if lib.flags["fh_enabled"] and _G.__fhTarget and _G.__fhTarget.Character then
					local fhRoot = _G.__fhTarget.Character:FindFirstChild("HumanoidRootPart")
					local fhHum = _G.__fhTarget.Character:FindFirstChildOfClass("Humanoid")
					if fhRoot and fhHum and fhHum.Health > 0 then
						kbTarget = _G.__fhTarget
					else
						_G.__fhTarget = nil
						local best = kbGetClosest()
						if best then kbTarget = best end
					end
				else
					local best = kbGetClosest()
					if best then kbTarget = best end
				end
				if kbTarget and kbTarget.Character then
					local kbChar = kbTarget.Character
					local eRoot = kbChar:FindFirstChild("HumanoidRootPart")
					local eHum = kbChar:FindFirstChildOfClass("Humanoid")
					local eBE = kbChar:FindFirstChild("BodyEffects")
					local eKO = eBE and eBE:FindFirstChild("K.O") and eBE["K.O"].Value
					local eDead = eBE and eBE:FindFirstChild("Dead") and eBE["Dead"].Value
					if eRoot and eHum and eHum.Health > 0 then
						local attachPart = lib.flags["kb_attachpart"] or "HumanoidRootPart"
						local targetPart = kbChar:FindFirstChild(attachPart) or eRoot
						pcall(function() eRoot:SetNetworkOwner(client.player) end)
						pcall(function() sethiddenproperty(myRoot, "PhysicsRepRootPart", eRoot) end)
						myRoot.AssemblyLinearVelocity = Vector3.zero
						myRoot.AssemblyAngularVelocity = Vector3.zero
						myRoot.CFrame = targetPart.CFrame
						if lib.flags["kb_resolver"] then
							pcall(function() myRoot.RotVelocity = Vector3.zero end)
							pcall(function() eRoot:SetNetworkOwner(client.player) end)
							pcall(function() sethiddenproperty(myRoot, "PhysicsRepRootPart", eRoot) end)
							myRoot.AssemblyLinearVelocity = Vector3.zero
							myRoot.AssemblyAngularVelocity = Vector3.zero
							myRoot.CFrame = targetPart.CFrame
						end
						if lib.flags["kb_autoswing"] then
							local now = tick()
							local lastSwing = _G.__kbLastSwing or 0
							local delay = lib.flags["kb_swingdelay"] or 0
							if now - lastSwing >= delay then
								pcall(function()
									for _, tool in pairs(myChar:GetChildren()) do
										if tool:IsA("Tool") then
											tool:Activate()
											_G.__kbLastSwing = now
											break
										end
									end
								end)
							end
						end
						local cam = workspace.CurrentCamera
						if lib.flags["kb_tracer"] and kbLine and kbLineOutline then
							local pos2, vis2 = cam:WorldToViewportPoint(eRoot.Position)
							if vis2 and pos2.Z > 0 then
								local tColor = Color3.fromRGB(0, 120, 255)
								local oColor = Color3.new(0, 0, 0)
								local mouse = userInputService:GetMouseLocation()
								pcall(function()
									kbLine.Thickness = lib.flags["kb_tracerthickness"] or 2
									kbLine.Color = tColor or Color3.fromRGB(0, 120, 255)
									kbLineOutline.Thickness = (lib.flags["kb_tracerthickness"] or 2) + 1.5
									kbLineOutline.Color = oColor or Color3.new(0, 0, 0)
									kbLine.From = mouse
									kbLine.To = Vector2.new(pos2.X, pos2.Y)
									kbLineOutline.From = mouse
									kbLineOutline.To = Vector2.new(pos2.X, pos2.Y)
									kbLine.Visible = true
									kbLineOutline.Visible = true
								end)
							else
								pcall(function() kbLine.Visible = false end)
								pcall(function() kbLineOutline.Visible = false end)
							end
						elseif kbLine and kbLineOutline then
							pcall(function() kbLine.Visible = false end)
							pcall(function() kbLineOutline.Visible = false end)
						end
						local eHum2 = kbChar:FindFirstChildOfClass("Humanoid")
						if eHum2 then
							if cam.CameraSubject ~= eHum2 then
								cam.CameraType = Enum.CameraType.Custom
								cam.CameraSubject = eHum2
							end
						end
					else
						if lib.flags["kb_autostomp"] and eKO and not eDead then
							local torso = kbChar:FindFirstChild("UpperTorso") or kbChar:FindFirstChild("Torso")
							if torso then
								pcall(function()
									myRoot.AssemblyLinearVelocity = Vector3.zero
									myRoot.AssemblyAngularVelocity = Vector3.zero
									myRoot.CFrame = torso.CFrame + Vector3.new(0, 3.5, 0)
								end)
								for i = 1, 5 do
									pcall(function()
										if mainEvent then
											mainEvent:FireServer("Stomp")
										end
									end)
								end
							end
						else
							kbTarget = nil
							if kbLine then pcall(function() kbLine.Visible = false end) end
							if kbLineOutline then pcall(function() kbLineOutline.Visible = false end) end
						end
					end
				else
					kbTarget = nil
					if kbLine then pcall(function() kbLine.Visible = false end) end
					if kbLineOutline then pcall(function() kbLineOutline.Visible = false end) end
				end
			end
		else
			kbTarget = nil
			if kbLine then pcall(function() kbLine.Visible = false end) end
			if kbLineOutline then pcall(function() kbLineOutline.Visible = false end) end
			local cam = workspace.CurrentCamera
			local myChar = client.player.Character
			if myChar then
				local myHum = myChar:FindFirstChildOfClass("Humanoid")
				if myHum and cam.CameraSubject ~= myHum then
					cam.CameraType = Enum.CameraType.Custom
					cam.CameraSubject = myHum
				end
			end
		end
	end
	end
end))()

-- { Auto Reload } --
local __autoReloadLast = {}
task.spawn(LPH_NO_VIRTUALIZE(function()
	while true do
		task.wait()
		if lib.flags["autoreload"] then
			local char = client.player.Character
			if char then
				for _, name in ipairs({"[Revolver]","[DoubleBarrel]","[TacticalShotgun]","[SMG]","[Shotgun]","[Silencer]"}) do
					local t = char:FindFirstChild(name)
					if t and (not __autoReloadLast[name] or tick() - __autoReloadLast[name] >= 1) then
						local s = t:FindFirstChild("Script")
						local a = s and s:FindFirstChild("Ammo")
						if a and a:IsA("IntValue") and a.Value == 0 then
							VirtualInputManager:SendKeyEvent(true, Enum.KeyCode.R, false, nil)
							VirtualInputManager:SendKeyEvent(false, Enum.KeyCode.R, false, nil)
							__autoReloadLast[name] = tick()
						end
					end
				end
			end
		end
	end
end))

-- { Chat Spy } --
task.spawn(LPH_NO_VIRTUALIZE(function()
	local spyGui = Instance.new("ScreenGui")
	spyGui.Name = " "
	spyGui.ResetOnSpawn = false
	spyGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
	spyGui.Parent = game.CoreGui
	spyGui.Enabled = false

	local spyBack = Instance.new("Frame")
	spyBack.Name = "spyBack"
	spyBack.Parent = spyGui
	spyBack.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
	spyBack.BorderSizePixel = 0
	spyBack.Size = UDim2.new(0, 280, 0, 200)
	spyBack.Position = UDim2.new(0, 20, 0, 260)
	Instance.new("UICorner", spyBack).CornerRadius = UDim.new(0, 6)
	local spyStroke = Instance.new("UIStroke")
	spyStroke.Parent = spyBack
	spyStroke.Color = Color3.fromRGB(15, 15, 15)
	spyStroke.Thickness = 1

	do
		local dragging, dragInput, dragStart, startPos
		spyBack.InputBegan:Connect(function(input)
			if input.UserInputType == Enum.UserInputType.MouseButton1 then
				dragging = true
				dragStart = input.Position
				startPos = spyBack.Position
				input.Changed:Connect(function()
					if input.UserInputState == Enum.UserInputState.End then
						dragging = false
					end
				end)
			end
		end)
		spyBack.InputChanged:Connect(function(input)
			if input.UserInputType == Enum.UserInputType.MouseMovement then
				dragInput = input
			end
		end)
		userInputService.InputChanged:Connect(function(input)
			if input == dragInput and dragging then
				local delta = input.Position - dragStart
				spyBack.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
			end
		end)
	end

	local spyTitle = Instance.new("TextLabel")
	spyTitle.Name = "spyTitle"
	spyTitle.Parent = spyBack
	spyTitle.BackgroundTransparency = 1
	spyTitle.Position = UDim2.new(0, 0, 0, 4)
	spyTitle.Size = UDim2.new(1, 0, 0, 14)
	spyTitle.Font = Enum.Font.Arial
	spyTitle.Text = "chat spy"
	spyTitle.TextColor3 = Color3.fromRGB(208, 208, 208)
	spyTitle.TextSize = 10
	spyTitle.TextStrokeTransparency = 0.5
	spyTitle.TextXAlignment = Enum.TextXAlignment.Center

	local spyLine = Instance.new("Frame")
	spyLine.Name = "spyLine"
	spyLine.Parent = spyBack
	spyLine.BackgroundColor3 = lib.accent or Color3.fromRGB(218, 154, 169)
	spyLine.BorderSizePixel = 0
	spyLine.Position = UDim2.new(0, 6, 0, 18)
	spyLine.Size = UDim2.new(1, -12, 0, 1)
	table.insert(lib.accentItems, spyLine)

	local spyHolder = Instance.new("ScrollingFrame")
	spyHolder.Name = "spyHolder"
	spyHolder.Parent = spyBack
	spyHolder.BackgroundTransparency = 1
	spyHolder.Position = UDim2.new(0, 8, 0, 22)
	spyHolder.Size = UDim2.new(1, -16, 1, -26)
	spyHolder.BorderSizePixel = 0
	spyHolder.ScrollBarThickness = 2
	spyHolder.ScrollBarImageColor3 = lib.accent or Color3.fromRGB(218, 154, 169)
	spyHolder.CanvasSize = UDim2.new(0, 0, 0, 0)
	spyHolder.AutomaticCanvasSize = Enum.AutomaticSize.Y
	local spyLayout = Instance.new("UIListLayout", spyHolder)
	spyLayout.SortOrder = Enum.SortOrder.LayoutOrder
	spyLayout.Padding = UDim.new(0, 2)

	local maxMessages = 50
	local msgCount = 0

	local function addSpyMessage(plrName, message)
		msgCount = msgCount + 1
		local entry = Instance.new("TextLabel")
		entry.Name = "spyEntry"
		entry.Parent = spyHolder
		entry.BackgroundTransparency = 1
		entry.Size = UDim2.new(1, 0, 0, 0)
		entry.AutomaticSize = Enum.AutomaticSize.Y
		entry.Font = Enum.Font.Arial
		entry.Text = plrName .. ": " .. message
		entry.TextColor3 = Color3.fromRGB(182, 182, 182)
		entry.TextSize = 11
		entry.TextStrokeTransparency = 0.35
		entry.TextWrapped = true
		entry.TextXAlignment = Enum.TextXAlignment.Left
		entry.TextYAlignment = Enum.TextYAlignment.Top
		entry.LayoutOrder = msgCount
		if msgCount > maxMessages then
			for _, child in pairs(spyHolder:GetChildren()) do
				if child:IsA("TextLabel") and child.LayoutOrder <= msgCount - maxMessages then
					child:Destroy()
				end
			end
		end
	end

	_G.spyGui = spyGui
	_G.spyLine = spyLine
	_G.spyBack = spyBack
	_G.spyStroke = spyStroke
	_G.spyTitle = spyTitle
	_G.spyHolder = spyHolder

	for _, p in pairs(playerService:GetPlayers()) do
		if p ~= client.player then
			p.Chatted:Connect(function(msg)
				if lib.flags["chatspy_enabled"] then
					addSpyMessage(p.Name, msg)
				end
			end)
		end
	end
	playerService.PlayerAdded:Connect(function(p)
		p.Chatted:Connect(function(msg)
			if lib.flags["chatspy_enabled"] then
				addSpyMessage(p.Name, msg)
			end
		end)
	end)

	while true do
		task.wait(0.1)
		pcall(function()
			spyGui.Enabled = lib.flags["chatspy_enabled"] or false
		end)
	end
end))

-- { Anti Void + Anti Stomp } --
task.spawn(LPH_NO_VIRTUALIZE(function()
	while true do
		task.wait(0.1)
		if lib.flags["antivoid"] then
			workspace.FallenPartsDestroyHeight = -math.huge
		else
			workspace.FallenPartsDestroyHeight = -500
		end
		if lib.flags["antistomp"] then
			local myChar = client.player.Character
			if myChar then
				local myHum = myChar:FindFirstChildOfClass("Humanoid")
				local threshold = lib.flags["antisthreshold"] or 29
				if myHum and myHum.Health > 0 and myHum.Health <= threshold then
					myHum.Health = 0
				end
			end
		end
	end
end))
-- { KB Hitbox Expander } --
local function kbExpandHitbox(char)
	if not lib.flags["kb_hitboxexpand"] then return end
	local handle = char:FindFirstChild("[Knife]") and char["[Knife"]:FindFirstChild("Handle")
	if handle then
		local hitbox = handle:FindFirstChild("HITBOX_PART")
		if hitbox then
			hitbox.Size = Vector3.new(35, 35, 35)
		end
	end
end

for _, p in pairs(playerService:GetPlayers()) do
	if p ~= client.player then
		p.CharacterAdded:Connect(function(c) task.wait(0.5) kbExpandHitbox(c) end)
		if p.Character then task.spawn(function() task.wait(0.5) kbExpandHitbox(p.Character) end) end
	end
end
playerService.PlayerAdded:Connect(function(p)
	p.CharacterAdded:Connect(function(c) task.wait(0.5) kbExpandHitbox(c) end)
end)

coroutine.wrap(LPH_NO_VIRTUALIZE(function()
	while true do
		task.wait(0.5)
		if lib.flags["kb_hitboxexpand"] then
			for _, p in pairs(playerService:GetPlayers()) do
				if p ~= client.player and p.Character then
					kbExpandHitbox(p.Character)
				end
			end
		end
	end
end))()

notify("v3nom.cc loaded")

-- { Auto-Disconnect on UI Lock } --
task.spawn(LPH_NO_VIRTUALIZE(function()
	while true do
		task.wait(0.5)
		local ui = nil
		for _, v in pairs(game.CoreGui:GetChildren()) do
			if v:IsA("ScreenGui") and v:FindFirstChild("uiBorder1") then
				ui = v
				break
			end
		end
		if ui then
			ui:GetPropertyChangedSignal("Enabled"):Connect(function()
				if not ui.Enabled then
					if lib.flags["fh_enabled"] then
						lib.flags["fh_enabled"] = false
						if _G.__uiRefs and _G.__uiRefs["fh_enabled"] then
							pcall(function() _G.__uiRefs["fh_enabled"].set(false) end)
						end
					end
					if lib.flags["kb_connection"] then
						lib.flags["kb_connection"] = false
						if _G.__uiRefs and _G.__uiRefs["kb_connection"] then
							pcall(function() _G.__uiRefs["kb_connection"].set(false) end)
						end
					end
				end
			end)
			break
		end
	end
end))


-- Canvas size recalculation loop (enables scrolling)
task.spawn(function()
	task.wait(1)
	while true do
		task.wait(0.5)
		pcall(function()
			for _, tab in pairs(lib.tabframes or {}) do
				local maxY = 0
				for _, s in pairs(tab:GetChildren()) do
					if s:IsA("Frame") then
						local bottom = s.Position.Y.Offset + s.Size.Y.Offset
						if bottom > maxY then maxY = bottom end
					end
				end
				local minCanvas = tab.AbsoluteSize.Y + 50
				if maxY < minCanvas then maxY = minCanvas end
				tab.CanvasSize = UDim2.new(0, 0, 0, maxY + 40)
			end
		end)
	end
end)


-- Spinbot implementation
local spinbotAngle = 0
local spinbotConn
local function spinbotStart()
	if spinbotConn then return end
	local char = client.player.Character
	if not char then return end
	local hrp = char:FindFirstChild("HumanoidRootPart")
	if not hrp then return end
	
	spinbotConn = runService.Heartbeat:Connect(LPH_NO_VIRTUALIZE(function(dt)
		if not lib.flags["spinbot"] then return end
		local char = client.player.Character
		if not char then return end
		local hrp = char:FindFirstChild("HumanoidRootPart")
		if not hrp then return end
		
		local intensity = (lib.flags["spin_intensity"] or 50) / 10
		local method = lib.flags["spin_method"] or "spin"
		
		if method == "spin" then
			spinbotAngle = spinbotAngle + (dt * intensity)
			if spinbotAngle > math.pi * 2 then
				spinbotAngle = spinbotAngle - math.pi * 2
			end
			hrp.CFrame = CFrame.new(hrp.Position) * CFrame.Angles(0, spinbotAngle, 0)
		elseif method == "jitter" then
			local jitter = math.sin(tick() * intensity * 2) * math.rad(180)
			hrp.CFrame = CFrame.new(hrp.Position) * CFrame.Angles(0, jitter, 0)
		elseif method == "anti aim" then
			local aa = math.sin(tick() * intensity) * math.rad(90)
			hrp.CFrame = CFrame.new(hrp.Position) * CFrame.Angles(0, aa, 0)
		end
	end))
end

local function spinbotStop()
	if spinbotConn then
		spinbotConn:Disconnect()
		spinbotConn = nil
	end
end

task.spawn(LPH_NO_VIRTUALIZE(function()
	while true do
		task.wait(0.2)
		if lib.flags["spinbot"] and not spinbotConn then
			pcall(spinbotStart)
		elseif not lib.flags["spinbot"] and spinbotConn then
			spinbotStop()
		end
	end
end))

client.player.CharacterAdded:Connect(function()
	if lib.flags["spinbot"] then
		spinbotStop()
		task.wait(0.25)
		pcall(spinbotStart)
	end
end)
