
            if getgenv().Splitasloaded == true then
            if getgenv().Splitas.Options.Notifications == true then
            
            game.StarterGui:SetCore(
                                "SendNotification",
                                {
                                    Title = "prime leaked ya what can i say",
                                    Text = "Script Already Loaded Copied Settings.",
                                    Duration = 1.5
                                }
                            )
                        end
                return
            end
            getgenv().Splitasloaded = true
            
            if getgenv().Splitas.Options.Notifications == true then
            wait(0.5)
            game.StarterGui:SetCore(
            "SendNotification",
            {
                Title = "PRIME LEAKED U",
                Text = "welcome PRIME SONS.", 
                Duration = 1.5 
            }
            )
            end
        
        
            local Prey
            local Plr
        
            local Players, Client, Mouse, RS, Camera =
            game:GetService("Players"),
            game:GetService("Players").LocalPlayer,
            game:GetService("Players").LocalPlayer:GetMouse(),
            game:GetService("RunService"),
            game:GetService("Workspace").CurrentCamera
        
            local silentcircle = Drawing.new("Circle")
            local tracercircle = Drawing.new("Circle")
           
            silentcircle.Transparency = getgenv().Splitas.Fov.Silent.Transparency
            silentcircle.Thickness = getgenv().Splitas.Fov.Silent.Thickness
            silentcircle.Color = getgenv().Splitas.Fov.Silent.Color
            silentcircle.Filled = getgenv().Splitas.Fov.Silent.Filled
            tracercircle.Transparency = getgenv().Splitas.Fov.Camlock.Transparency
            tracercircle.Thickness = getgenv().Splitas.Fov.Camlock.Thickness
            tracercircle.Color = getgenv().Splitas.Fov.Camlock.Color
            tracercircle.Filled = getgenv().Splitas.Fov.Camlock.Filled
        
            local UpdateFOV = function ()
            if (not silentcircle and not tracercircle) then
                return silentcircle and tracercircle
            end
            tracercircle.Visible  = getgenv().Splitas.Fov.Camlock.Visible
            tracercircle.Radius   = getgenv().Splitas.Fov.Camlock.Size * 2
            tracercircle.Filled = getgenv().Splitas.Fov.Camlock.Filled
            tracercircle.Color = getgenv().Splitas.Fov.Camlock.Color
            tracercircle.Transparency = getgenv().Splitas.Fov.Camlock.Transparency
            tracercircle.Thickness = getgenv().Splitas.Fov.Camlock.Thickness
            tracercircle.Position = Vector2.new(Mouse.X, Mouse.Y + (game:GetService("GuiService"):GetGuiInset().Y))
            
            silentcircle.Visible  = getgenv().Splitas.Fov.Silent.Visible
            silentcircle.Radius   = getgenv().Splitas.Fov.Silent.Size * 2
            silentcircle.Filled = getgenv().Splitas.Fov.Silent.Filled
            silentcircle.Color = getgenv().Splitas.Fov.Silent.Color
            silentcircle.Transparency = getgenv().Splitas.Fov.Silent.Transparency
            silentcircle.Thickness = getgenv().Splitas.Fov.Silent.Thickness
            silentcircle.Position = Vector2.new(Mouse.X, Mouse.Y + (game:GetService("GuiService"):GetGuiInset().Y))
            return silentcircle and tracercircle
            end
        
            RS.Heartbeat:Connect(UpdateFOV)
        
        local WallCheck = function(destination, ignore)
            local Origin    = Camera.CFrame.p
            local CheckRay  = Ray.new(Origin, destination - Origin)
            local Hit = game.workspace:FindPartOnRayWithIgnoreList(CheckRay, ignore)
            return Hit == nil
        end
        
        
        local WTS = function (Object)
            local ObjectVector = Camera:WorldToScreenPoint(Object.Position)
            return Vector2.new(ObjectVector.X, ObjectVector.Y)
        end
        
        local IsOnScreen = function (Object)
            local IsOnScreen = Camera:WorldToScreenPoint(Object.Position)
            return IsOnScreen
        end
        
        local FilterObjs = function (Object)
            if string.find(Object.Name, "Gun") then
                return
            end
            if table.find({"Part", "MeshPart", "BasePart"}, Object.ClassName) then
                return true
            end
        end
        
        local ClosestPlrFromMouse = function()
            local Target, Closest = nil, 1/0
            
            for _ ,v in pairs(Players:GetPlayers()) do
                if getgenv().Splitas.Checks.Wall then
                    if (v.Character and v ~= Client and v.Character:FindFirstChild("HumanoidRootPart")) then
                        wait(0.01)
                        local Position, OnScreen = Camera:WorldToScreenPoint(v.Character.HumanoidRootPart.Position)
                        local Distance = (Vector2.new(Position.X, Position.Y) - Vector2.new(Mouse.X, Mouse.Y)).Magnitude
            
                        if (silentcircle.Radius * 1.27 > Distance and Distance < Closest and OnScreen) and WallCheck(v.Character.HumanoidRootPart.Position, {Client, v.Character}) then
                            Closest = Distance
                            Target = v
                
        
                        end
                    end
                else
                    if (v.Character and v ~= Client and v.Character:FindFirstChild("HumanoidRootPart")) then
                        local Position, OnScreen = Camera:WorldToScreenPoint(v.Character.HumanoidRootPart.Position)
                        local Distance = (Vector2.new(Position.X, Position.Y) - Vector2.new(Mouse.X, Mouse.Y)).Magnitude
            
                        if (silentcircle.Radius * 1.27 > Distance and Distance < Closest and OnScreen) then
                            Closest = Distance
                            Target = v
                        end
                    end
                end
            end
            return Target
        end
        
        local ClosestPlrFromMouse2 = function()
            local Target, Closest = nil, tracercircle.Radius * 1.27
            
            for _ ,v in pairs(Players:GetPlayers()) do
                if (v.Character and v ~= Client and v.Character:FindFirstChild("HumanoidRootPart")) then
                    if getgenv().Splitas.Checks.Wall then
                        local Position, OnScreen = Camera:WorldToScreenPoint(v.Character.HumanoidRootPart.Position)
                        local Distance = (Vector2.new(Position.X, Position.Y) - Vector2.new(Mouse.X, Mouse.Y)).Magnitude
                
                        if (Distance < Closest and OnScreen) and WallCheck(v.Character.HumanoidRootPart.Position, {Client, v.Character}) then
                            Closest = Distance
                            Target = v
                        end
                        else
                            local Position, OnScreen = Camera:WorldToScreenPoint(v.Character.HumanoidRootPart.Position)
                            local Distance = (Vector2.new(Position.X, Position.Y) - Vector2.new(Mouse.X, Mouse.Y)).Magnitude
                
                            if (Distance < Closest and OnScreen) then
                                Closest = Distance
                                Target = v
                            end
                        end
                    end
                end
            return Target
        end
        
        local GetClosestBodyPart = function (character)
            local ClosestDistance = 1/0
            local BodyPart = nil
            
            if (character and character:GetChildren()) then
                for _,  x in next, character:GetChildren() do
                    if FilterObjs(x) and IsOnScreen(x) then
                        local Distance = (WTS(x) - Vector2.new(Mouse.X, Mouse.Y)).Magnitude
                        if (silentcircle.Radius * 1.27 > Distance and Distance < ClosestDistance) then
                            ClosestDistance = Distance
                            BodyPart = x
                        end
                    end
                end
            end
            return BodyPart
        end
        
        local GetClosestBodyPartV2 = function (character)
            local ClosestDistance = 1/0
            local BodyPart = nil
            
            if (character and character:GetChildren()) then
                for _,  x in next, character:GetChildren() do
                    if FilterObjs(x) and IsOnScreen(x) then
                        local Distance = (WTS(x) - Vector2.new(Mouse.X, Mouse.Y)).Magnitude
                        if (Distance < ClosestDistance) then
                            ClosestDistance = Distance
                            BodyPart = x
                        end
                    end
                end
            end
            return BodyPart
        end
        
        Mouse.KeyDown:Connect(function(Key)
            local Keybind = getgenv().Splitas.Camlock.Keybind:lower()
            if (Key == Keybind) then
                if getgenv().Splitas.Camlock.Enabled == true then
                    IsTargetting = not IsTargetting
                    if IsTargetting then
                        Plr = ClosestPlrFromMouse2()
                    else
                        if Plr ~= nil then
                            Plr = nil
                            IsTargetting = false
                        end
                    end
                end
            end
        end)
        
        Mouse.KeyDown:Connect(function(Key)
            local Keybind = getgenv().Splitas.Silent.Keybind:lower()
            if (Key == Keybind) and getgenv().Splitas.Silent.UseKeybind == true then
                    if getgenv().Splitas.Silent.Enabled == true then
                        getgenv().Splitas.Silent.Enabled = false
                        if getgenv().Splitas.Options.Notifications == true then
                            
        game.StarterGui:SetCore(
            "SendNotification",
            {
                Title = "Splitas", 
                Text = "Silent Disabled", 
                Duration = 1.5 
            }
        )
                     end   
                    else
                        getgenv().Splitas.Silent.Enabled = true
                        if getgenv().Splitas.Options.Notifications == true then
                            
        game.StarterGui:SetCore(
            "SendNotification",
            {
                Title = "Splitas", 
                Text = "Silent Enabled", 
                Duration = 1.5 
            }
        )
        end
        end
        end
        end)
        
        local grmt = getrawmetatable(game)
        local backupindex = grmt.__index
        setreadonly(grmt, false)
        
        grmt.__index = newcclosure(function(self, v)
            if (getgenv().Splitas.Silent.Enabled and Mouse and tostring(v) == "Hit") then
                if Prey and Prey.Character then
                    if getgenv().Splitas.Silent.Predict then
                        local endpoint = game.Players[tostring(Prey)].Character[getgenv().Splitas.Silent.Aimpart].CFrame + (
                            game.Players[tostring(Prey)].Character[getgenv().Splitas.Silent.Aimpart].Velocity * getgenv().Splitas.Silent.Prediction
                        )
                        return (tostring(v) == "Hit" and endpoint)
                    else
                        local endpoint = game.Players[tostring(Prey)].Character[getgenv().Splitas.Silent.Aimpart].CFrame
                        return (tostring(v) == "Hit" and endpoint)
                    end
                end
            end
            return backupindex(self, v)
        end)
        
        
        
        RS.Heartbeat:Connect(function()
            if getgenv().Splitas.Silent.Enabled then
                if Prey and Prey.Character and Prey.Character:WaitForChild(getgenv().Splitas.Silent.Aimpart) then
                    if getgenv().Splitas.Resolver.Enabled == true and Prey.Character:WaitForChild("HumanoidRootPart").Velocity.magnitude > 70 then            
                        pcall(function()
                            local TargetVel = Prey.Character[getgenv().Splitas.Silent.Aimpart]
                            TargetVel.Velocity = Vector3.new(0, 0, 0)
                            TargetVel.AssemblyLinearVelocity = Vector3.new(0, 0, 0)
                    
                        end)
                    end
                    if getgenv().Splitas.Checks.AntiGroundShots == true and Prey.Character:FindFirstChild("Humanoid") == Enum.HumanoidStateType.Freefall then
                        pcall(function()
                            local TargetVelv5 = Prey.Character[getgenv().Splitas.Silent.Aimpart]
                            TargetVelv5.Velocity = Vector3.new(TargetVelv5.Velocity.X, (TargetVelv5.Velocity.Y * 5), TargetVelv5.Velocity.Z)
                            TargetVelv5.AssemblyLinearVelocity = Vector3.new(TargetVelv5.Velocity.X, (TargetVelv5.Velocity.Y * 5), TargetVelv5.Velocity.Z)
                        end)
                    end
                    
                    if getgenv().Splitas.Resolver.Enabled == true then            
                        pcall(function()
                            local TargetVelv2 = Prey.Character[getgenv().Splitas.Silent.Aimpart]
                            TargetVelv2.Velocity = Vector3.new(TargetVelv2.Velocity.X, 0, TargetVelv2.Velocity.Z)
                            TargetVelv2.AssemblyLinearVelocity = Vector3.new(TargetVelv2.Velocity.X, 0, TargetVelv2.Velocity.Z)
                        end)
                    end
                end
            end
        
            if getgenv().Splitas.Camlock.Enabled == true then
                if getgenv().Splitas.Resolver.Enabled == true and Plr and Plr.Character and Plr.Character:WaitForChild(getgenv().Splitas.Camlock.Aimpart) and Plr.Character:WaitForChild("HumanoidRootPart").Velocity.magnitude > 70 then
                    pcall(function()
                        local TargetVelv3 = Plr.Character[getgenv().Splitas.Camlock.Aimpart]
                        TargetVelv3.Velocity = Vector3.new(0, 0, 0)
                        TargetVelv3.AssemblyLinearVelocity = Vector3.new(0, 0, 0)
                    end)
                end
                if getgenv().Splitas.Checks.AntiGroundShots == true and Plr.Character:FindFirstChild("Humanoid") == Enum.HumanoidStateType.Freefall then
                        pcall(function()
                            local TargetVelv5 = Plr.Character[getgenv().Splitas.Camlock.Aimpart]
                            TargetVelv5.Velocity = Vector3.new(TargetVelv5.Velocity.X, (TargetVelv5.Velocity.Y * 5), TargetVelv5.Velocity.Z)
                            TargetVelv5.AssemblyLinearVelocity = Vector3.new(TargetVelv5.Velocity.X, (TargetVelv5.Velocity.Y * 5), TargetVelv5.Velocity.Z)
                        end)
                end
            
                if getgenv().Splitas.Resolver.Enabled == true and Plr and Plr.Character and Plr.Character:WaitForChild(getgenv().Splitas.Camlock.Aimpart) then
                    pcall(function()
                        local TargetVelv4 = Plr.Character[getgenv().Splitas.Camlock.Aimpart]
                        TargetVelv4.Velocity = Vector3.new(TargetVelv4.Velocity.X, 0, TargetVelv4.Velocity.Z)
                        TargetVelv4.AssemblyLinearVelocity = Vector3.new(TargetVelv4.Velocity.X, 0, TargetVelv4.Velocity.Z)
                    end)
                end
            end
        end)
        
        RS.RenderStepped:Connect(function()
            if getgenv().Splitas.Silent.Enabled then
                if getgenv().Splitas.Checks.Knocked == true and Prey and Prey.Character then 
                    local KOd = Prey.Character:WaitForChild("BodyEffects")["K.O"].Value
                    local Grabbed = Prey.Character:FindFirstChild("GRABBING_CONSTRAINT") ~= nil
        
                    if KOd or Grabbed then
                        Prey = nil
                    end
                end
            end
            if getgenv().Splitas.Camlock.Enabled == true then
                if getgenv().Splitas.Checks.Knocked == true and Plr and Plr.Character then 
                    local KOd = Plr.Character:WaitForChild("BodyEffects")["K.O"].Value
                    local Grabbed = Plr.Character:FindFirstChild("GRABBING_CONSTRAINT") ~= nil
        
                    if KOd or Grabbed then
                        Plr = nil
                        IsTargetting = false
                    end
                end
                
                if getgenv().Splitas.Checks.DisableOnDeath == true and Plr and Plr.Character:FindFirstChild("Humanoid") then
        
                    if Plr.Character.Humanoid.health < 0.1 then
                        Plr = nil
                        IsTargetting = false
                    end
                end
                if getgenv().Splitas.Checks.DisableOnDeath == true and Plr and Plr.Character:FindFirstChild("Humanoid") then
        
                    if Client.Character.Humanoid.health < 0.1 then
                        Plr = nil
                        IsTargetting = false
                    end
                end
                if getgenv().Splitas.Checks.DisableOutsideFov == true and Plr and Plr.Character and Plr.Character:WaitForChild("HumanoidRootPart") then
        
                    if
                    Camlock.Radius <
                        (Vector2.new(
                            Camera:WorldToScreenPoint(Plr.Character.HumanoidRootPart.Position).X,
                            Camera:WorldToScreenPoint(Plr.Character.HumanoidRootPart.Position).Y
                        ) - Vector2.new(Mouse.X, Mouse.Y)).Magnitude
                     then
                        Plr = nil
                        IsTargetting = false
                    end
                end
                if getgenv().Splitas.Camlock.Predict and Plr and Plr.Character and Plr.Character:FindFirstChild(getgenv().Splitas.Camlock.Aimpart) then
                    if getgenv().Splitas.Camlock.Shake then
                        local Main = CFrame.new(Camera.CFrame.p,Plr.Character[getgenv().Splitas.Camlock.Aimpart].Position + Plr.Character[getgenv().Splitas.Camlock.Aimpart].Velocity * getgenv().Splitas.Camlock.Prediction +
                        Vector3.new(
                            math.random(-getgenv().Splitas.Camlock.ShakeValue, getgenv().Splitas.Camlock.ShakeValue),
                            math.random(-getgenv().Splitas.Camlock.ShakeValue, getgenv().Splitas.Camlock.ShakeValue),
                            math.random(-getgenv().Splitas.Camlock.ShakeValue, getgenv().Splitas.Camlock.ShakeValue)
                        ) * 0.1)
                        Camera.CFrame = Camera.CFrame:Lerp(Main, getgenv().Splitas.Camlock.SmoothnessValue / 2, Enum.EasingStyle.Elastic, Enum.EasingDirection.InOut, Enum.EasingStyle.Sine, Enum.EasingDirection.Out)
                    else
                        local Main = CFrame.new(Camera.CFrame.p,Plr.Character[getgenv().Splitas.Camlock.Aimpart].Position + Plr.Character[getgenv().Splitas.Camlock.Aimpart].Velocity * getgenv().Splitas.Camlock.Prediction)
                        Camera.CFrame = Camera.CFrame:Lerp(Main, getgenv().Splitas.Camlock.SmoothnessValue / 2, Enum.EasingStyle.Elastic, Enum.EasingDirection.InOut, Enum.EasingStyle.Sine, Enum.EasingDirection.Out)
                    end
                elseif getgenv().Splitas.Camlock.Predict == false and Plr and Plr.Character and Plr.Character:FindFirstChild(getgenv().Splitas.Camlock.Aimpart) then
                    if getgenv().Splitas.Camlock.Shake then
                        local Main = CFrame.new(Camera.CFrame.p,Plr.Character[getgenv().Splitas.Camlock.Aimpart].Position +
                        Vector3.new(
                            math.random(-getgenv().Splitas.Camlock.ShakeValue, getgenv().Splitas.Camlock.ShakeValue),
                            math.random(-getgenv().Splitas.Camlock.ShakeValue, getgenv().Splitas.Camlock.ShakeValue),
                            math.random(-getgenv().Splitas.Camlock.ShakeValue, getgenv().Splitas.Camlock.ShakeValue)
                        ) * 0.1)
                        Camera.CFrame = Camera.CFrame:Lerp(Main, getgenv().Splitas.Camlock.SmoothnessValue / 2, Enum.EasingStyle.Elastic, Enum.EasingDirection.InOut, Enum.EasingStyle.Sine, Enum.EasingDirection.Out)
                    else
                        local Main = CFrame.new(Camera.CFrame.p,Plr.Character[getgenv().Splitas.Camlock.Aimpart].Position)
                        Camera.CFrame = Camera.CFrame:Lerp(Main, getgenv().Splitas.Camlock.SmoothnessValue / 2, Enum.EasingStyle.Elastic, Enum.EasingDirection.InOut, Enum.EasingStyle.Sine, Enum.EasingDirection.Out)
                    end
                end
            end
        end)
        
        task.spawn(function ()
            while task.wait() do
                if getgenv().Splitas.Silent.Enabled then
                    Prey = ClosestPlrFromMouse()
                end
                if Plr then
                    if getgenv().Splitas.Camlock.Enabled and (Plr.Character) and getgenv().Splitas.Camlock.NearestCursorAimpart then
                        
                        getgenv().Splitas.Camlock.Aimpart = tostring(GetClosestBodyPartV2(Plr.Character))
                    end
                end
                if Prey then
                    if getgenv().Splitas.Silent.Enabled and (Prey.Character) and getgenv().Splitas.Silent.NearestCursorAimpart then
                        
                        getgenv().Splitas.Silent.Aimpart = tostring(GetClosestBodyPart(Prey.Character))
                    end
                end
            end
        end)
        
        getgenv().uhpoop = {
            ["Enabled"] = (getgenv().Splitas.GunFov.Enabled),
            ["Double-Barrel SG"] = {["FOV"] = (getgenv().Splitas.GunFov.DoubleBarrel)},
            ["DoubleBarrel"] = {["FOV"] = (getgenv().Splitas.GunFov.DoubleBarrel)}, 
            ["Revolver"] = {["FOV"] = (getgenv().Splitas.GunFov.Revolver)},
            ["SMG"] = {["FOV"] = (getgenv().Splitas.GunFov.Smg)}, 
            ["Shotgun"] = {["FOV"] = (getgenv().Splitas.GunFov.Shotgun)}, 
            ["TacticalShotgun"] = {["FOV"] = (getgenv().Splitas.GunFov.TacticalShotgun)}, 
            ["Silencer"] = {["FOV"] = (getgenv().Splitas.GunFov.Silencer)}, 
            
        }                 
        
        local Script = {Functions = {}}
            Script.Functions.getToolName = function(name)
                local split = string.split(string.split(name, "[")[2], "]")[1]
                return split
            end
            Script.Functions.getEquippedWeaponName = function()
                if (Client.Character) and Client.Character:FindFirstChildWhichIsA("Tool") then
                   local Tool =  Client.Character:FindFirstChildWhichIsA("Tool")
                   if string.find(Tool.Name, "%[") and string.find(Tool.Name, "%]") and not string.find(Tool.Name, "Wallet") and not string.find(Tool.Name, "Phone") then
                      return Script.Functions.getToolName(Tool.Name)
                   end
                end
                return nil
            end
            RS.RenderStepped:Connect(function()
            if Script.Functions.getEquippedWeaponName() ~= nil then
                local WeaponSettings = getgenv().uhpoop[Script.Functions.getEquippedWeaponName()]
                if WeaponSettings ~= nil and getgenv().Splitas.GunFov.Enabled == true then
                    getgenv().Splitas.Fov.Silent.Size = WeaponSettings.FOV
                else
                    getgenv().Splitas.Fov.Silent.Size = getgenv().Splitas.Fov.Silent.Size
                end
            end
        end)
        
        
        local Player = game:GetService("Players").LocalPlayer
                    local Mouse = Player:GetMouse()
                    local SpeedGlitch = false
                    Mouse.KeyDown:Connect(function(Key)
                        if getgenv().Splitas.Macro.Type == "Normal" and getgenv().Splitas.Macro.Enabled == true and Key == getgenv().Splitas.Macro.Keybind then
                            SpeedGlitch = not SpeedGlitch
                            if SpeedGlitch == true then
                                repeat game:GetService("RunService").Heartbeat:wait()
                                    keypress(0x49)
                                    game:GetService("RunService").Heartbeat:wait()
        
                                    keypress(0x4F)
                                    game:GetService("RunService").Heartbeat:wait()
        
                                    keyrelease(0x49)
                                    game:GetService("RunService").Heartbeat:wait()
        
                                    keyrelease(0x4F)
                                    game:GetService("RunService").Heartbeat:wait()
        
                                until SpeedGlitch == false
                            end
                        end
                    end)
        
        getgenv().predictionTable = {
            {20, 0.12588},
            {30, 0.11911},
            {40, 0.12471},
            {50, 0.12766},
            {60, 0.12731},
            {70, 0.12951},
            {80, 0.13181},
            {90, 0.13573},
            {100, 0.13334},
            {110, 0.14552},
            {120, 0.14376},
            {130, 0.15669},
            {140, 0.12234},
            {150, 0.15214},
        }
        while getgenv().Splitas.AutoPrediction.Enabled do
            local ping = game:GetService("Stats").Network.ServerStatsItem["Data Ping"]:GetValueString()
            local pingValue = string.split(ping, " ")[1]
            local pingNumber = tonumber(pingValue-10)
            local prediction = 0
            wait(0.2)
            for i = 1, #predictionTable do
                if pingNumber < predictionTable[i][1] then
                    prediction = predictionTable[i][2]
                    break
                end
        end 
            task.wait(1.89)
            getgenv().Splitas.Silent.Prediction = prediction
            task.wait(0.00054)
            ifelse:
            warn('Auto pred has broken.')
        end
print('hi')
