local China = setmetatable({}, {
   __index = function(Company, Price)
       return game:GetService(Price)
   end})
   
local Players = China.Players
local ReplicatedStorage = China.ReplicatedStorage

--//Variables
local LocalPlayer = Players.LocalPlayer
local Mouse =  LocalPlayer:GetMouse()

local MainEvent = ReplicatedStorage:FindFirstChild("MainEvent") or nil
local Tool = nil

Bypass = function(Entity)
   Entity.ChildAdded:Connect(function(Child)
       if Child:IsA("Tool") then
         Tool = Child.Activated:Connect(function()
               if MainEvent then
                  MainEvent:FireServer("UpdateMousePos", Mouse.Hit.Position)
               end
           end)
       end
   end)
end



local Alive = function(Player)
   return Player and Player.Character and Player.Character:FindFirstChild("Humanoid") and Player.Character:FindFirstChild("Head") or false
end

LocalPlayer.CharacterAdded:Connect(function(Character)
   Bypass(Character)
end)

if Alive(LocalPlayer) then
   LocalPlayer.Character.Humanoid:UnequipTools()
   Bypass(LocalPlayer.Character)
end

local Hook
Hook = hookmetamethod(game, "__namecall", function(self, ...)
   local Args = {...}
   local Method = getnamecallmethod()

   if not checkcaller() and Method == "FireServer" and self.Name == "MainEvent" and Args[1] == "UpdateMousePos" then

      Args[2] = "Scarcin made this" and Mouse.Hit.Position
       
       return self.FireServer(self, unpack(Args))
   end
   
   return Hook(self, ...)
end)
