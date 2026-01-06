# roblox-scripting-portfolio
Beginner Roblox Lua scripting portfolio


# Roblox Scripting Portfolio

Hi, I’m a beginner Roblox scripter.
with about 3 months of scripting knowledge

## Skills
- Roblox Basic LuaU (tables , functions etc)
- TweenService
- RemoteEvents & RemoteFunctions
- GUI scripting
- Touched events
- Vector3 & math.random
- and more!

## Projects




## 1. Growing Part
   local TweenService = game:GetService("TweenService")
local Part = script.Parent

local Info = TweenInfo.new(
	5,	--Length/Time
	Enum.EasingStyle.Sine, -- The Style
	Enum.EasingDirection.Out , --direction 
	1,  -- Repeat start at 0 not 1 , 1 is 2 times
	true,  -- Bolean if you want to reverse
	2 -- Delay
)


local Goals = {  -- the goals you want erg : size , position , brick color etc
	Size =  Vector3.new(15, 5 ,  15) ;  -- the goals use ; as comas for tables not , 
	
}

local makePartBiggerTween = TweenService:Create(Part, Info, Goals)
makePartBiggerTween:Play()




## Simple Buy button  
game.Players.PlayerAdded:Connect(function(plr)
	local leaderstats = Instance.new("Folder", plr)
	leaderstats.Name = "leaderstats"
	
	local coins = Instance.new("IntValue", leaderstats)
	coins.Name = "Coins"
	coins.Value = 50
end)


local BuyButtonRemote = game.ReplicatedStorage.BuyButton



BuyButtonRemote.OnServerInvoke	= function(plr)
	local PurchaseSuccesful = false
	local leaderstats = plr.leaderstats 
	local Coins = leaderstats.Coins
	if Coins.Value >= 50 then
		Coins.Value -=50
		PurchaseSuccesful = true
	end
	
	return PurchaseSuccesful
end



local BuyButtonRemote = game.ReplicatedStorage.BuyButton
local gui = script.Parent
local BuyButton = gui.BuyButton
local Prompt = gui.Prompt


BuyButton.MouseButton1Click:Connect(function()
	local PurchaseSuccesful = BuyButtonRemote:InvokeServer()
	
	if PurchaseSuccesful then
		Prompt.Text = "Purchase Succesful"
		Prompt.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
			
	else
		Prompt.Text = "Purchase Failed"
		Prompt.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
	end
end)

