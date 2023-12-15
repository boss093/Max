local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/Patskorn/GUI/main/Copy-SynapOver.lua"))()

local GUI = library:new("X HUB","[ GAME ]")
local Tab1 = GUI:Tap("Menu 1")
local Tab2 = GUI:Tap("Menu 2")

Wapon = {}
for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do  
    if v:IsA("Tool") then
       table.insert(Wapon ,v.Name)
    end
end
for i,v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do  
    if v:IsA("Tool") then
       table.insert(Wapon, v.Name)
    end
end

MonName = {

  "Baboon",
  "ชื่อมอน",
  "ชื่อมอน",
  "ชื่อมอน",
  "ชื่อมอน",
  "ชื่อมอน",
  "ชื่อมอน"
}


Tab1:Dropdown("Select Weapon",Wapon,function(t)
    	_G.Weapon = t
end)

Tab1:Button("Refresh Weapon",function()
    Wapon = {}
        for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do  
    if v:IsA("Tool") then
       table.insert(Wapon ,v.Name)
    end
end
for i,v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do  
    if v:IsA("Tool") then
       table.insert(Wapon, v.Name)
    end
end
              Weapon_Tab:Refresh(Wapon,true)

end)

Tab1:Label("Farm")

Tab1:Dropdown("Select Monster",MonName,function(t)
    	_G.Monster = t
end)

function TP(CFrame)
    pcall(function()
        game.Players.LocalPlayer.Character:WaitForChild("HumanoidRootPart").CFrame = CFrame
    end)
end


function EquipWeapon(ToolSe)
		if game.Players.LocalPlayer.Backpack:FindFirstChild(ToolSe) then
			Tool = game.Players.LocalPlayer.Backpack:WaitForChild(ToolSe)
			wait(.1)
			game.Players.LocalPlayer.Character.Humanoid:EquipTool(Tool)
	end
end


Tab1:Toggle("Auto Farm Monster",nil,function(value)
        pcall(function()
		_G.Auto_Farm_Monster = true
        _G.NOCLIP = Value
if Value then
    AutoFarmMonster()
    else
        _G.Auto_Farm_Monster = false
        NoclipToFly:Destroy()
       game:GetService("Players").LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip"):Destroy()
          end
     end)
end)

spawn(function()
    pcall(function()
        game:GetService("RunService").Heartbeat:Connect(function()
            if _G.NOCLIPRanbow then
                if not game:GetService("Workspace"):FindFirstChild("LOL") then
                    Paertaiteen = Instance.new("Part")
                    Paertaiteen.Name = "LOL"
                    Paertaiteen.Parent = game.Workspace
                    Paertaiteen.Anchored = true
                    Paertaiteen.Transparency = 1
                    Paertaiteen.Size = Vector3.new(15,0.5,15)
                    Paertaiteen.Material = "Neon"
                elseif game:GetService("Workspace"):FindFirstChild("LOL") then
                    pcall(function()
                    game.Workspace["LOL"].CFrame = CFrame.new(game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.X,game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.Y - 3.92,game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.Z)
                    end)
                end
            else
                if game:GetService("Workspace"):FindFirstChild("LOL") then
                    game:GetService("Workspace"):FindFirstChild("LOL"):Destroy()
                end
            end
        end)
    end)
 end)

function AutoFarmMonster()

    spawn(function()

        while _G.Auto_Farm_Monster == true do wait()
            pcall(function()
                if not game:GetService("Players").LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip") and _G.Auto_Farm_Monster == true then
                    NoclipToFly = Instance.new("BodyVelocity")
                    NoclipToFly.Name = "BodyClip"
                    NoclipToFly.Parent = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart
                    NoclipToFly.MaxForce = Vector3.new(100000,100000,100000)
                    NoclipToFly.Velocity = Vector3.new(0,0,0)
                elseif _G.Auto_Farm_Monster == false then
                    NoclipToFly:Destroy()
                end
                EquipWeapon(tostring(_G.Weapon))
            for i,v in pairs(game:GetService("Workspace").Enemy:GetChildren()) do
                if v:FindFirstChild("Humanoid") and v.Name ~= game.Players.LocalPlayer.Name  then
                    v.Humanoid:ChangeState(11)
                    v.Humanoid:ChangeState(14)
                    v.HumanoidRootPart.Size = Vector3.new(60,60,60)
                    v.HumanoidRootPart.Transparency = 0.5
            if v.Name == tostring(_G.Monster) and v.Humanoid.Health >0 and v.Name ~= " " and v.Name ~= "" then
                chosenDemon = false
                if chosenDemon == false then
				TP(v.HumanoidRootPart.CFrame * CFrame.new(0,5,12))
game.Players.LocalPlayer.Character[_G.Weapon]:Activate()
                v.Humanoid.HealthChanged:Connect(function()
                    if v.Humanoid.Health <= 0 then
                        chosenDemon = true
                               end
                          end)
                     end
                end
           end
      end
end)
      end
           end)
                 end


spawn(function()
	pcall(function()
		game:GetService("RunService").Stepped:Connect(function()
			if _G.NOCLIP == true then
				for i,v in pairs(game:GetService("Players").LocalPlayer.Character:GetDescendants()) do
					if v:IsA("BasePart") then
						v.CanCollide = false    
					end
				end
			end
		end)
	end)
end)
